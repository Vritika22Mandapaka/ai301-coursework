# Plan for Issue #58: Broaden bias-detector pattern coverage

## Diagnosis

The reproduced failures are caused by the current regular-expression patterns being narrower than the biased phrasings they are intended to detect.

`BiasDetector.detect_bias()` checks the input against `DISMISSIVE_PATTERNS` and `DEMOGRAPHIC_PATTERNS` using `re.search(..., re.IGNORECASE)` and returns `(False, "")` when no pattern matches. Existing passing tests show that detect_bias() flags phrases already represented by the current patterns, such as bootcamp training is inadequate for professional development, supporting pattern coverage as the source of the reproduced failures rather than the iteration or return logic.

For educational-background bias, the existing patterns expect structures such as `bootcamp graduates lack rigor`, `bootcamp training is inadequate`, or `bootcamp is not comparable to university`. They do not cover the reproduced natural phrasing where the educational reference and dismissive claim are separated by other words.

The existing test `test_dismissive_bootcamp_language_detected` fails for a different reason. Its input, `bootcamp graduates can't write production code`, keeps the words adjacent, but the `(?:bootcamp|self-taught)\s+(?:graduates?|developers?)` pattern only accepts `(?:lack|missing)` as the following verb, so dismissive verbs such as `can't` or `cannot` are not matched.

For demographic bias, the current age pattern expects an age term followed by a singular role such as `young developer` before `can't`, so the reproduced existing test phrase `young developers can't handle complex systems` falls outside that pattern.

Reproduction evidence from Unit 2:

`BiasDetector.detect_bias("The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education")`

Observed: `(False, '')`

Expected: the text is flagged as dismissive educational-background bias.

The existing issue-specific test `test_dismissive_bootcamp_language_detected` also produced:

- `1 xfailed in 0.12s`

The existing demographic test `test_demographic_assumption_age_detected` produced:

- `1 xfailed in 0.13s`

These failures show that common biased phrasings can bypass the current regex coverage.

## Scope

### In scope

- Broaden the existing dismissive educational-background regex coverage for the reproduced/common bootcamp phrasing.
- Widen the dismissive verbs accepted after `bootcamp graduates/developers` to include inability claims such as `can't`.
- Broaden the existing age demographic regex coverage for the reproduced plural-role phrasing.
- Update the corresponding Issue #58 regression tests so fixed cases are expected to pass rather than remain expected failures.
- Preserve the existing bias categories and return values.

### Out of scope

- Replacing the regex-based detector with a new detection architecture.
- Adding an ML/LLM-based bias classifier.
- Changing logging or the `detect_bias()` return structure.
- Broad refactoring of unrelated safety code.
- Claiming coverage for every possible biased phrase or every existing Issue #58 expected-failure case without evidence that the bounded pattern changes cover it.

## Files

- `safety/bias_detector.py`
  - Adjust the relevant entries in `DISMISSIVE_PATTERNS` and `DEMOGRAPHIC_PATTERNS`.

- `tests/unit/test_bias_detector.py`
  - Convert the reproduced Issue #58 cases from expected failures to normal regression tests once the implementation detects them.
  - Keep existing positive and neutral examples as controls against overmatching.

## Approach

1. Extend the educational-background patterns so dismissive bootcamp language can match the reproduced/common phrasing without requiring only the currently supported fixed word order.
2. Widen the verb alternation in the `graduates/developers` dismissive pattern to include inability claims such as `can't` and `cannot`, so `bootcamp graduates can't ...` is matched.
3. Extend the age demographic pattern to recognize the reproduced plural role form such as `young developers can't ...`, while retaining the existing supported singular forms.
4. Keep the changes within the existing `DISMISSIVE_PATTERNS` and `DEMOGRAPHIC_PATTERNS` design rather than changing `detect_bias()` itself.
5. Remove the `xfail` markers only from Issue #58 tests that are covered by and pass because of these changes.
6. Run the focused regression cases and the complete bias-detector test file to check both newly detected biased phrases and existing positive/neutral controls.

## Test plan

After the change:

1. Run the same direct Unit 2 reproduction:
   `BiasDetector.detect_bias("The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education")`

   Expected result: `is_biased` is `True` with the dismissive educational-background reason instead of `(False, '')`.

2. Run:
   `test_dismissive_bootcamp_language_detected`

   Expected result: PASS rather than XFAIL, because `bootcamp graduates can't write production code` now matches the widened verb alternation.

3. Run:
   `test_demographic_assumption_age_detected`

   Expected result: PASS rather than XFAIL, with a demographic reason.

4. Run the full `tests/unit/test_bias_detector.py` suite.

   Expected result: the newly supported cases pass, while existing positive and neutral controls such as positive bootcamp mentions, neutral bootcamp mentions, and clean technical feedback remain unflagged.

## Risks and unknowns

Broadening regex patterns can introduce false positives if the expressions become too permissive. The change should therefore remain tied to recognizable dismissive or demographic-assumption language rather than flagging any mention of a bootcamp or age term.

The test file contains additional Issue #58 expected-failure cases beyond the two reproduced in Unit 2. Some may be addressed by the same bounded pattern changes, but I will not assume that in advance. I will only remove an `xfail` marker when the corresponding behavior is actually covered and verified.

## Deviations

No material deviations from the posted plan. The bounded regex changes also caused `test_coding_bootcamp_variant` and `test_multiple_bias_indicators` to pass, so I removed their strict `xfail` markers after verifying the behavior. Five other Issue #58 expected-failure tests remain unchanged.