# Rubric: is this pull request ready to submit?


## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| issue-coverage | Issue requirements compared with the plan and actual branch diff | The diff addresses the issue's stated objective without contradicting an explicit acceptance requirement. A disclosed limitation does not fail this check unless it defeats the issue's core objective. | required |
| plan-fidelity | Plan scope and deviations compared with the diff's changed files and behavior | Every material implementation change is within the planned scope or is accurately recorded as a deviation. No material change is silently added or omitted. | required |
| description-accuracy | PR title and description compared with the plan, deviations, and actual diff | The description accurately represents the implemented behavior, including material limitations, and makes no claim contradicted by the diff. | required |
| test-observability | Test evidence compared with the plan's test cases and the changed behavior | The package provides observable evidence of relevant verification, such as actual commands and results, reproducible output, or recorded failures. Unsupported claims of testing do not pass. | required |
| repository-checks | Repository-defined validation commands compared with the test evidence and PR disclosure | Required repository checks have credible results, or any checks not run or failing are accurately disclosed with their implications. A disclosed shortfall is not automatically a failure unless repository policy explicitly makes the check mandatory for submission. | required |
| diff-focus | Changed files and hunks in the branch diff compared with the issue and plan scope | The diff is sufficiently focused to review the intended change without unrelated implementation work obscuring it. | required |
| artifact-hygiene | Diff file list and changed content, including generated files and temporary artifacts | No accidental debris, credentials, machine-specific files, or unrelated generated output is included. | required |
| template-compliance | PR description compared with the repository's PR template and repo-facts standards | All applicable mandatory template requests are substantively answered, including required disclosures. Honest N/A responses are acceptable where relevant. | required |
| disclosure-accuracy | PR description, repository disclosure rules, and supplied development evidence | Required AI-assistance, testing, and deviation disclosures are truthful and do not conceal material information. | required |
| reviewer-context | PR description compared with the issue, diff, and test evidence | The description gives a reviewer a useful explanation of what changed, why, and what was verified, without requiring unnecessary reconstruction. | preferred |

## Verdict rule

Assign each check exactly one grade: `pass`, `fail`, or `unclear`, based on the evidence and pass condition specified in the checks table.

Return **`accept`** only when every `required` check receives `pass`.

Return **`reject`** when at least one `required` check receives `fail` or `unclear`. Treat `unclear` as blocking for required checks because the available evidence does not establish that the requirement is satisfied.

A `preferred` check may receive `pass`, `fail`, or `unclear`, but its grade must never change the final verdict. Report preferred-check weaknesses as nonblocking improvements.

Evaluate honest disclosures according to the specific check's pass condition. A disclosed limitation, incomplete optional work item, unrun check, or known test failure is not automatically grounds for rejection. Reject only when the evidence establishes a violation of a required pass condition or when a required condition cannot be verified.

Do not average grades, calculate a numerical score, or introduce conditional acceptance. The verdict space is strictly binary: `accept` means the PR is ready to submit; `reject` means the PR should be held for correction.

For every `fail` or `unclear`, identify the check name, the deciding evidence or missing information, and the correction or clarification needed. Apply the same verdict rule in live and eval modes.
