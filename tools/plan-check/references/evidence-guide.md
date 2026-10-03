# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where it lives:** In an eval package, read the candidate plan's stated cause against the Issue and Repro evidence sections. In live mode, read the diagnosis in the draft plan against the issue thread and the student's posted reproduction evidence.

**What good looks like:** The stated cause explains the behavior that the reproduction actually demonstrates and does not contradict or ignore material evidence. If the evidence supports the failure but does not establish the proposed cause, that uncertainty should remain visible rather than being treated as proven.

## Scope

**Where it lives:** In an eval package, read the candidate plan's proposed change, boundaries, and named files or areas against the reproduced issue. In live mode, use the scope, files-to-touch, and out-of-scope statements in the draft plan.

**What good looks like:** The work is bounded to the change needed for the reproduced issue. Unrelated refactors, cleanup, features, or changes outside that purpose are not included.

## Executability

**Where it lives:** In an eval package, read the candidate plan's implementation approach, named files or areas, and description of where the change will occur. In live mode, use the approach and files-to-touch portions of the draft plan.

**What good looks like:** Another developer can identify where to begin and what concrete implementation change to attempt without asking the author for a missing implementation decision. The proposed approach acts on the diagnosed cause rather than merely masking the visible symptom.

## Test plan

**Where it lives:** In an eval package, compare the candidate plan's test instructions and expected results with the steps and observed behavior in Repro evidence. In live mode, compare the draft test plan with the student's posted reproduction steps and output.

**What good looks like:** The test exercises the affected behavior through the relevant code path and states an observable result after the change. That result distinguishes the intended fixed behavior from the reproduced failure.

## Honesty

**Where it lives:** In an eval package, compare the candidate plan's diagnosis, assumptions, risks, unknowns, and certainty with what the Issue and Repro evidence actually establish. In live mode, also read the draft plan's risks, unknowns, and Deviations section when applicable.

**What good looks like:** Established facts are distinguished from assumptions or unknowns. Unresolved details are stated as uncertainty rather than certainty, and any build-time departure from the posted plan is recorded honestly in Deviations.

## Comms

**Where it lives:** In an eval package, read the Candidate plan comment against Thread highlights and Repo facts, especially contribution, communication, and AI-use disclosure requirements. In live mode, read the draft comment against the current issue thread and the repository's applicable contribution documentation.

**What good looks like:** The comment presents the candidate's own plan, stays consistent with the technical plan, responds to applicable maintainer direction, and follows repository-stated contribution or disclosure requirements. It should not claim work or certainty unsupported by the candidate's evidence.