# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The repro report's environment record, read against the issue context and repo-facts block as mapped in `references/evidence-guide.md` under Environment | Pass if the report identifies the relevant runtime, dependency or package versions, operating system or platform, and other setup details needed to interpret the reproduction, and those details either match the issue's target environment or explicitly state any meaningful difference. | required |
| steps-followable | The reproduction steps in the repro report, read against the issue context and the Steps section of `references/evidence-guide.md` | Pass if a stranger can follow the stated actions from the described starting state to the relevant trigger without having to guess a necessary command, input, configuration, or action, and the steps exercise the scenario described by the issue rather than an unrelated scenario. | required |
| behavior-matches | The repro report's artifacts, including command output, test output, logs, error messages, or screenshots, read against the behavior described in the issue context and the Behavior shown section of `references/evidence-guide.md` | Pass if the artifacts provide observable evidence about the specific behavior described by the issue: either they show that behavior occurring, or they show that it did not occur during a documented cannot-reproduce attempt. Evidence only of a different error, failure, or adjacent behavior does not pass this check. | required |
| outcome-honest | The outcome and conclusions stated in the repro report, compared with the report's artifacts and the issue context as mapped in `references/evidence-guide.md` under Honesty | Pass if the stated outcome is supported by the evidence and does not claim more than the artifacts demonstrate. A supported reproduced result or a supported cannot-reproduce result passes; uncertainty, environment differences, or incomplete results must be stated rather than presented as confirmed reproduction. | required |
| repo-conventions | The claim comment and repro report, read against the repository contribution or comment conventions and any AI-use disclosure requirements provided in the issue context or repo-facts block, as mapped in `references/evidence-guide.md` under Comms | Pass only if all applicable repository-stated communication, contribution, and AI-use disclosure requirements are satisfied. If the repository requires AI-use disclosure for issues or comments, the candidate claim/repro communication must contain the required disclosure, including any required tool and extent-of-use information; if that required disclosure is absent, fail this check. If the repository explicitly states that issue comments do not require AI disclosure, absence of disclosure does not fail this check. The claim must also identify the specific issue and next investigation or reproduction action without promising a fix or completion date, and the repro communication must report the student's own result rather than relying on another contributor's reproduction. | required |

## Verdict rule

Accept only if every required check passes. Any required check graded fail or unclear makes the package reject. Preferred checks, if any are added later, may inform feedback but never change the accept or reject verdict.
