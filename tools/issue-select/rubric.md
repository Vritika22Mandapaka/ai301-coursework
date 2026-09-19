# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | The last 5 default-branch commit dates and authors in the repo-facts block | Pass if at least 2 human commits occurred within the last 90 days | required |
| repo-in-use | Latest release, last push date, and last 5 default-branch commits in the repo-facts block | Pass if either the repository published a release within the last 12 months OR the repository has at least 2 default-branch commits within the last 90 days | required |
| scope-fits | Issue title, issue body, and issue labels | Pass if the issue identifies a specific bug, feature, documentation change, or other concrete outcome to work toward; a short description or technically substantial task does not fail by itself when the requested outcome is identifiable | required |
| unclaimed | Issue assignees, linked pull requests, and the full captured comment thread | Pass only if all three are true: (1) there is no current assignee, (2) there is no open linked pull request implementing the issue, and (3) every contributor claim in the captured comment thread has later evidence explicitly rejecting or ending that claim. A successful claim is indicated by a contributor claim command such as `@zulipbot claim` or an equivalent explicit statement of intent to work on the issue. If the final/latest claim in the captured thread has no later rejection, cancellation, release, or unassignment, grade this check FAIL even when the repo-facts block says `assignees: none`. | required |
| maintainer-responsive | Maintainer first-response sample in the repo-facts block | Pass if at least one sampled issue received an owner/member/collaborator response within 30 days | preferred |

## Verdict rule

Accept only if every required check passes. Preferred checks never change
the accept or reject verdict and are used only to rank accepted issues.
Any required check graded unclear counts as fail.