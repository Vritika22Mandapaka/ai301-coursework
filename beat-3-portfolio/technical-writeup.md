# Before the First Line of Code: What My First Open-Source Contributions Taught Me

## Overview

The most important line in my first merged open-source contribution wasn't a line of Python. It was a question I asked the maintainer.

When I found [EcoTrace Issue #211](https://github.com/Zwony/ecotrace/issues/211), I thought my challenge was to write a FastAPI example demonstrating how developers could measure the carbon emissions and execution duration of HTTP requests. It was a focused task in an unfamiliar codebase, and I was excited to contribute something other developers could actually run.

But before writing the example, I discovered something unexpected: **the issue described an interface that didn't exist in the repository as written.**

I had initially repeated the middleware name from the issue in my communication with the maintainer. Only after inspecting the source did I realize the instructions and implementation disagreed. Rather than continuing with an assumption, I asked which interface was correct.

That question shaped the contribution. I built a 49-line FastAPI example using EcoTrace's existing middleware, verified its behavior through actual HTTP responses, and ran the project's tests. The result was [PR #228](https://github.com/Zwony/ecotrace/pull/228), merged on October 29, 2026.

What began as a small implementation task became a lesson in engineering judgment: understanding existing code, asking useful questions, and treating evidence—not confidence—as the basis for decisions.

## What happened

### Finding a contribution worth making

In Unit 5, I built **Issue Scout** to evaluate open-source opportunities based on scope, maintainer activity, feasibility, and available evidence.

One opportunity, codex-lb Issue #1572, involved encryption-key configuration for stateless replicas. I was interested in it, but unresolved questions about security and configuration behavior made me hesitant to implement anything without clarification. That experience pushed me to refine Issue Scout:** I needed to distinguish technical difficulty from uncertainty about what a safe, acceptable solution would be.

EcoTrace Issue #211 was different. It requested a self-contained example with a clear user-facing outcome. I could inspect the integration, run the application, and check whether the expected tracking information appeared.

### Discovering the problem before implementing it

The issue requested `StarletteEmissionsMiddleware` from `ecotrace.middleware.starlette` and described an `X-Carbon-gCO2eq` header.

But the source code in `ecotrace/middleware/fastapi.py` showed a different interface:

|                 | Issue description               | Repository implementation     |
| --------------- | ------------------------------- | ----------------------------- |
| Middleware      | `StarletteEmissionsMiddleware`  | `EcoTraceMiddleware`          |
| Import path     | `ecotrace.middleware.starlette` | `ecotrace.middleware.fastapi` |
| Carbon header   | `X-Carbon-gCO2eq`               | `X-Eco-Carbon-Emitted`        |
| Duration header | Not specified                   | `X-Eco-Duration`              |

I had already repeated the issue's proposed middleware name before verifying it. That was my mistake. I corrected course by documenting the discrepancy and asking the maintainer rather than silently inventing an interface. The maintainer acknowledged the finding with “Great catch” and confirmed that the example should use the existing FastAPI integration ([discussion](https://github.com/Zwony/ecotrace/issues/211#issuecomment-6507532319)).

The maintainer confirmed that the example should use the existing FastAPI middleware ([Issue #211 clarification](https://github.com/Zwony/ecotrace/issues/211#issuecomment-6507532319)).

That response resolved the ambiguity and changed my implementation plan. I no longer needed to build around the issue's outdated names; I needed to demonstrate the code that actually existed.

### Getting the example to run

I added `examples/fastapi_tracking.py`, registering the existing middleware:

```python
app.add_middleware(EcoTraceMiddleware)
```

The example provided `/health`, returning a basic status, and `/compute`, performing a calculation to demonstrate tracking during a more active request.

I included dependency installation, startup instructions, example requests, and expected tracking headers. The change remained one new file with 49 additions and no modifications to the core package.

**Evidence:** [Implementation commit](https://github.com/Zwony/ecotrace/commit/0d6d842788588f8133fbe354866993355a679434).

### A small debugging problem with a useful lesson

After writing the example, I encountered an import error while starting the application with Uvicorn.

Initially, I used the short module name from the repository root, but Python couldn't locate the example in that context. This wasn't a major code defect, but it changed how I thought about documentation.

An example is only useful if another developer can follow its instructions and reproduce the result.

My first Uvicorn launch failed because I ran the short module name from the repository root:

```bash
uvicorn fastapi_tracking:app --reload
```

Python couldn't resolve the example from that directory. The correct root-level command was:

```bash
uvicorn examples.fastapi_tracking:app --reload
```

The shorter command worked from inside `examples/`. This was a small debugging problem, but it taught me that documentation must account for the environment in which someone will follow it.

### Proving the middleware was working

I tested both endpoints with `curl.exe`. I specifically checked the tracking headers because a `200 OK` response alone wouldn't demonstrate the purpose of the contribution.

**Evidence — `/health`:**

```text
HTTP/1.1 200 OK
x-eco-carbon-emitted: 0.00003795g
x-eco-duration: 0.0529s
{"status":"ok"}
```

**Evidence — `/compute`:**

```text
HTTP/1.1 200 OK
x-eco-carbon-emitted: 0.00003753g
x-eco-duration: 0.0522s
{"status":"completed","result":333332833333500000}
```

Both returned the expected JSON and EcoTrace headers. I also ran the project's automated test suite:

**pytest output**

```text
239 passed, 2 skipped in 58.90s
```

The skips concerned optional LangChain dependencies. I also validated Python syntax and checked the staged changes for whitespace errors. The manual endpoint checks and automated tests served different purposes. The HTTP checks verified the new example's observable behavior, while the existing tests provided broader regression confidence. These checks gave me confidence that the example behaved as intended without breaking the existing tests.

### The merge - the moment the contribution became real

The PR added **49 lines in one file**, without modifying the core package. All **11 GitHub checks passed**. The maintainer's review stated:

- Thank you for the well-structured contribution and clean implementation. The endpoints, docstrings, and middleware integration look great and adhere strictly to the project requirements. Merging now.

[PR #228](https://github.com/Zwony/ecotrace/pull/228) merged on October 29, 2026.

The review mattered because it recognized not just the working endpoints, but the documentation and integration choices that made the example useful.

### What I changed in my tools

The contribution also shaped the AI-assisted workflows I developed across Units 5–8.

**Unit 5 — Issue Scout:** I refined issue scoring to account for ambiguous requirements and realistic feasibility, rather than treating technical difficulty as the only challenge.

**Unit 6 — Voice Guard:** I updated communication and command checks to accommodate Windows PowerShell, after finding that Bash-oriented guidance didn't always fit my environment.

**Unit 7 — Ship Gate:** A retrospective review helped me separate scoped lint checks from full-suite validation and identify a missing newline.

**Unit 8 — PR Monitor:** The tool suggested asking the maintainer to close Issue #211. I checked GitHub, found the issue already closed and the maintainer already thanked, and chose not to post.

That final decision reflected the same lesson as the middleware mismatch: AI tools can suggest the next action, but I remain responsible for verifying whether it is correct or necessary.

## Limitations and what's next

The FastAPI example worked in my manual checks, but I didn't add dedicated automated tests asserting the endpoint responses and `X-Eco-*` headers. SonarQube reported 0.0% new-code coverage, although Codecov reported coverage of modified lines. The missing endpoint-specific tests remain a meaningful limitation regardless of those different reports.

The recorded emissions values confirmed that the middleware returned tracking information; they did not establish measurement accuracy or emissions reduction. I did not measure consistency across repeated runs or compare emissions before and after an optimization. I would need a separate benchmarking approach to make those claims responsibly.

My next assigned contribution is [EcoTrace Issue #213](https://github.com/Zwony/ecotrace/issues/213), a Flask application and Blueprint emissions-tracking example. I plan to inspect the existing Flask integration before coding, clarify any interface ambiguity, document commands that work from the correct directory, and propose automated tests for response bodies and tracking headers within the agreed issue scope.

I also completed a second merged contribution, [Rafter PR #318](https://github.com/Raftersecurity/rafter-cli/pull/318), improving Windsurf integration documentation with setup, verification, troubleshooting, security-tool references, and uninstall instructions. That work reinforced how important clear, reproducible guidance is to a developer's experience.

I began this contribution wanting to get code merged. I finished it with a better standard for what makes a contribution useful.

**The 49 lines mattered because they worked. The question I asked beforehand mattered because it helped me build the right thing.**
