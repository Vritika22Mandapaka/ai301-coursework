# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->
## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The candidate plan's stated cause read against the issue context and the behavior demonstrated in the repro-evidence block. | Pass only if the stated cause explains the reproduced behavior without contradicting or ignoring material reproduction evidence. If the evidence does not support the claimed cause strongly enough to make that diagnosis, grade unclear rather than assuming it. | required |
| scope-bounded | The candidate plan's stated change, in-scope and out-of-scope boundaries, and named files or areas, read against the reproduced issue. | Pass only if the proposed work is one bounded change needed to address the reproduced issue and does not include unrelated rewrites, cleanup, features, or changes outside that purpose. | required |
| approach-targets-cause | The candidate plan's proposed approach read against its diagnosis and the repro evidence. | Pass only if the proposed change acts on the diagnosed cause of the reproduced behavior rather than merely hiding, bypassing, or compensating for the visible symptom. | required |
| plan-executable | The candidate plan's named files or areas, implementation approach, and order or location of the proposed work. | Pass only if another developer could identify where to begin and what concrete change to attempt without needing the plan author to supply a missing implementation decision. | required |
| test-plan-observable | The candidate plan's test steps and expected results read against the repro-evidence steps and observed failure. | Pass only if the planned test exercises the affected behavior through the relevant code path and names an observable post-change result that distinguishes the fixed behavior from the reproduced failure. | required |
| uncertainty-honest | The candidate plan's diagnosis, risks, unknowns, assumptions, and any stated certainty read against the available issue and repro evidence. | Pass only if unresolved facts are represented as risks, assumptions, or unknowns rather than being presented as established facts. A plan may still pass when uncertainty exists if that uncertainty does not prevent starting the bounded change. | required |
| comment-conventions | The candidate plan comment read against the issue and thread highlights plus the repo-facts block's contribution, communication, and disclosure requirements. | Pass only if the comment describes the candidate's own plan, remains consistent with the plan and thread, responds to applicable maintainer direction, and satisfies every applicable repository-stated contribution or disclosure requirement. If the repo explicitly requires AI-use disclosure, the comment must contain the required disclosure details, such as the tool and extent of assistance when those are required; silence does not satisfy an explicit disclosure requirement. | required |

## Verdict rule

Accept only if every required check passes. Any required check graded fail or unclear makes the verdict reject. Preferred checks, if any are added later, do not change the verdict.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
