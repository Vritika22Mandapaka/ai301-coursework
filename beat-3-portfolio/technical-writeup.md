
# Before the First Line of Code: What My First Open-Source Contribution Taught Me

## Overview

The most important part of my first merged open-source contribution was not a line of Python. It was a question I asked the maintainer.

I selected [EcoTrace Issue #211](https://github.com/Zwony/ecotrace/issues/211), which requested a runnable FastAPI example demonstrating estimated carbon emissions and request duration. The task appeared straightforward until I discovered that the middleware named in the issue did not match the implementation in the repository.

I documented the discrepancy and asked the maintainer for clarification. After receiving guidance, I created a 49-line example using the existing middleware, tested both endpoints, and ran the project's test suite.

My contribution was merged as [EcoTrace PR #228](https://github.com/Zwony/ecotrace/pull/228) on October 29, 2026.

The experience changed how I approach engineering work: inspect the existing system, clarify uncertainty, and support implementation decisions with evidence.

## What happened

### Finding a contribution worth making

During CodePath AI301 Unit 5, I developed Issue Scout to evaluate open-source issues based on scope, feasibility, maintainer activity, and available evidence.

An early candidate, codex-lb Issue #1572, involved encryption-key configuration for stateless replicas. The work was interesting, but unresolved security and configuration questions made it difficult to define a safe implementation.

That experience led me to distinguish an issue's actionability from its technical difficulty. EcoTrace #211 offered a more focused contribution: a standalone example that I could implement and verify without changing the library's core behavior.

### Discovering the mismatch

EcoTrace's issue description referenced a middleware class and response header that differed from the repository's existing implementation.

| Component | Issue description | Repository implementation |
| --- | --- | --- |
| Middleware | `StarletteEmissionsMiddleware` | `EcoTraceMiddleware` |
| Import path | `ecotrace.middleware.starlette` | `ecotrace.middleware.fastapi` |
| Carbon header | `X-Carbon-gCO2eq` | `X-Eco-Carbon-Emitted` |
| Duration header | Not specified | `X-Eco-Duration` |

I initially repeated the issue's middleware name before checking the source. Once I identified the discrepancy, I asked the maintainer which interface the example should use.

The maintainer responded with "Great catch" and confirmed that I should demonstrate the existing FastAPI middleware.

Evidence: [Maintainer clarification on Issue #211](https://github.com/Zwony/ecotrace/issues/211#issuecomment-6507532319).

That response changed my implementation plan. Rather than creating or referencing a nonexistent interface, I could build directly on the integration already maintained by the project.

### Building the example

I added `examples/fastapi_tracking.py` and registered the existing middleware:

    app.add_middleware(EcoTraceMiddleware)

The application included two endpoints:

- `GET /health` returned a lightweight status response.
- `GET /compute` performed a calculation to demonstrate tracking during a more active request.

I documented installation, startup, example requests, and the expected response headers. The change consisted of one new file with 49 additions and no modifications to EcoTrace's core package.

Evidence: [Implementation commit](https://github.com/Zwony/ecotrace/commit/0d6d842788588f8133fbe354866993355a679434).

### Fixing a startup problem

My first Uvicorn command failed when executed from the repository root:

    uvicorn fastapi_tracking:app --reload

The problem was the module path, not the middleware. From the repository root, the correct command was:

    uvicorn examples.fastapi_tracking:app --reload

The shorter command worked when executed inside `examples/`.

I corrected the documentation because a runnable example is only useful when another developer can reproduce it from the stated working directory.

### Testing the implementation

I used `curl.exe` to verify that both endpoints returned successful responses and included the expected tracking headers.

Evidence - `/health`:

    HTTP/1.1 200 OK
    x-eco-carbon-emitted: 0.00003795g
    x-eco-duration: 0.0529s
    {"status":"ok"}

Evidence - `/compute`:

    HTTP/1.1 200 OK
    x-eco-carbon-emitted: 0.00003753g
    x-eco-duration: 0.0522s
    {"status":"completed","result":333332833333500000}

I also ran the repository's existing automated tests:

    239 passed, 2 skipped in 58.90s

The HTTP checks demonstrated the example's observable behavior, while the automated suite provided broader regression evidence. Neither test established that the emissions estimates were scientifically accurate.

### The contribution was merged

All 11 GitHub checks passed. The maintainer praised the endpoints, documentation, and middleware integration before merging [PR #228](https://github.com/Zwony/ecotrace/pull/228) on October 29, 2026.

The result was a small, focused contribution that other developers could use to understand EcoTrace's existing FastAPI integration.

### How the experience improved my tools

My contribution also influenced the AI-assisted workflows I developed during CodePath AI301.

#### Issue Scout - Unit 5

I revised the rubric from `scope-fits` to `scope-feasible` and introduced informational difficulty classifications: straightforward, moderate, and ambitious.

This helped me avoid treating complex but actionable issues as automatically unsuitable.

#### Voice Guard - Unit 6

I discovered that my command hook recognized Bash but not PowerShell. I expanded the accepted tool names:

    - if payload.get("tool_name") != "Bash":
    + if payload.get("tool_name") not in ("Bash", "PowerShell"):

The guard log also recorded blocked GitHub commands whose message bodies could not be inspected:

    2026-11-01 04:05 [hook] stop:
    no body the guard can read
    (interactive and --help forms are stopped on purpose)
    target: gh pr create --help

This demonstrated blocking behavior, although the log did not identify which shell originated that event.

#### Ship Gate - Unit 7

On November 1, I ran a retrospective contribution-readiness check against my EcoTrace work.

The gate initially blocked the review because of a Windows test-command problem, missing review evidence, and documentation issues.

The recorded verdict sequence in `gate-log.md` was:

    2026-11-01 04:20 [manual]
    - verdict: BLOCK

    2026-11-01 04:23 [manual]
    - verdict: BLOCK

    2026-11-01 04:29 [manual]
    - verdict: BLOCK

    2026-11-01 04:41 [manual]
    - verdict: PASS

The final retrospective check recorded all nine required checks passing, along with the preferred reviewer-context check. The supporting evidence included the 239 passing tests and two skips.

The review also identified a missing final newline. I disclosed that finding rather than claiming the committed file had been corrected.

Importantly, Ship Gate ran after the PR was merged. Its PASS was not a pre-merge approval.

#### PR Monitor - Unit 8

On November 3, PR Monitor detected that PR #228 had merged and suggested a conditional follow-up concerning Issue #211.

I checked GitHub and confirmed that the issue was already closed and that I had already thanked the maintainer.

I did not send another message. The experience reinforced that automated recommendations still require human verification.

## Limitations and what's next

Although the FastAPI example worked during manual testing, I did not add dedicated automated tests for the endpoint response bodies and `X-Eco-*` headers.

SonarQube reported 0.0% new-code coverage, while Codecov reported coverage of modified lines. Endpoint-specific tests would provide stronger evidence regardless of those different reports.

The emitted values showed that the middleware returned measurements, not that those measurements were accurate or that the example reduced carbon emissions. Validating those claims would require repeatable benchmarks and an appropriate measurement methodology.

My next assigned contribution is [EcoTrace Issue #213](https://github.com/Zwony/ecotrace/issues/213), involving Flask and Blueprint emissions-tracking examples.

I plan to inspect the existing integration first, confirm the intended interface, document reproducible commands, and propose focused endpoint tests within the agreed scope.

I also completed [Rafter PR #318](https://github.com/Raftersecurity/rafter-cli/pull/318), improving Windsurf integration documentation. That contribution reinforced the value of clear setup, verification, troubleshooting, and removal instructions.

My biggest lesson is that a successful contribution requires more than working code. It requires understanding the problem, checking assumptions, communicating clearly, and providing evidence that others can inspect.

The 49 lines mattered because they worked. The question I asked beforehand mattered because it helped me build the right thing.
