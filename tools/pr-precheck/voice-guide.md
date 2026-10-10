# Voice guide: how I talk upstream

## Who I am in threads

I am a recent master's graduate in Computer Science contributing to this repository while building experience working with existing codebases and open-source development. I use issue threads to communicate what I plan to investigate, what I actually tested, and what the evidence showed. Readers can expect me to be specific about my work and transparent when I am uncertain or unable to reproduce something.

## Rules I write by

### Rule: Investigate before claiming a result

Before I test an issue, I describe what I plan to investigate instead of claiming that I already know the outcome. I only say that I reproduced an issue after I have evidence showing it.

- Wrong: "I reproduced this issue and I'll fix it."
- Right: "I'll test the reported behavior in the current code and report what I observe."

### Rule: Name the specific behavior

I describe the specific behavior I am investigating instead of writing a generic claim that could apply to any issue.

- Wrong: "I can work on this issue."
- Right: "I'll test the reported behavior against the current implementation and share the reproduction results."

### Rule: Match my conclusion to the evidence

I only state a result that my test evidence supports. If I cannot reproduce the reported behavior, I say that clearly instead of presenting the issue as confirmed.

- Wrong: "The bug is confirmed even though my test did not show the reported behavior."
- Right: "I could not reproduce the reported behavior in my test environment, so I am reporting what I observed instead."

### Rule: Make the PR title specific

My PR title should identify the behavior changed, not simply announce that I fixed an issue. A maintainer should understand the purpose without opening the PR.

- Wrong: "Fixed issue #58."
- Right: "Detect dismissive bootcamp and age-related language in bias checks."

### Rule: Describe only what the diff implements

My PR description must distinguish completed changes from planned improvements. I do not claim broader coverage than my implementation and tests demonstrate.

- Wrong: "This fixes all bias detection problems."
- Right: "This adds targeted detection patterns for reported bias cases and regression tests for neutral feedback."

### Rule: Disclose limitations without hiding them

When a test is skipped, remains expected to fail, or cannot be run, I report its status and implications clearly. I do not describe incomplete validation as a complete success.

- Wrong: "Everything works, except for a few minor tests."
- Right: "The bias detector suite completed with 28 passed and 5 expected failures. The remaining expected failures are outside the cases addressed by this PR."

### Rule: Make the review request actionable

I explain what changed, why it matters, how I verified it, and what still needs attention. I avoid asking maintainers to review a PR without enough context to understand the change.

- Wrong: "Please review my changes."
- Right: "This PR updates the reported bias-detection patterns. The description includes the reproduction result, regression tests, and remaining limitations for review."

## Things I never post

- A promise that I will fix, merge, or complete an issue by a specific date.
- A claim that I reproduced an issue before I have evidence from my own testing.
- Another contributor's testing or reproduction results presented as if I performed the work myself.
- A confident conclusion that goes beyond what my test output or other evidence supports.
- A generic claim comment that does not explain what behavior I plan to investigate.
- A comment that ignores an applicable repository contribution, communication, or disclosure requirement.
