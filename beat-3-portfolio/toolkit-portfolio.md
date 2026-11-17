# Toolkit Portfolio

**Student:** Kamakshi Padma Vritika Mandapaka

## Featured Tools

Throughout AI301, I developed a toolkit to support different stages of contributing to open-source projects, from selecting an issue to verifying a pull request and deciding what to do after it is merged.

I selected Issue Select, Issue Scout, Voice Guard, and Ship Gate as my featured tools because they demonstrate how my judgment evolved through evaluation failures, real repository investigation, Windows compatibility problems, and contribution-readiness checks. These tools also connect to my EcoTrace contribution, which was merged as PR #228 on October 29, 2026, closing issue #211.

**Issue Select**

**What it is, and the judgment hole I wrote:**

Issue Select is a tool I developed in Unit 1 to evaluate whether an open-source issue is a suitable contribution opportunity. It checks whether the repository is active, maintainers are engaged, the work is appropriately scoped, and the issue is not already claimed.

I designed its rubric around four required checks: `maintainer-alive`, `repo-in-use`, `scope-fits`, and `unclaimed`, along with the preferred `maintainer-responsive` check.

My main judgment contribution was defining what counts as an unclaimed issue. I learned that checking the assignee field alone was insufficient because contributors may claim issues through comments without appearing as assignees.

**How it evolved, dated:**

On September 19, 2026, evaluation revealed that Issue Select incorrectly accepted `issue-15`. The issue had no current assignee or open linked pull request, but its comment history contained an unresolved `@zulipbot claim`.

I revised the `unclaimed` criterion to consider the assignee field, linked pull requests, and contributor claims in the captured comment history.

Before the revision, the targeted evaluation incorrectly accepted `issue-15`. After the change, the tool rejected it and matched the expected result.

The final evaluation reached 18/20, meeting the passing threshold.

**Evidence:**

From my Unit 1 evaluation history:

```text
agreement: 0/1 scored items
agreement: 1/1 scored items
agreement: 18/20 scored items  (bar: 18/20: PASS)
```

The final rubric required that unresolved contributor claims be treated as active even when no assignee was recorded.

The tool also helped me select CodePath issue #58, concerning bias-detector patterns that failed to recognize certain forms of dismissive language about educational backgrounds.

This experience taught me that a reliable issue-selection tool needs to examine the evidence behind a status rather than trusting a single GitHub field.

**Issue Scout**

**What it is, and the judgment hole I wrote:**

Issue Scout is a Claude Code skill I used during Units 5 and 6 to evaluate real open-source contribution opportunities.

It considers repository activity, issue status, existing pull requests, maintainer participation, and the scope of the requested work.

My judgment contribution was refining how the tool distinguishes whether an issue is feasible from how difficult it might be.

An issue can be clearly defined and actionable while still requiring unfamiliar technical knowledge or significant investigation. I wanted the tool to communicate that distinction instead of automatically rejecting ambitious work.

**How it evolved, dated:**

On October 24, 2026, I worked with Issue Scout while comparing open-source contribution opportunities.

One candidate was codex-lb issue #1572, involving more ambitious encryption-key work. Another was EcoTrace issue #211, requesting a self-contained FastAPI middleware example.

I selected EcoTrace #211 because it offered a concrete, reviewable contribution. During repository investigation, I discovered that the issue description referenced `StarletteEmissionsMiddleware`, whereas the repository implemented `EcoTraceMiddleware` in `ecotrace.middleware.fastapi`.

Rather than inventing an implementation based on the issue description, I contacted the maintainer. The maintainer confirmed that I should use the existing middleware and supported response headers.

I submitted the contribution as EcoTrace PR #228, **“docs: Add FastAPI emissions tracking example.”** The PR was merged by Zwony on **October 29, 2026, at 5:48 PM EDT**.

Between October 24 and November 1, 2026, I also refined Issue Scout's rubric. I replaced `scope-fits` with `scope-feasible`, requiring an identifiable piece of work rather than assuming that feasible work must be easy.

I introduced three informational difficulty classifications: straightforward, moderate, and ambitious. These classifications communicate implementation difficulty without automatically changing an issue's accept/reject decision.

The earlier rubric snapshot was last modified on October 24, and the revised rubric was saved by November 1. These timestamps establish the revision window rather than its exact editing time.

**Evidence:**

My before-and-after rubric comparison showed:

```text
Before: scope-fits
After:  scope-feasible
```

The revised rubric introduced a difficulty note with three classifications:

```text
straightforward
moderate
ambitious
```

The difficulty note is informational and does not independently determine whether an issue is accepted or rejected.

The retrospective comparison classified EcoTrace #211 as straightforward and codex-lb #1572 as ambitious.

The real contribution also revealed an important issue-description mismatch:

```text
Issue description: StarletteEmissionsMiddleware
Repository implementation: EcoTraceMiddleware
Module: ecotrace.middleware.fastapi
```

After maintainer clarification, I used the existing middleware and supported response headers.

Contribution evidence:

- Issue: https://github.com/Zwony/ecotrace/issues/211
- Merged PR: https://github.com/Zwony/ecotrace/pull/228
- Merge timestamp: October 29, 2026, 21:48:01 UTC
- Merged by: Zwony

Issue Scout helped me find a realistic contribution opportunity, but the actual repository investigation and maintainer communication remained essential.

**Voice Guard**

**What it is, and the judgment hole I wrote:**

Voice Guard is a command-review tool designed to prevent GitHub actions from proceeding when the content being submitted cannot be inspected properly.

It uses a voice guide and a command hook to check GitHub operations before execution.

My judgment contribution involved defining situations where the guard should stop a command rather than allow an action whose message body it cannot review.

This matters because commands that create issues, comments, or pull requests can publish content publicly. A guard should not assume that a command is safe merely because it is syntactically valid.

**How it evolved, dated:**

During October 31–November 1, 2026, I discovered a compatibility problem with the original hook.

The implementation recognized only commands identified as `Bash`, but my development environment used Windows PowerShell.

As a result, PowerShell commands could bypass the hook's processing path.

I modified the tool-name condition to recognize both Bash and PowerShell.

The operational log recorded blocking decisions for GitHub commands whose message bodies could not be read.

**Evidence:**

Exact code change:

```diff
- if payload.get("tool_name") != "Bash":
+ if payload.get("tool_name") not in ("Bash", "PowerShell"):
```

From `guard-log.md`:

```text
2026-11-01 04:05 [hook] stop: no body the guard can read (interactive and --help forms are stopped on purpose) | target: gh pr create --help
```

The log contains seven blocking entries between October 31 and November 1.

The code diff verifies the PowerShell compatibility change, while the log independently demonstrates recorded blocking behavior. The log does not identify the originating shell for each event, so I cannot attribute those specific blocking events to PowerShell.

This experience showed me that a safety mechanism must account for the actual environment in which it operates. A guard that works in one shell may leave an unexpected gap in another.

**Ship Gate**

**What it is, and the judgment hole I wrote:**

Ship Gate is a contribution-readiness tool I used in Unit 7 to determine whether a branch has sufficient evidence and documentation for review.

It combines repository-specific checks with my PR Precheck criteria.

My judgment contribution involved deciding which checks were required, which findings needed explanation, and what evidence a reviewer should receive before evaluating a change.

The tool examines areas such as issue coverage, plan fidelity, test observability, repository checks, diff focus, artifact hygiene, template compliance, disclosure accuracy, and reviewer context.

**How it evolved, dated:**

On November 1, 2026, I ran Ship Gate retrospectively against my EcoTrace FastAPI example branch.

This was after the PR had already merged on October 29, so the gate did not control the original merge.

The first run blocked because the test command was not executed correctly in the Windows environment.

I corrected the command to use the Windows virtual-environment executable.

The next run passed the repository tests but blocked because the supplied review materials lacked important context, including a PR description, implementation plan, and test evidence.

After supplying more documentation, another run identified a missing final newline and incomplete PR-template evidence.

I improved the supplied review documentation and disclosures, then reran the gate.

At 04:41 on November 1, the final retrospective run passed.

**Evidence:**

From `gate-log.md`:

```text
2026-11-01 04:20 [manual]
- verdict: BLOCK

2026-11-01 04:23 [manual]
- verdict: BLOCK

2026-11-01 04:29 [manual]
- verdict: BLOCK

2026-11-01 04:41 [manual]
- verdict: PASS
```

The corrected Windows test command used the virtual-environment Python executable:

```powershell
.\.venv\Scripts\python.exe -m pytest
```

The final run recorded successful execution of the full test suite and scoped FastAPI lint.

All nine required PR Precheck checks passed, along with the preferred reviewer-context check.

The supporting test evidence recorded:

```text
239 passed, 2 skipped
```

The real EcoTrace PR added one file, `examples/fastapi_tracking.py`, with 49 additions and no changes to core package files.

The example provided `GET /health` and `GET /compute` endpoints and demonstrated the existing `EcoTraceMiddleware` response headers:

```text
X-Eco-Carbon-Emitted
X-Eco-Duration
```

Both example endpoints were manually verified with HTTP 200 responses.

The contribution was merged as PR #228 on October 29, 2026, closing issue #211.

Importantly, Ship Gate's final PASS demonstrated that the retrospective evidence met the gate's criteria. It did not establish that the gate approved the original contribution before merging.

The process taught me that passing tests alone is not sufficient for contribution readiness. Reviewers also need accurate descriptions, reproducible verification steps, clear scope, and honest disclosure of limitations.

## Inventory

- **Repro Check — Unit 2:** A reproduction-evidence tool that evaluates whether a reported problem can be demonstrated and whether repository conventions are followed. On September 25, 2026, I refined its `repo-conventions` criterion after a case involving missing required AI disclosure. Its final evaluation reached **20/20 — PASS**.

- **Plan Check — Unit 3:** A tool for evaluating implementation plans against repository conventions and executable scope. On October 3, 2026, I refined its comment-convention checks after a false acceptance involving missing AI disclosure. Its verified final evaluation reached **19/20 — PASS**. A remaining false rejection highlighted the trade-off between strictness and flexibility.

- **PR Precheck — Unit 4:** A pull-request review tool that checks whether the proposed change is focused, supported by evidence, consistent with the plan, and understandable to reviewers. On October 9, 2026, its verified final evaluation reached **18/20 — PASS**, with remaining disagreements about repository-check strictness.

- **PR Monitor — Unit 8:** A monitoring tool that checks pull-request status and proposes appropriate follow-up actions. On November 3, 2026, it detected that EcoTrace PR #228 had merged and suggested a conditional follow-up if issue #211 remained open. I independently checked that the issue was already closed and that I had already thanked the maintainer, so I did not perform the redundant action.

## The Arc

**Beat 1 — Issue Select: Learning to inspect claims**

**Date:** September 19, 2026

**Friction:** Issue Select incorrectly accepted `issue-15` because the absence of an assignee or linked PR did not reveal an unresolved contributor claim in the comments.

**Change:** I revised the `unclaimed` rubric to examine assignees, linked pull requests, and contributor claims in the captured comment history.

**Result:** A targeted rerun correctly rejected `issue-15`, and the final evaluation reached 18/20.

**Beat 2 — Repro Check: Strengthening evidence conventions**

**Date:** September 25, 2026

**Friction:** Repro Check incorrectly accepted a package that did not satisfy a repository-required AI disclosure convention.

**Change:** I strengthened the `repo-conventions` criterion and reran targeted evaluations to verify the revised behavior.

**Result:** The final evaluation reached 20/20, demonstrating improved agreement with the expected judgments.

**Beat 3 — Plan Check and PR Precheck: Learning from evaluation disagreements**

**Dates:** October 3–9, 2026

**Friction:** Plan Check initially accepted a package missing required AI disclosure, while PR Precheck later showed disagreements involving repository-check strictness.

**Change:** I revised Plan Check's comment-convention criterion and examined the remaining disagreements in both tools rather than treating the passing threshold as proof of perfect judgment.

**Result:** Plan Check reached 19/20 and PR Precheck reached 18/20. Both passed, but their remaining disagreements informed my later contribution-readiness checks.

**Beat 4 — Issue Scout and EcoTrace: From opportunity to merged contribution**

**Dates:** October 24–29, 2026

**Friction:** I needed to choose a realistic open-source contribution. During investigation, EcoTrace #211 referenced a middleware class that did not match the current repository implementation.

**Change:** I selected the focused FastAPI example task, inspected the existing code, and asked the maintainer to confirm the correct middleware and response headers.

**Result:** The maintainer clarified the implementation, and EcoTrace PR #228 was merged by Zwony on October 29, 2026, at 5:48 PM EDT.

**Beat 5 — Issue Scout and Voice Guard: Refining judgment and compatibility**

**Dates:** October 31–November 1, 2026

**Friction:** Issue Scout needed to distinguish feasibility from difficulty, while Voice Guard recognized Bash but not PowerShell.

**Change:** I revised Issue Scout's `scope-feasible` criterion and added informational difficulty classifications. I also updated Voice Guard's hook to recognize both Bash and PowerShell.

**Result:** The revised Issue Scout rubric was saved by November 1. Voice Guard's code comparison confirmed the compatibility change, and its log recorded seven blocking events, although the originating shell was not recorded.

**Beat 6 — Ship Gate: Making review evidence explicit**

**Date:** November 1, 2026

**Friction:** Ship Gate's retrospective checks initially failed because of a Windows command-execution problem, missing review context, and incomplete PR-template evidence.

**Change:** I corrected the test command and improved the supporting documentation, test evidence, and disclosures.

**Result:** The gate progressed through three BLOCK verdicts before reaching PASS at 04:41, with all nine required checks and the preferred reviewer-context check passing.

**Beat 7 — PR Monitor: Knowing when not to act**

**Date:** November 3, 2026

**Friction:** PR Monitor suggested a follow-up after detecting that EcoTrace PR #228 had merged, but the proposed action depended on whether the related issue was still open.

**Change:** I independently checked the issue status and previous maintainer communication before deciding whether to act.

**Result:** I confirmed that issue #211 was already closed and that I had already thanked the maintainer. I avoided an unnecessary follow-up.

## Limitations and What's Next

My toolkit now supports multiple stages of the open-source contribution process, but it does not eliminate the need for human judgment.

Issue-selection tools can miss changes in repository status or misunderstand contributor claims. Evaluation scores show performance on specific test packages rather than guaranteed correctness across every GitHub repository.

Command guards also depend on their integration with the execution environment. A guard that fails to recognize a shell or command format may not inspect an action as intended.

Contribution-readiness checks can identify missing evidence, but they cannot guarantee that a reviewer will accept a pull request. They also need to distinguish genuine defects from existing repository problems and documented exceptions.

Finally, PR monitoring can recommend follow-up actions without knowing whether those actions have already been completed outside its recorded state.

My next priorities would be to expand edge-case evaluations, improve compatibility across execution environments, make evidence provenance clearer, and connect the tools into a more consistent contribution workflow. I would also preserve explicit human approval for actions that publish content or communicate with maintainers.

**Tool limits**

**Issue Select:** The final evaluation still disagreed with the expected results for `issue-09` and `issue-20`. Its strict treatment of unresolved claims may also reject issues whose recorded status is incomplete or outdated.

**Issue Scout:** Feasibility and difficulty classifications depend on the available issue information. An actionable issue may still require more time, experience, or clarification than the tool initially predicts. The rubric revision's exact edit time is not established by file timestamps alone.

**Voice Guard:** The recorded blocking log does not identify the originating shell, and the observed events do not prove that every possible GitHub command format is covered.

**Ship Gate:** The final PASS was retrospective and did not establish pre-merge approval. The evaluation accepted an explicitly disclosed missing-newline issue rather than demonstrating that the committed file had been corrected. Existing repository-wide lint failures also remained outside the scoped FastAPI lint result.