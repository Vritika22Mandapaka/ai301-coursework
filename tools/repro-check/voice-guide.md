# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

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

## Things I never post

- A promise that I will fix, merge, or complete an issue by a specific date.
- A claim that I reproduced an issue before I have evidence from my own testing.
- Another contributor's testing or reproduction results presented as if I performed the work myself.
- A confident conclusion that goes beyond what my test output or other evidence supports.
- A generic claim comment that does not explain what behavior I plan to investigate.
- A comment that ignores an applicable repository contribution, communication, or disclosure requirement.
