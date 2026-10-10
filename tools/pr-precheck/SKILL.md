---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Decide whether a pull request is ready to submit by evaluating the actual implementation against the issue, the contributor's stated plan, the branch diff, and the evidence supporting the claimed changes.

Treat a PR package as a reviewable collection of artifacts: the issue or issue context, the implementation plan including deviations, the proposed code changes, the draft PR title and description, and the available test evidence.

Judge whether the changes fulfill the stated intent, remain within the declared scope, have credible verification, and provide enough information for a maintainer to review them confidently. Do not substitute writing quality, formatting preferences, or unsupported assumptions for evidence of correct behavior.

Answer one question: **Is this PR ready to submit, or should it be held for correction?**

## Inputs and modes

Operate in exactly one of two modes: **live mode** or **eval mode**. Determine the mode from the user's request and the supplied artifacts before grading.

**Live mode — actual pull request**

Read the following inputs:

1. **Issue:** Read the linked GitHub issue and its relevant discussion to identify the requested behavior, constraints, and acceptance expectations.
2. **Plan:** Read `plan.md` from the working repository, including the diagnosis, scope, proposed approach, test plan, risks, and documented deviations.
3. **Branch diff:** From the repository working copy, run `git diff main...HEAD` (three dots) to inspect all committed changes relative to the default branch. Treat the actual diff as authoritative evidence of what changed, rather than relying on the contributor's description.
4. **PR draft:** Read the proposed PR title and description from `pr_draft.md`, or from the supplied draft PR artifact.
5. **Test evidence:** Read `test_evidence.md` and any supplied test output. Distinguish tests actually executed from tests merely planned or claimed.
6. **Repository standards:** Read the applicable PR template and `docs/CONTRIBUTING.md` to identify review and submission requirements.

For a house-chain exercise, use the corresponding provided plan, diff, issue context, PR draft, test evidence, and repository-standard artifacts from that exercise rather than assuming the student's own PathReview files are the target. Do not substitute unrelated local files.

**Eval mode — packaged evaluation**

Treat the supplied evaluation bundle as the complete evidence universe. Read its included issue context, plan, diff, PR description, tests, and standards where provided.

Do not fetch GitHub pages, inspect the local working repository, or import evidence from outside the bundle. Do not use live-mode scope or voice requirements.

Apply every applicable rubric check and the full accept/reject verdict rule to each bundle. Do not relax the grading criteria because the input is an evaluation package.

If an input is missing, record that absence and apply the rubric's missing-evidence rules. Never invent test results, implementation details, or issue requirements.

## The scope seam (live mode only)

In live mode, read `scope.md` before inspecting the issue, plan, diff, PR draft, or test evidence.

Use the repository identity and any additional restrictions in `scope.md` to determine whether the requested PR review is authorized.

If the repository does not match the configured scope, refuse to grade the PR. Explain which scope requirement was not satisfied and do not produce an accept/reject verdict for the out-of-scope request.

If the repository entry in `scope.md` is missing, blank, or still contains an unfilled placeholder, refuse to proceed. Instruct the user to configure the repository scope before requesting a live review.

Do not infer authorization from the current working directory, the Git remote, or the user's request when `scope.md` does not authorize the target.

In eval mode, ignore `scope.md` completely. Do not apply repository restrictions from the live environment to evaluation bundles.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after confirming that the requested repository is within the configured scope and before evaluating the draft PR title and description.

Apply the voice guide to the contributor's outgoing PR title and description. Check that the language is professional, specific, factual, appropriately concise, and consistent with the repository's documented communication conventions.

When a voice rule is violated, report the exact problematic wording, identify the relevant rule, and recommend a concrete correction. Keep voice feedback separate from the substantive rubric checks.

Do not change an `accept` verdict to `reject` solely because of a voice-guide violation. The rubric and its verdict rule determine submission readiness. If wording also creates a substantive problem, such as an unsupported test claim or an undisclosed deviation, grade that problem under the appropriate rubric check using independent evidence.

In eval mode, ignore `voice-guide.md` entirely. Do not apply live-mode voice requirements to evaluation bundles.

## Component reads

Read `rubric.md`, `procedure.md`, and `references/evidence-guide.md` before beginning substantive grading.

Use `rubric.md` as the authoritative definition of the review checks, their pass/fail conditions, their required or preferred status, and the binary verdict rule. Do not invent additional grading requirements or combine separate checks into a single judgment.

Use `references/evidence-guide.md` to locate the evidence needed for each check. Follow its distinctions between issue requirements, planned changes, actual diff content, test execution, and PR claims. Use only evidence permitted by the current mode.

Execute `procedure.md` in its documented order. Follow its instructions for gathering evidence, running checks, recording grades, and assembling the final verdict. Do not replace the procedure with an improvised workflow.

If `procedure.md` is silent about a necessary step, explicitly report the procedural gap. Do not invent a new step, assume missing evidence exists, or silently bypass the gap.

If `rubric.md` or `procedure.md` is missing, empty, or contains only placeholder instructions rather than usable grading rules, refuse to grade the package. Identify the missing or incomplete component and request that it be completed before continuing.

Keep the responsibilities separate: the rubric decides what constitutes a pass or failure, the procedure controls execution, and the evidence guide identifies where proof can be found.

## Verdict and output

Produce exactly one final submission-readiness verdict: `accept` or `reject`.

Use `accept` only when the PR satisfies the verdict rule defined in `rubric.md` and the evidence supports submission. Use `reject` when the rubric requires the PR to be held for correction. Do not introduce intermediate verdicts such as conditional acceptance.

Report each rubric check using its exact check name, a grade of `pass`, `fail`, or `unclear`, and one concise line of evidence identifying the fact, artifact, or quotation that determined the grade.

Before the structured result, briefly explain the main findings, identify any blocking failures, and distinguish required corrections from optional improvements. In live mode, report voice-guide violations separately without allowing them to independently determine the verdict.

End every completed grading response with the fenced JSON block specified below. Replace the placeholders with the actual PR URL or evaluation bundle ID, check results, and verdict. Ensure the populated JSON is syntactically valid.

The JSON block must be the final content in the response. Do not add explanations, recommendations, or other text after its closing fence.

For requests that must be refused under the scope or component-read rules, explain the refusal instead of manufacturing a grading verdict.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Grade every PR package using observable evidence rather than assumptions, confidence, or presentation quality.

**Evidence first:** For each rubric check, identify the relevant evidence before assigning `pass`, `fail`, or `unclear`. Prefer the actual diff, reproducible test results, issue requirements, and documented deviations over unsupported claims in the PR description.

**Grade the implementation, not the polish:** Evaluate whether the changes satisfy the issue and plan, are adequately tested, and are reviewable. Do not fail an otherwise correct PR solely because its wording or formatting could be improved, unless a specific rubric requirement is violated.

**Rubric authority:** Apply the checks, pass conditions, required/preferred distinctions, and verdict rule defined in `rubric.md`. Do not silently strengthen, weaken, merge, or omit checks. Record separate results for separate responsibilities.

**Procedure authority:** Follow `procedure.md` for the reading order, evidence collection, check execution, and verdict assembly. Report missing procedural instructions rather than improvising an undocumented grading process.

**Unclear evidence:** Assign `unclear` when the available artifacts do not establish whether a check passes or fails. Explain exactly what evidence is missing or ambiguous. If the rubric does not specify how an `unclear` grade affects the verdict, treat `unclear` on a required check as blocking submission and return `reject`. Do not convert uncertainty into a pass.

**Consistent verdicts:** Apply the same substantive standards in live and eval modes. An `accept` must be supported by the rubric's verdict rule; a `reject` must identify the blocking check or evidence gap. Never claim that tests passed, CI succeeded, or an issue was fully resolved without supporting evidence.

Keep feedback actionable: identify the specific problem, cite the deciding evidence, and explain what must change before submission.
