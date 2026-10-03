# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Vritika22Mandapaka

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58#issuecomment-5974457157

I reproduced #58 against the current implementation.

My plan is to keep the fix within the existing regex-based detector. The current educational-background patterns miss common dismissive phrasing where the bootcamp reference and negative claim are separated by other words. Separately, the `bootcamp graduates/developers` pattern only accepts `lack` or `missing`as the verb, so the existing test phrase `bootcamp graduates can't write production code` is not matched. The age pattern does not cover the reproduced plural-role form such as `young developers can't ...`.

I'll make a bounded update to the relevant `DISMISSIVE_PATTERNS` and `DEMOGRAPHIC_PATTERNS` in `safety/bias_detector.py`, then update only the Issue #58 regression tests whose behavior is actually fixed. I'll also run the full bias-detector test file to make sure positive and neutral educational-background examples remain unflagged.

I am not planning to redesign the detector or claim coverage for every possible biased phrasing. The main risk is overmatching from broader regexes, so theexisting neutral and positive cases will be used as controls.

---

## Your branch

**Branch**

fix/58-bias-detector-patterns

**Evidence**

### Before

Direct Unit 2 reproduction:

`python -c "from safety.bias_detector import BiasDetector; print(BiasDetector.detect_bias('The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education'))"`

Output:

```text
(False, '')
```

Focused regression:

`python -m pytest tests/unit/test_bias_detector.py::TestBiasDetector::test_dismissive_bootcamp_language_detected -v`

Output:

```text
XFAIL
1 xfailed in 0.14s
```

Age regression:

`python -m pytest tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_age_detected -v`

Output:

```text
XFAIL
1 xfailed in 0.15s
```

### After

Re-running the same direct reproduction against `fix/58-bias-detector-patterns`:

`python -c "from safety.bias_detector import BiasDetector; print(BiasDetector.detect_bias('The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education'))"`

Output:

```text
2026-10-03 19:48:32 [warning  ] bias_detected                  reason='Dismissive language about educational background'
(True, 'Dismissive language about educational background')
```

Re-running the bootcamp regression:

`python -m pytest tests/unit/test_bias_detector.py::TestBiasDetector::test_dismissive_bootcamp_language_detected -v`

Output:

```text
tests/unit/test_bias_detector.py::TestBiasDetector::test_dismissive_bootcamp_language_detected PASSED [100%]
1 passed in 0.09s
```

Re-running the age regression:

`python -m pytest tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_age_detected -v`

Output:

```text
tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_age_detected PASSED [100%]
1 passed in 0.08s
```

The complete `tests/unit/test_bias_detector.py` run after the implementation also completed with:

```text
27 passed, 5 xfailed in 0.21s
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- Smoke run (`--limit 3`): 3/3
- First full scored run: 18/20
- Targeted retry (`--only pkg-04,pkg-20`): 2/2
- Final confirming full scored run: 19/20

**Package analysis**

`pkg-20`: My first full run incorrectly accepted this package, while the gold label expected rejection. The candidate comment did not include the AI-use disclosure required by the repository policy, but my original `comment-conventions` check was not explicit enough about enforcing repository-stated disclosure requirements. I revised that check so a plan comment must include any disclosure explicitly required by the repository. After the revision, `pkg-20` was correctly rejected in the targeted retry.

**Check rationale**

I chose the `comment-conventions` check:

> **comment-conventions** — Evidence: The candidate plan comment read against the issue and thread highlights plus the repo-facts block's contribution, communication, and disclosure requirements. Pass condition: Pass only if the comment describes the candidate's own plan, remains consistent with the plan and thread, responds to applicable maintainer direction, and satisfies every applicable repository-stated contribution or disclosure requirement. If the repo explicitly requires AI-use disclosure, the comment must contain the required disclosure details, such as the tool and extent of assistance when those are required; silence does not satisfy an explicit disclosure requirement.

I revised this check after the first full evaluation incorrectly accepted `pkg-20`. The earlier wording did not make an explicit repository-required AI-use disclosure independently enforceable, so a comment could otherwise look consistent with the plan and thread while still violating a stated repository requirement. I chose the current wording to make explicit contribution and disclosure requirements observable without requiring disclosure when the repository does not state one.

**Trade-offs**

Tightening `comment-conventions` fixed the false accept on `pkg-20`, but a stricter convention check could also reject comments that should be accepted. To check for that regression, I re-ran `pkg-04` as a canary alongside `pkg-20` using `--only pkg-04,pkg-20`. The targeted retry scored 2/2: `pkg-20` changed to the correct rejection while `pkg-04` retained its correct result. I therefore kept the disclosure requirement conditional on the repository explicitly requiring it rather than requiring AI disclosure for every repository.

I also accepted the remaining false rejection on `pkg-14` in the final 19/20 run rather than loosening `plan-executable`. Loosening that check enough to accept `pkg-14` risked allowing genuinely unbuildable plans to pass, so I kept the stricter executable-plan boundary.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
