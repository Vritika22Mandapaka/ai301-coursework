# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

Ranked read-out

1. ACCEPT — #58 Bias detector patterns are too narrow to match common phrasings (bug, safety, tier-1)
Fit: top-ranked because it sits squarely in the fit profile's lead interest — AI ethics, fairness and bias — while still being a bounded, reproducible Python fix with 9 named failing tests to verify against, no architectural rewrite required.

┌──────────────────────────┬───────┬────────────────────────────────────────────────────────────┐
│          Check           │ Grade │                          Evidence                          │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ maintainer-alive         │ pass  │ 3 human commits by Aburke225 on 2026-09-16, within 90 days │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ repo-in-use              │ pass  │ 0 releases, but 5 default-branch commits within 90 days    │
│                          │       │ (≥2)                                                       │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│                          │       │ Body names the file safety/bias_detector.py, gives a repro │
│ scope-fits               │ pass  │  snippet, and lists 9 failing tests in                     │
│                          │       │ tests/unit/test_bias_detector.py                           │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ unclaimed                │ pass  │ assignees: []; no PRs exist in repo; comments: [] — no     │
│                          │       │ claim to reject                                            │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ maintainer-responsive    │ pass  │ #52: COLLABORATOR Aburke225 replied 6 days after open      │
│ (preferred)              │       │                                                            │
└──────────────────────────┴───────┴────────────────────────────────────────────────────────────┘

2. ACCEPT — #53 PII scrubber fails to redact parenthesized US phone numbers (bug, good first issue, safety, tier-1)
Fit: responsible-AI/data-privacy work with the sharpest scope of the three — one regex, 4 named failing tests, and a good first issue label.

┌───────────────────────────┬───────┬───────────────────────────────────────────────────────────┐
│           Check           │ Grade │                         Evidence                          │
├───────────────────────────┼───────┼───────────────────────────────────────────────────────────┤
│ maintainer-alive          │ pass  │ Same 3 human commits by Aburke225 on 2026-09-16           │
├───────────────────────────┼───────┼───────────────────────────────────────────────────────────┤
│ repo-in-use               │ pass  │ 5 default-branch commits within 90 days                   │
├───────────────────────────┼───────┼───────────────────────────────────────────────────────────┤
│                           │       │ "phone-number pattern in pii_scrubber.py matches dashed   │
│ scope-fits                │ pass  │ formats … but not (555) 123-4567", with repro and 4 named │
│                           │       │  tests                                                    │
├───────────────────────────┼───────┼───────────────────────────────────────────────────────────┤
│ unclaimed                 │ pass  │ assignees: []; no PRs exist in repo; comments: []         │
├───────────────────────────┼───────┼───────────────────────────────────────────────────────────┤
│ maintainer-responsive     │ pass  │ COLLABORATOR reply within 6 days on sampled issue #52     │
│ (preferred)               │       │                                                           │
└───────────────────────────┴───────┴───────────────────────────────────────────────────────────┘

3. ACCEPT — #60 Faithfulness checker crashes when a context chunk has text: None (bug, good first issue, rag, tier-1)
Fit: touches trustworthy-AI/model-evaluation (RAG faithfulness), but it is a single None-guard with one failing test — least depth of the three for the stated goal of understanding an existing codebase.

┌──────────────────────────┬───────┬────────────────────────────────────────────────────────────┐
│          Check           │ Grade │                          Evidence                          │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ maintainer-alive         │ pass  │ Same 3 human commits by Aburke225 on 2026-09-16            │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ repo-in-use              │ pass  │ 5 default-branch commits within 90 days                    │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│                          │       │ "check() builds the context with chunk.get(\"text\", \"\") │
│ scope-fits               │ pass  │  … \" \".join(...) raises TypeError", repro +              │
│                          │       │ test_none_context_chunk_text                               │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ unclaimed                │ pass  │ assignees: []; no PRs exist in repo; comments: []          │
├──────────────────────────┼───────┼────────────────────────────────────────────────────────────┤
│ maintainer-responsive    │ pass  │ COLLABORATOR reply within 6 days on sampled issue #52      │
│ (preferred)              │       │                                                            │
└──────────────────────────┴───────┴────────────────────────────────────────────────────────────┘

No rejected candidates.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last 5 default-branch commits all by human Aburke225; 3 of them dated 2026-09-16, within 90 days of 2026-09-19"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "0 releases, but 5 default-branch commits within 90 days (3 on 2026-09-16, 2 on 2026-08-24); last push 2026-09-16T21:48:27Z, archived: false"},
      {"name": "scope-fits", "grade": "pass", "evidence": "Body names safety/bias_detector.py, gives a runnable repro, and lists 9 failing tests in tests/unit/test_bias_detector.py; labels bug, safety, tier-1"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; gh pr list --state all returns [] so no linked PR; comments: [] so no contributor claim exists"},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Sampled issue #52 opened 2026-09-10T21:37:48Z, first reply 2026-09-16T21:50:02Z by Aburke225 (COLLABORATOR) — 6 days"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "3 human commits by Aburke225 on 2026-09-16, within 90 days of 2026-09-19"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "0 releases, but 5 default-branch commits within 90 days; last push 2026-09-16T21:48:27Z"},
      {"name": "scope-fits", "grade": "pass", "evidence": "Body: phone pattern in pii_scrubber.py misses '(555) 123-4567'; repro snippet plus 4 named failing tests in tests/unit/test_pii_scrubber.py; labeled good first issue, tier-1"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; no PRs exist in the repo; comments: [] so no contributor claim exists"},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Sampled issue #52 received a COLLABORATOR reply from Aburke225 6 days after opening"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "3 human commits by Aburke225 on 2026-09-16, within 90 days of 2026-09-19"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "0 releases, but 5 default-branch commits within 90 days; archived: false"},
      {"name": "scope-fits", "grade": "pass", "evidence": "Body pinpoints chunk.get(\"text\", \"\") returning None and the resulting TypeError in join(), with repro and failing test test_none_context_chunk_text"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; no PRs exist in the repo; comments: [] so no contributor claim exists"},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Sampled issue #52 received a COLLABORATOR reply from Aburke225 6 days after opening"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

- `agreement: 2/3 scored items`
- `agreement: 15/20 scored items`
- `agreement: 4/5 scored items`
- `agreement: 0/1 scored items`
- `agreement: 1/1 scored items`
- `agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

`issue-15`

Rubric decision: `reject`  
Gold label: `reject`

Reasoning: The issue had no current assignee and no open linked pull request, but the captured comment thread ended with a contributor using `@zulipbot claim`. There was no later evidence in the captured thread showing that this final claim was rejected, released, cancelled, or unassigned. Under the final `unclaimed` check, that unresolved claim counts as active, so the required check fails and the overall verdict is `reject`.

**Check rationale**

**Quoted check from rubric.md:**

"unclaimed — Pass only if all three are true: (1) there is no current assignee, (2) there is no open linked pull request implementing the issue, and (3) every contributor claim in the captured comment thread has later evidence explicitly rejecting or ending that claim. A successful claim is indicated by a contributor claim command such as @zulipbot claim or an equivalent explicit statement of intent to work on the issue. If the final/latest claim in the captured thread has no later rejection, cancellation, release, or unassignment, grade this check FAIL even when the repo-facts block says assignees: none."

**Reasoning:** I made this check specific because looking only at the current assignee field was not enough to determine whether someone had already claimed an issue. During evaluation, issue-15 showed that a contributor could claim an issue in the comment thread even when the issue had no current assignee. The final version therefore checks the assignee, linked pull requests, and the captured comment history so that an unresolved contributor claim is treated as claimed.

**Trade-offs**

I re-ran issue-15 with --only while refining the unclaimed check. Before the rule was made more explicit, the rubric still accepted issue-15 even though its gold label was reject. After changing the check to treat a final unresolved contributor claim as active, issue-15 changed to reject and matched the gold label. The trade-off is that this stricter rule may reject an issue when the comment history contains an unresolved claim even if the current assignee field is empty.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. This issue fits my interests because I am interested in responsible AI, especially AI fairness and bias. It also looks manageable within the available time because the problem is clearly scoped to the bias detector and already has specific failing tests that I can use to understand and verify the fix.

2. The verdict correctly identified that the repository is active, the issue has a clear scope, the maintainers are responsive, and the issue was unclaimed when I checked it. What the rubric could not fully weigh was my personal interest in learning how bias detection works in a real AI system. That made issue #58 more interesting to me than the other accepted issues.

3. I expect claiming the issue to be relatively straightforward because, when I evaluated it, there was no assignee, linked pull request, or existing claim in the comments. However, I will check the issue again before claiming it because another contributor could claim it after my evaluation.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
