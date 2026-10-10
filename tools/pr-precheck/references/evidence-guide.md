# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives**

- **Eval mode:** Read the issue requirements and the plan-context block, especially its scope boundaries, planned files, intended behavior, exclusions, and deviation notes. Compare them with the candidate PR's unified diff, changed-file list, and description.
- **Live mode:** Read the GitHub issue and relevant discussion, `plan.md` and its deviation notes, `git diff main...HEAD`, and the draft PR title and description in `pr_draft.md`.
- **Evidence to record:** List the planned changes beside the actual changes. Identify any material added or omitted behavior, changed files outside the planned boundary, undocumented deviations, and PR claims that contradict the diff.

**What good looks like**

The implementation satisfies the issue's core objective, and every material change is within the planned scope or accurately documented as a deviation. The PR description represents the actual implementation without claiming behavior the diff does not provide.

A change is **silent drift** when the diff introduces unplanned material behavior without disclosure, omits planned material work without explanation, or contradicts the PR's implementation claims. An accurately disclosed limitation does not automatically block submission unless it violates an explicit requirement or defeats the issue's core objective.

**Related rubric checks:** `issue-coverage`, `plan-fidelity`, `description-accuracy`.

## Test evidence (harness category: not-tested)

**Where it lives**

- **Eval mode:** Read the plan-context block's test plan, the candidate PR's test-evidence section, the reproduction steps and expected behavior, and the repo-facts block's required validation commands or testing policy.
- **Live mode:** Read the test plan in `plan.md`, captured commands and outputs in `test_evidence.md`, relevant changed or added tests in `git diff main...HEAD`, and testing requirements in `docs/CONTRIBUTING.md` or the repository's documented tooling.
- **Evidence to record:** Match each planned test or reproduction step to an actual command, observable output, and reported result. Record before-and-after behavior, relevant regression coverage, passing and failing tests, skipped checks, and explanations for tests not run.

**What good looks like**

The evidence identifies the behavior being tested, states the expected result, and provides observable results supporting the implementation's claims. Relevant repository checks have credible outcomes, or missing and failing checks are accurately disclosed with their implications.

A statement such as "all tests pass" without commands, results, reproducible output, or another credible observation is not sufficient proof. An honestly disclosed unrun check or known failure is not automatically disqualifying unless repository policy requires that check to succeed before submission.

**Related rubric checks:** `test-observability`, `repository-checks`.

## Diff quality (harness category: unreviewable)

**Where it lives**

- **Eval mode:** Inspect the candidate PR's unified diff, changed-file list, and commit history. Compare the changed files and hunks with the issue requirements and the plan-context block's scope boundaries.
- **Live mode:** Inspect `git diff main...HEAD`, `git diff main...HEAD --stat`, and `git log main..HEAD --oneline`. Compare the implementation with the planned changes in `plan.md`.
- **Evidence to record:** Identify the files and hunks implementing the intended fix, unrelated changes, unnecessary formatting churn, debugging statements, commented-out code, temporary files, generated artifacts, and machine-specific content. Record exact paths and representative hunks for any problems.

**What good looks like**

The diff makes the intended implementation and relevant tests visible without unrelated work obscuring the change. Every changed file has a defensible connection to the issue, plan, or documented deviation.

The PR should not contain accidental debris such as debug leftovers, dead code, commented-out experiments, unrelated generated output, credentials, or local environment files. A larger diff is not automatically unreviewable when its changes are relevant and clearly organized.

**Related rubric checks:** `diff-focus`, `artifact-hygiene`.

## Standards and comms (harness category: standards-wall)

**Where it lives**

- **Eval mode:** Read the repo-facts block, including the PR template requirements, contributing instructions, mandatory disclosures, and stated repository policies. Compare these requirements with the candidate PR title, description, and relevant issue or maintainer discussion.
- **Live mode:** Read `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, the GitHub issue discussion, and the draft PR title and description in `pr_draft.md`. Review `voice-guide.md` separately for live-mode communication guidance.
- **Evidence to record:** Identify every mandatory template field, required AI-assistance disclosure, testing disclosure, deviation disclosure, and explicit maintainer instruction. Record where the PR addresses each requirement, or identify the missing, misleading, or boilerplate response.

**What good looks like**

The PR substantively answers all applicable mandatory template questions, truthfully discloses AI assistance and relevant testing or implementation limitations, and addresses explicit maintainer directions. An honest `N/A` is acceptable when the requirement genuinely does not apply.

A standards-wall failure occurs when the PR ignores a mandatory template request, omits a required disclosure, substitutes generic boilerplate for substantive information, or disregards an applicable maintainer instruction. Optional style preferences and live-mode voice-guide issues should be reported separately and must not independently determine the accept/reject verdict.

Accuracy of implementation claims against the actual diff belongs to the Plan fidelity family, not this category.

**Related rubric checks:** `template-compliance`, `disclosure-accuracy`, `reviewer-context`.