# Procedure: how this tool grades a PR package

## Read order

1. **Determine the review mode.** Identify whether the request is a live PR review or an evaluation bundle. In live mode, read `scope.md` first and refuse an unauthorized or unconfigured repository. In eval mode, use only the supplied bundle and ignore `scope.md` and `voice-guide.md`.

2. **Load the grading instructions.** Read `rubric.md` to identify the exact checks and verdict rule. Read `references/evidence-guide.md` to locate the evidence families. Follow this procedure in order. If `rubric.md` or `procedure.md` is empty or unusable, refuse to grade.

3. **Read the issue context.** Identify the requested behavior, explicit acceptance criteria, constraints, and any issue discussion that changes the expected outcome. Record the core objective separately from optional improvements.

4. **Read the implementation plan before the diff.** Record the planned scope, named files or components, proposed behavior, exclusions, test plan, known risks, and documented deviations. Establish this baseline before examining what was actually changed.

5. **Read the actual diff.** In live mode, run `git diff main...HEAD`. In eval mode, read the supplied diff artifact. Record changed files, material hunks, implemented behavior, additions outside the plan, and any planned work absent from the implementation.

6. **Read the test evidence.** Record test commands, observed results, reproduced behavior, failed or skipped checks, and any limitations. Compare these observations with the plan's proposed tests and the repository's validation requirements.

7. **Read the PR title and description.** Extract the claimed changes, testing statements, limitations, deviations, and disclosures. Compare these claims with the previously recorded plan, diff, and test evidence rather than accepting the description as proof.

8. **Read repository standards.** In live mode, inspect the applicable PR template and `docs/CONTRIBUTING.md`. In eval mode, use the standards or repo-facts included in the bundle. Record mandatory submission requirements separately from recommendations.

9. **Apply the live-mode voice guide.** After confirming repository scope, use `voice-guide.md` to review the outgoing PR title and description. Report violations separately; do not let voice feedback independently determine the verdict.

Do not assign check grades until the applicable artifacts have been read and the evidence comparisons have been recorded. Preserve the distinction between a missing artifact, an unsupported claim, and an explicitly disclosed limitation.

## Evidence gathering

Gather evidence using the four families defined in `references/evidence-guide.md`. For every observation, record the source artifact, the specific fact or quotation, and the rubric check it supports. In eval mode, use only bundle artifacts.

**1. Plan fidelity — silent drift**

- For `issue-coverage`, extract the issue's core objective and explicit acceptance criteria. Compare them with the implemented behavior visible in the diff. Record any unmet mandatory requirement separately from disclosed optional limitations.
- For `plan-fidelity`, create a comparison of planned files, behaviors, exclusions, and deviations against the actual changed files and hunks. Record material additions, omissions, and changes that lack a documented deviation.
- For `description-accuracy`, compare each material claim in the PR title and description with the plan, deviation notes, and diff. Record unsupported or contradicted claims using the exact wording.

**2. Test evidence — not tested**

- For `test-observability`, compare the plan's test cases with the supplied test evidence. Record actual commands, outputs, results, reproductions, failures, and skipped tests. Distinguish observable verification from statements that tests were planned or passed without proof.
- For `repository-checks`, identify the repository's expected validation commands from its standards or repo-facts. Match each applicable command with its recorded result or explicit disclosure that it was not run. Record whether repository policy makes successful execution mandatory for submission.

**3. Diff quality — unreviewable**

- For `diff-focus`, inspect the diff's changed-file list and individual hunks. Compare them with the issue objective and planned scope. Record unrelated modifications that obscure the intended implementation.
- For `artifact-hygiene`, inspect added files and changed content for accidental generated output, temporary files, machine-specific artifacts, credentials, or unrelated debris. Record exact file paths and relevant hunks when present.

**4. Standards and communication — standards wall**

- For `template-compliance`, extract mandatory fields and questions from the repository PR template or supplied repo-facts. Compare them with the PR description and record missing substantive answers.
- For `disclosure-accuracy`, identify mandatory disclosure rules and compare the PR's AI-assistance, testing, and deviation statements with the supplied evidence. Record omissions, contradictions, or accurately disclosed limitations.
- For `reviewer-context`, compare the PR description with the issue, diff, and tests. Record whether a reviewer can identify the purpose, material changes, and verification without reconstructing the entire package.

For each check, retain a concise evidence note sufficient to justify `pass`, `fail`, or `unclear`. Do not treat a missing artifact as proof of failure when the applicable requirement cannot be established; record the uncertainty and apply the rubric's `unclear` rule. Do not retrieve external evidence in eval mode.

## Check execution

1. **Follow rubric order.** Execute every check in the exact order listed in `rubric.md`: `issue-coverage`, `plan-fidelity`, `description-accuracy`, `test-observability`, `repository-checks`, `diff-focus`, `artifact-hygiene`, `template-compliance`, `disclosure-accuracy`, and `reviewer-context`. Do not skip a check because another check has already failed.

2. **Evaluate one responsibility at a time.** For each check, retrieve its recorded evidence from the Evidence gathering stage. Compare that evidence only with the check's stated pass condition. Do not merge checks, introduce new requirements, or allow a preferred check to override a required check.

3. **Assign `pass` when supported.** Grade `pass` when the available evidence affirmatively satisfies the check's pass condition. Record the decisive supporting fact, including the relevant file, diff hunk, test result, or PR statement.

4. **Assign `fail` when contradicted.** Grade `fail` when the evidence demonstrates that the pass condition is violated. Identify the exact contradiction, omitted mandatory requirement, unrelated change, unsupported claim, or other observed defect.

5. **Assign `unclear` when unverifiable.** Grade `unclear` when the evidence needed to decide the check is missing, ambiguous, or insufficient. Identify the missing evidence. Do not invent results, assume success, or treat an unsupported claim as verified.

6. **Respect honest disclosures.** When a limitation, failed test, or unrun validation command is explicitly disclosed, apply the individual check's pass condition and the repository's mandatory requirements. Do not automatically fail the package solely because a limitation exists.

7. **Use recorded evidence efficiently.** Grade from the evidence notes without rereading the entire package when those notes contain the relevant facts and their sources. Reopen a specific artifact only when a necessary detail is missing or conflicting; in eval mode, never consult material outside the bundle.

8. **Record every result.** For each check, save its exact rubric name, weight, grade, and one concise evidence line. Keep the results in rubric order for final JSON assembly.

After all checks have been evaluated, pass the complete results to the Verdict assembly stage. Do not issue an early verdict or omit nonblocking findings.

## Verdict assembly

1. **Collect the completed grades.** Confirm that every check listed in `rubric.md` has exactly one result containing its exact name, weight, grade (`pass`, `fail`, or `unclear`), and a concise evidence statement. Preserve the original rubric order.

2. **Apply the verdict rule.** Return `accept` only if every `required` check is graded `pass`. Return `reject` if any `required` check is graded `fail` or `unclear`. Preferred checks are advisory and never change the verdict.

3. **Treat uncertainty consistently.** An `unclear` grade on a required check blocks submission because the available evidence does not establish that its pass condition is satisfied. An `unclear` grade on a preferred check is nonblocking.

4. **Select the deciding check.** If the verdict is `reject`, identify the first required check graded `fail` or `unclear` in rubric order as the primary blocking reason. Quote or identify the exact evidence, contradiction, or missing artifact that determined that grade. If multiple required checks are blocking, report the others as additional failures without changing the primary selection rule.

5. **Explain an acceptance.** If the verdict is `accept`, identify the strongest observable evidence supporting readiness, such as alignment between the issue, plan, diff, and test results. Mention any nonblocking preferred-check weaknesses or honestly disclosed limitations without treating them as failures.

6. **Provide actionable feedback.** Summarize the verdict and identify what must be corrected before submission when rejected. Separate required corrections from optional improvements. In live mode, report voice-guide violations separately; they must not independently affect the verdict.

7. **Assemble the final JSON.** Use the exact schema specified in `SKILL.md`. Set `item` to the PR URL or evaluation bundle ID. Include every check in rubric order, using only `name`, `grade`, and `evidence` for each check entry. Set `verdict` to exactly `accept` or `reject`. Do not add fields or alter the schema.

8. **Validate the response.** Confirm that the JSON is syntactically valid, the verdict matches the required-check grades, and each evidence line supports its assigned grade. End the response with the fenced JSON block and place nothing after its closing fence.

If the review must be refused because the live repository is out of scope or a mandatory grading component is unusable, explain the refusal without manufacturing check grades or an accept/reject verdict.
