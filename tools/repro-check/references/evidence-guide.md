# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

- **Where it lives:** In an eval package, look at the issue context and repo-facts block for the environment the issue targets, then compare those details with the environment recorded in the repro report. In live mode, use the GitHub issue and repository setup or contribution documentation to identify the expected environment, and use the student's repro report for the environment actually tested.

- **What good looks like:** The repro report records the relevant runtime, dependency or package versions, operating system or platform, and other setup details needed to understand the test. These details should match the environment targeted by the issue, or any meaningful difference should be stated explicitly.

## Steps

- **Where it lives:** In an eval package, look at the reproduction steps in the repro report and use the issue context and repo-facts block to understand the expected starting state and trigger. In live mode, compare the student's repro report with the GitHub issue and the repository's setup or testing documentation.

- **What good looks like:** The steps give a stranger enough information to move from the stated starting state to the behavior being tested without guessing a missing command, input, configuration, or action. The steps should reproduce the issue's relevant trigger rather than a different or merely similar scenario.

## Behavior shown

- **Where it lives:** In an eval package, look at the repro report's artifacts such as command output, test output, logs, error messages, or screenshots, and read them against the behavior described in the issue context. In live mode, compare the evidence included in the student's repro report with the behavior described in the GitHub issue.

- **What good looks like:** The artifacts provide observable evidence of the specific behavior the issue describes, or observable evidence that the behavior did not occur during an honest cannot-reproduce attempt. Evidence of a different error, failure, or adjacent behavior does not establish reproduction of the issue.

## Honesty

- **Where it lives:** In an eval package, compare the outcome and conclusions stated in the repro report with its artifacts, command or test output, and the behavior described in the issue context. In live mode, compare the student's stated result in the draft repro comment with the evidence they collected while testing the issue.

- **What good looks like:** The stated outcome does not claim more than the evidence demonstrates. A report may honestly say the issue was reproduced or could not be reproduced when its evidence supports that conclusion; uncertainty, environment differences, or incomplete results should be stated rather than presented as confirmed reproduction.

## Comms

- **Where it lives:** In an eval package, look at the claim comment and repro report alongside the issue context, repo-facts block, and any repository contribution or comment conventions included in the package. In live mode, compare the student's draft comment with the GitHub issue and the repository's contribution documentation, issue templates, and any stated AI-use disclosure requirements.

- **What good looks like:** The claim identifies the specific issue and states the next investigation or reproduction action without promising a fix or completion date. The repro communication reports the student's own result specifically and honestly, follows any repository-required comment or disclosure conventions, and does not substitute another contributor's reproduction for the student's own work.
