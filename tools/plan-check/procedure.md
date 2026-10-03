# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the Issue section first. Record the reported behavior, expected behavior, and the specific problem the issue asks to address.
2. Read Repo facts and Thread highlights next. Record any maintainer direction and any contribution, communication, or disclosure requirements that apply to the candidate.
3. Read Repro evidence before reading the candidate plan. Record the reproduction steps, observed failure, expected behavior, and what the evidence establishes or leaves uncertain. Do not infer a cause that the reproduction does not establish.
4. Read the Candidate plan. Record its diagnosis, proposed change, scope boundaries, named files or areas, implementation approach, test plan, risks, assumptions, and unknowns.
5. Read the Candidate plan comment last. Record what it claims about the work and compare it with the plan, thread, repo facts, and reproduction evidence.
6. In live mode, use the same order with the current issue thread, repository contribution documentation, the student's posted reproduction evidence, draft plan, and draft comment.

## Evidence gathering

1. For `diagnosis-grounded`, pair the plan's stated cause with the specific behavior and observations recorded from the repro evidence. Record any contradiction or unsupported causal leap.
2. For `scope-bounded`, record the proposed change, in-scope and out-of-scope boundaries, and named files or areas. Compare each proposed part with the reproduced issue and flag unrelated work.
3. For `approach-targets-cause`, pair the implementation approach with the stated diagnosis. Record whether the proposed change acts on that cause or only masks the visible symptom.
4. For `plan-executable`, record the implementation location and concrete change another developer is expected to make. Note any missing decision that would prevent a developer from knowing where or how to begin.
5. For `test-plan-observable`, pair each relevant planned test with the reproduced failure. Record the code path or behavior exercised and the expected post-change observation that would distinguish success from the original failure.
6. For `uncertainty-honest`, record claims of certainty alongside the evidence supporting them. Also record explicit risks, assumptions, and unknowns.
7. For `comment-conventions`, record applicable maintainer direction and repository-stated contribution, communication, or disclosure requirements, then compare them with the candidate plan comment.
8. Use the evidence guide for the exact eval-package and live-mode locations for each evidence family. Do not substitute evidence from another candidate or from outside the supplied snapshot during eval mode.

## Check execution

1. Grade the checks in this order: `diagnosis-grounded`, `scope-bounded`, `approach-targets-cause`, `plan-executable`, `test-plan-observable`, `uncertainty-honest`, and `comment-conventions`.
2. Apply only the pass condition written for the current rubric check to the evidence gathered for that check. Do not fail one check solely because a different check failed.
3. Grade `pass` when the gathered evidence satisfies the check's pass condition.
4. Grade `fail` when the gathered evidence shows that the pass condition is violated.
5. Grade `unclear` when evidence required to decide the check is genuinely missing or insufficient. Do not invent missing repository facts, causal evidence, implementation details, test results, or maintainer instructions.
6. Once the necessary evidence has been recorded, grade the check from those recorded facts without re-reading the entire package unless two recorded facts conflict or required context was missed.
7. Continue grading every check even after one required check fails so the final output identifies all material reasons the plan is not ready.

## Verdict assembly

1. Collect the grade for every rubric check after all checks have been executed.
2. Apply the rubric verdict rule exactly: accept only when every required check passes.
3. Treat `unclear` on a required check as holding the plan, so the final verdict is reject.
4. A failed preferred check, if preferred checks are added later, does not change the verdict.
5. For an accept verdict, state that all required checks passed and briefly identify the evidence supporting readiness.
6. For a reject verdict, identify the required check or checks that failed or were unclear. Quote or closely point to the smallest relevant piece of package evidence for the deciding check so the reason for holding the plan is traceable.
7. Do not change the verdict because the plan is well written, detailed, or plausible if a required outcome-based check fails.