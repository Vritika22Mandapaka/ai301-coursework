# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**
Vritika22Mandapaka

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58#issuecomment-5841081946

Hi! I'd like to work on issue #58, "Bias detector patterns are too narrow to match common phrasings." I'll test the reported bias-detector patterns against the current implementation, including the common phrasings described in the issue, and document the behavior I observe. I'll report back here with my environment, reproduction steps, and results.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58#issuecomment-5841407925

## Reproduction report for #58

I reproduced the reported bias-detector behavior in my local environment.

### Environment

- OS: Windows
- Python: 3.11.0
- pytest: 9.1.1
- Repository: Vritika22Mandapaka/pathreview-ai301-fa26-s1
- Branch: main
- Test file: `tests/unit/test_bias_detector.py`
- Relevant implementation: `safety/bias_detector.py`

I created a Python 3.11 virtual environment and installed pytest and structlog for this focused unit-test reproduction. I did not modify the source code.

### Steps to reproduce

From the repository root with the virtual environment activated, I ran the issue's reported phrasing directly through `BiasDetector.detect_bias()`:

```powershell
python -c "from safety.bias_detector import BiasDetector; print(BiasDetector.detect_bias('The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education'))"
```

Observed output:

```text
(False, '')
```

I also ran the existing issue-specific unit test:

```powershell
python -m pytest tests/unit/test_bias_detector.py::TestBiasDetector::test_dismissive_bootcamp_language_detected -v
```

Observed result:

```text
tests/unit/test_bias_detector.py::TestBiasDetector::test_dismissive_bootcamp_language_detected XFAIL (issue #58: bias detector patterns are too ...)
1 xfailed in 0.12s
```

I then checked the age/demographic case with:

```powershell
python -m pytest tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_age_detected -v
```

Observed result:

```text
tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_age_detected XFAIL (issue #58: bias detector patterns are too na...)
1 xfailed in 0.13s
```

### Expected behavior

The bootcamp phrasing should be flagged as dismissive educational-background bias rather than returning `(False, '')`.

The existing age test also expects `"young developers can't handle complex systems"` to be detected as biased and to return a reason identifying demographic bias.

### Observed behavior

The issue's bootcamp example returned:

`(False, '')`

The two existing tests associated with issue #58 both produced their expected `XFAIL` results.

### Result

Reproduced. The current bias detector does not flag the issue's reported natural bootcamp phrasing, and the existing issue #58 tests for dismissive bootcamp language and an age-based demographic assumption remain expected failures in this environment.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- Smoke run (`--limit 3`): 3/3 agreement.
- First full evaluation: 19/20 agreement.
- Targeted rerun of `pkg-09`: matched the gold label.
- Next full evaluation: 18/20 agreement.
- Targeted rerun of `pkg-20`: matched the gold label.
- Final confirming full evaluation with `--save-run eval-run.txt`: 20/20 agreement.

**Package analysis**

I analyzed `pkg-20`. My rubric initially accepted the package, while the gold label was reject. The reproduction evidence itself was strong, but the repository required disclosure of AI use in issue comments, and the candidate comments omitted that required disclosure. My original `repo-conventions` check did not make this requirement explicit enough, so it incorrectly focused on the technical reproduction evidence and accepted the package. After reviewing the disagreement, I revised `repo-conventions` so that when a repository requires AI-use disclosure for issues or comments, omitting the required tool or extent disclosure causes that check to fail. After the revision, a targeted rerun of `pkg-20` matched the gold reject label.

**Check rationale**

I revised the `repo-conventions` check after analyzing `pkg-20`.

**Quoted check from `rubric.md`:**

- Pass only if all applicable repository-stated communication, contribution, and AI-use disclosure requirements are satisfied. If the repository requires AI-use disclosure for issues or comments, the candidate claim/repro communication must contain the required disclosure, including any required tool and extent-of-use information; if that required disclosure is absent, fail this check. If the repository explicitly states that issue comments do not require AI disclosure, absence of disclosure does not fail this check. The claim must also identify the specific issue and next investigation or reproduction action without promising a fix or completion date, and the repro communication must report the student's own result rather than relying on another contributor's reproduction.

I revised this check because my earlier version did not make required AI-use disclosure explicit enough. That caused `pkg-20` to be accepted even though its repository required AI-use disclosure in comments and the candidate omitted it. I chose this final wording so the check follows the repository's own rules: missing disclosure fails when disclosure is required, but the rubric does not penalize a package when the repository explicitly says issue comments do not require disclosure. The check also preserves the communication requirements for a specific claim, no fix or completion-date promise, and reporting the student's own reproduction result.

**Trade-offs**

The revised `repo-conventions` check changed the result of `pkg-20`. Before the revision, my rubric accepted `pkg-20` even though the repository required AI-use disclosure in issue comments and the candidate omitted it. I re-ran `pkg-20` as a targeted canary after strengthening the check, and it then matched the gold reject label. The trade-off is that this check is stricter about repository-specific communication rules: a package can have strong technical reproduction evidence and still be rejected when it violates a required disclosure rule. At the same time, the check avoids over-rejecting packages by explicitly allowing no disclosure when the repository states that issue comments do not require it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
