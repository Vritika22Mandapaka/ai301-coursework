# Contribution: Add FastAPI Emissions Tracking Example to EcoTrace
Contribution Number: 1
Student: Kamakshi Padma Vritika Mandapaka
GitHub Username: Vritika22Mandapaka
Issue: https://github.com/Zwony/ecotrace/issues/211
Pull Request: https://github.com/Zwony/ecotrace/pull/228
Contribution Summary: Added a runnable FastAPI example demonstrating EcoTrace's existing emissions-tracking middleware. The implementation includes a lightweight health-check endpoint, a CPU-intensive computation endpoint, installation and execution instructions, and documentation of the emissions and duration response headers. The contribution was reviewed, approved, and merged by the repository owner.

## Toolkit
Unit 5: Built an issue-scout workflow to evaluate open-source contribution opportunities

I created an issue-scout skill using Claude Code to research and evaluate GitHub issues based on project activity, technical feasibility, and alignment with my Python and AI interests. My initial search returned several issues that were already closed, claimed, or too broad for my timeline, so I refined the selection process to verify issue status, existing pull requests, maintainer activity, and implementation scope. After comparing multiple candidates, I selected codex-lb Issue #1572 because it involves Python backend development, encryption-key management, and deployment reliability. I also contacted the maintainer with my proposed implementation approach and questions about the project's configuration constraints.

Unit 6: Strengthened my issue-scout workflow, added a voice guard, and created local repository memory

I expanded my Claude Code voice guide with five rules for upstream communication, covering issue claims, maintainer questions, and follow-up messages. I also updated my Issue Scout rubric to evaluate whether an issue has a feasible scope rather than automatically rejecting challenging work, and added difficulty notes to explain the assessment.

While installing the voice guard, I discovered that the starter hook checked only Bash commands, but Claude Code on my Windows setup uses PowerShell. I updated the script to recognize both tools and verified that it blocked a GitHub command without a readable message body. I also encountered Windows symlink restrictions, so I used pointer files to connect my three skills to the shared voice guide.

Finally, I used Claude Code to inspect three relevant EcoTrace files and created a local CLAUDE.local.md documenting contribution conventions, the FastAPI middleware, tests, and repository practices. I added the file to .git/info/exclude and verified that Git ignores it, keeping my AI-specific working notes out of the upstream repository.

Unit 7: Built and ran a retrospective ship-gate for my EcoTrace contribution.

I created a ship manifest defining the full test suite and scoped lint for the FastAPI example, then ran the ship-gate against my `feat/fastapi-example` branch, issue #211, and PR description. The gate passed all nine required rubric checks and the preferred reviewer-context check. The full test suite passed with 239 tests passed and 2 skipped, and the scoped lint check passed. The process also highlighted the distinction between scoped and repository-wide lint, the importance of the actual PR template, and a missing final newline in the merged file. Because PR #228 was already merged and issue #211 was closed, I did not open a duplicate PR; I documented the exercise as retrospective.

Unit 8: Installed the PR-monitor, created my playbook, and verified my merged EcoTrace contribution

I installed CodePath's PR-monitor and wrote a personal playbook defining my response rules, review waiting periods, follow-up etiquette, and criteria for closing a contribution. I ran the free state check and full monitor against EcoTrace PR #228, which confirmed that the PR was merged with 11 passing checks and generated a run report and a drafted follow-up. The draft suggested thanking the maintainer and checking whether Issue #211 still needed to be closed. I verified through GitHub CLI that the issue was already closed as completed and decided not to post another comment because I had already thanked the maintainer. This taught me to review AI-generated suggestions against current repository evidence rather than automatically sending them.

## Why I Chose This Issue
I began searching for open-source issues that matched my interests in Python, backend development, and AI-related developer tools. During Unit 5, I built an issue-scout workflow using Claude Code to assess issue availability, maintainer activity, technical feasibility, and scope. My initial choice was codex-lb Issue #1572, which proposed supporting environment-based encryption keys for stateless replicas. I reviewed the existing scoping notes, proposed an implementation approach, and asked about configuration precedence and safe handling of secrets. I did not receive a response to my questions, so I continued exploring opportunities rather than implementing the change without clarification.

I subsequently received positive maintainer responses for EcoTrace FastAPI Issue #211, EcoTrace Flask Issue #213, and rafter-cli Issue #33, where I was invited to work on the Windsurf documentation recipe. I chose to prioritize EcoTrace #211 for Assignment 5 because it offered a focused Python and FastAPI task, and its maintainer clarified an inconsistency between the issue description and the existing middleware. I could verify the implementation against the repository, test it locally, and deliver a self-contained example. I kept the other opportunities separate rather than representing them as completed Assignment 5 contributions. This process showed me that the scout's assessment was useful for finding candidates, but repository inspection, clear requirements, and maintainer communication were essential to making a final choice.

Issue Scout assessment (Unit 6 retrospective): EcoTrace #211 passed scope-feasible and was rated straightforward. Its current verdict was reject because my PR #228 was already merged. codex-lb #1572 also passed scope-feasible but was rated ambitious. These were retrospective results, not my original selection verdicts.

Issue: https://github.com/Zwony/ecotrace/issues/211

Claim comment: https://github.com/Zwony/ecotrace/issues/211#issuecomment-6482759771

Claim reflection: My original claim repeated the middleware class named in the issue before I verified it existed. I later inspected the code, identified the mismatch, and obtained the maintainer's approval. In future claims, I will inspect the relevant implementation first and clearly state my initial investigation step.

**Toolkit**
- Tool: Claude Code issue-scout workflow, GitHub issue discussions, and manual repository inspection.
- What it produced: A shortlist of possible contributions and an evaluation of their technical scope, availability, and suitability for my skills. The process eventually led me to EcoTrace Issue #211.
- Difficulties: Some issues were already claimed, too broad, or required clarification. The EcoTrace issue also referenced a middleware class and response header that did not match the existing implementation.
- What changed: I added manual verification of repository code and maintainer communication to my issue-selection process before beginning implementation.

## Understanding the Issue
**Problem Description**

EcoTrace is a Python package that tracks the energy consumption and carbon emissions of software execution. Issue #211 requested a simple, runnable FastAPI reference example to show developers how to integrate emissions tracking into HTTP request handling.

The repository already had middleware functionality, but the issue was that developers needed a self-contained example demonstrating how to configure it, create endpoints, run the application, and inspect the tracking results.

**Expected Behavior**

The example should provide a FastAPI application with two endpoints: a lightweight `/health` endpoint and a more computationally intensive endpoint. Developers should be able to start the application using Uvicorn, send HTTP requests, and observe the emissions-tracking information in the response headers.

The example should also include clear setup instructions and comments, without requiring changes to EcoTrace's core package.

**Current Behavior**

Before my contribution, the requested `examples/fastapi_tracking.py` reference script was missing. The issue description also mentioned `StarletteEmissionsMiddleware` from ecotrace.middleware.starlette and an `X-Carbon-gCO2eq` header, but these did not match the existing implementation I inspected.

The repository instead provided `EcoTraceMiddleware` in `ecotrace.middleware.fastapi`, which used the `X-Eco-Carbon-Emitted` and `X-Eco-Duration` response headers.

I asked the maintainer to clarify this difference. The maintainer confirmed that I should use the existing middleware and its supported headers rather than introducing a new middleware implementation.

**Affected Components**
- `examples/fastapi_tracking.py` - The new reference example requested by the issue.
- `ecotrace/middleware/fastapi.py` - The existing middleware implementation used by the example.
- FastAPI routes and HTTP responses - The integration points where emissions and execution duration can be observed.
  The contribution was limited to the new example file. No changes were made to the core ecotrace/ package.

**Toolkit**
- Tool: GitHub issue discussion, VS Code repository inspection, and PowerShell.
- What it produced: An understanding of the existing middleware implementation, the expected example behavior, and the correct response-header names.
- Difficulties: The middleware class and header specified in the issue description did not match the repository's existing code.
- What changed: I contacted the maintainer for clarification and adjusted the implementation plan to use `EcoTraceMiddleware` from `ecotrace.middleware.fastapi` with its existing response headers.

## Reproduction Process
**Environment Setup**

I worked on Windows using VS Code and PowerShell. I cloned my EcoTrace fork and created a Python virtual environment (`.venv`) to isolate the project's dependencies.

From the repository root, I installed the project with its web dependencies and installed FastAPI, Uvicorn, and pytest.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -e ".[web]"
python -m pip install fastapi uvicorn pytest
```

I used the `feat/fastapi-example` branch for the implementation. The virtual environment was excluded from Git tracking.

Environment versions (retrospective verification): Python 3.13.12; EcoTrace 1.7.1; FastAPI 0.162.0; Starlette 1.10.0; Uvicorn 0.54.0; pytest 9.2.0. These versions were observed during Unit 6 verification and may differ from the original development environment.

**Steps to Reproduce**
1. Before adding the example, I inspected the repository's examples/ directory and confirmed that `fastapi_tracking.py` was missing.
2. I examined the middleware implementation in `ecotrace/middleware/fastapi.py` and compared it with the middleware class and header names specified in Issue #211.
3. I found that the issue referenced `StarletteEmissionsMiddleware` and `X-Carbon-gCO2eq`, while the existing implementation used `EcoTraceMiddleware`, `X-Eco-Carbon-Emitted`, and `X-Eco-Duration`.
4. I asked the maintainer for clarification. The maintainer confirmed that the example should use the existing middleware implementation.
5. After implementing the example, I started the application using:

   ```powershell
   python -m uvicorn examples.fastapi_tracking:app --app-dir "$HOME\OneDrive\Desktop\AI301\ecotrace" --host 127.0.0.1 --port 8000
   ```

6. I tested both endpoints using `curl.exe` and verified the HTTP responses and emissions-tracking headers.
**Reproduction Evidence**
- Implementation commit: https://github.com/Zwony/ecotrace/commit/0d6d842788588f8133fbe354866993355a679434
- Issue discussion: https://github.com/Zwony/ecotrace/issues/211
- Pull request: https://github.com/Zwony/ecotrace/pull/228
- Observed results: The `/health` endpoint returned HTTP 200 and {"status":"ok"}. The `/compute` endpoint returned HTTP 200 and the expected result 333332833333500000. Both responses included `X-Eco-Carbon-Emitted` and `X-Eco-Duration`.
- My findings: The problem was the absence of a runnable FastAPI reference example, not a failure in the existing middleware. I also identified a mismatch between the issue description and the repository implementation. After maintainer clarification, I used the supported middleware and confirmed that both endpoints worked.
**Additional verified evidence (Unit 6 retrospective)**
- Git command: git cat-file -e "0d6d842^:examples/fastapi_tracking.py"
- Terminal output: fatal: path '`examples/fastapi_tracking.py`' exists on disk, but not in '0d6d842^'
- Exit code: 128 (Git could not find the file in the parent commit).
- The original issue referenced `ecotrace.middleware.starlette.StarletteEmissionsMiddleware` and `X-Carbon-gCO2eq`, but the existing implementation used `ecotrace.middleware.fastapi.EcoTraceMiddleware` and `X-Eco-Carbon-Emitted` / `X-Eco-Duration`.
- I reported this mismatch in https://github.com/Zwony/ecotrace/issues/211#issuecomment-6507274270.
- Maintainer Zwony explicitly approved using `EcoTraceMiddleware` and the existing X-Eco-* headers in https://github.com/Zwony/ecotrace/issues/211#issuecomment-6507532319.
- The actual response headers were `X-Eco-Carbon-Emitted` and `X-Eco-Duration`.
- This was a missing-example feature request, not a failing-behavior bug.
**Implementation Verification**
- Commit 0d6d842 added `examples/fastapi_tracking.py` (49 lines, one file changed).
- No core ecotrace/ package files were changed.
- Test command: python -m pytest -q "$HOME\OneDrive\Desktop\AI301\ecotrace\tests" -rs
- Actual output: 239 passed, 2 skipped in 65.46s (0:01:05).
- SKIPPED [1] ecotrace\tests\test_langchain_callback.py:188: could not import 'langchain_core.language_models.fake': No module named 'langchain_core'.
- SKIPPED [1] ecotrace\tests\test_langchain_callback.py:203: could not import 'langchain_core.language_models.fake_chat_models': No module named 'langchain_core'.
- No test failures were reported.
- HTTP verification commands: `curl.exe` -i --max-time 15 http://127.0.0.1:8000/health and `curl.exe` -i --max-time 15 http://127.0.0.1:8000/compute
- `/health` actual output: HTTP/1.1 200 OK; x-eco-carbon-emitted: 0.00003795g; x-eco-duration: 0.0529s; {"status":"ok"}
- `/compute` actual output: HTTP/1.1 200 OK; x-eco-carbon-emitted: 0.00003753g; x-eco-duration: 0.0522s; {"status":"completed","result":333332833333500000}
- Emissions and duration measurements vary between requests.
- PR: https://github.com/Zwony/ecotrace/pull/228 (merged).
**Toolkit**
- Tool: VS Code, PowerShell, Git, Python virtual environment, Uvicorn, and `curl.exe`.
- What it produced: A reproducible local development environment, confirmation of the missing example, and successful HTTP responses containing emissions and duration headers.
- Difficulties: The issue description referenced a middleware class that did not match the code. I also initially encountered a module import error when running Uvicorn with the short module name from the repository root.
- What changed: I used the maintainer-approved middleware and corrected the Uvicorn command to `examples.fastapi_tracking:app` when running from the repository root. I also verified that `uvicorn fastapi_tracking:app --reload` worked from inside the examples/ directory.

## Solution Approach
**Analysis**

After reviewing EcoTrace Issue #211 and inspecting the repository, I determined that the main problem was missing developer-facing documentation in the form of a runnable FastAPI example. The existing middleware implementation was already available in `ecotrace/middleware/fastapi.py`, so there was no need to create another middleware class or change the underlying emissions-tracking logic.

I also discovered that the middleware class and header names in the original issue description did not match the repository. I raised this with the maintainer, who confirmed that the example should use the existing `EcoTraceMiddleware` class and its supported response headers.

**Proposed Solution**

My solution was to create a standalone reference application in `examples/fastapi_tracking.py` using FastAPI and the existing EcoTrace middleware.

The application would expose two endpoints:
- GET `/health` - Returns a JSON health-check response: {"status":"ok"}.
- GET `/compute` - Runs a sample computation and returns the calculated result.
I planned to register `EcoTraceMiddleware` with the FastAPI application so that developers could inspect `X-Eco-Carbon-Emitted` and `X-Eco-Duration` in the HTTP response headers.

I also included installation instructions, Uvicorn commands, endpoint examples, and explanatory comments directly in the file's docstring.

The implementation was intentionally limited to the example file. I did not modify the existing middleware, the emissions calculations, or any other core package functionality.

**Implementation Plan**
1. Inspect `ecotrace/middleware/fastapi.py` and confirm the middleware's import path and supported response headers.
2. Create `examples/fastapi_tracking.py` and initialize a minimal FastAPI application.
3. Register `EcoTraceMiddleware` using `app.add_middleware(EcoTraceMiddleware)`.
4. Implement the `/health` and `/compute` endpoints.
5. Add clear setup, execution, and testing instructions to the module docstring.
6. Verify that the example imports successfully and that both endpoints return HTTP 200 with the expected JSON and tracking headers.
7. Run the repository's existing pytest suite and inspect the staged Git changes before committing.
**Changes to the Original Plan**

The original issue description referenced `StarletteEmissionsMiddleware` and `X-Carbon-gCO2eq`. After inspecting the repository and receiving maintainer clarification, I changed the plan to use `EcoTraceMiddleware`, `X-Eco-Carbon-Emitted`, and `X-Eco-Duration`.

I also corrected the Uvicorn launch command after discovering that `uvicorn fastapi_tracking:app --reload` could not import the example when executed from the repository root. The correct command from the root was `uvicorn examples.fastapi_tracking:app --reload`. The shorter command worked when executed from the examples/ directory.

**Toolkit**
- Tool: VS Code, PowerShell, GitHub issue discussions, Python, and FastAPI documentation.
- What it produced: A focused implementation plan for a runnable FastAPI example using EcoTrace's existing middleware, with two endpoints and documented emissions-tracking headers.
- Difficulties: The issue description contained outdated or mismatched middleware references, and the initial Uvicorn command depended on the working directory.
- What changed: I followed the maintainer-approved middleware interface, documented the correct response headers, and included working Uvicorn commands for both the repository root and the examples/ directory.

## Testing Strategy
I tested the FastAPI example locally to verify that it was runnable, returned the expected responses, and exposed EcoTrace's emissions-tracking headers. I also ran the repository's existing automated tests and checked the GitHub pull request's CI results.

**1. Before-and-After Verification**

Before implementation, `examples/fastapi_tracking.py` did not exist, so developers could not run the requested FastAPI reference example.

After adding the file, I confirmed that the application could start successfully and that both endpoints were accessible.

**2. Python Syntax Validation**

I checked the example for Python syntax errors using:

```powershell
python -m py_compile examples/fastapi_tracking.py
```

Result: The command completed successfully without syntax errors.

**3. FastAPI Endpoint Testing**

I started the application from the repository root:

```powershell
python -m uvicorn examples.fastapi_tracking:app --app-dir "$HOME\OneDrive\Desktop\AI301\ecotrace" --host 127.0.0.1 --port 8000
```

In another terminal, I tested both endpoints:

```powershell
curl.exe -i http://127.0.0.1:8000/health
curl.exe -i http://127.0.0.1:8000/compute
```

Observed results:
- `/health` returned HTTP 200 with {"status":"ok"}.
- `/compute` returned HTTP 200 with {"status":"completed","result":333332833333500000}.
- Both endpoints included the `X-Eco-Carbon-Emitted` response header.
- Both endpoints included the `X-Eco-Duration` response header.
These results confirmed that the FastAPI application worked and that the existing EcoTrace middleware was integrated into the request lifecycle.

**4. Repository Test Suite**

I ran the existing pytest suite:

```powershell
python -m pytest -q
```

Observed result:

```text
239 passed, 2 skipped in 58.90s
```

The existing test suite passed without requiring changes to the core package.

The two skipped tests were in `tests/test_langchain_callback.py` (lines 188 and 203) because the optional langchain_core test modules were unavailable in my environment. These were skips, not test failures.

**5. Git Change Validation**

Before committing, I inspected the staged changes and ran:

```powershell
git diff --cached --check
```

Result: No whitespace errors were reported.

**6. GitHub Pull Request Checks**

After opening PR #228, GitHub reported 11 successful checks. The SonarQube Quality Gate also passed, with no new issues or security hotspots reported.

The pull request was subsequently approved and merged by the repository owner.

**Evidence**
- Pull request and CI checks: https://github.com/Zwony/ecotrace/pull/228
- Implementation commit: https://github.com/Zwony/ecotrace/pull/228/commits/0d6d842
**Toolkit**
- Tool: Python py_compile, pytest, Uvicorn, `curl.exe`, Git, GitHub Actions, and SonarQube.
- What it produced: Successful syntax validation, HTTP 200 responses with expected JSON and emissions-tracking headers, 239 passing tests with 2 skips, a clean Git whitespace check, and 11 successful GitHub checks.
- Difficulties: The Uvicorn import path initially depended on the working directory. I also needed to verify that the emissions headers were actually present rather than relying only on successful HTTP responses.
- What changed: I corrected the application launch command, tested both endpoints with `curl.exe` -i to inspect response headers, and used the repository's automated test suite and CI checks to confirm that the contribution did not introduce detected regressions.

## Implementation Notes
October 2026 - Issue investigation and maintainer clarification (exact day not recorded here)

I reviewed EcoTrace Issue #211 and explored the repository to understand its existing middleware and examples. During this investigation, I discovered that the issue referenced `StarletteEmissionsMiddleware`, but the repository provided `EcoTraceMiddleware` in `ecotrace.middleware.fastapi`.

I contacted the maintainer to clarify which implementation I should use. The maintainer confirmed that the example should use the existing middleware and its supported response headers. This prevented me from introducing unnecessary changes to the core package.

October 2026 - Environment setup and implementation (exact day not recorded here)

I cloned my EcoTrace fork, created the `feat/fastapi-example` branch, and set up a Python virtual environment on Windows. I installed the required dependencies and created `examples/fastapi_tracking.py`.

I implemented a minimal FastAPI application, registered `EcoTraceMiddleware`, and added two routes. The `/health` route returned a simple status response, while `/compute` performed a CPU-intensive calculation to demonstrate request tracking.

I also added a module docstring explaining how to install dependencies, start the application, call the endpoints, and inspect the emissions and duration headers.

October 2026 - Local testing and validation (exact day not recorded here)

During testing, I encountered an import-path problem when attempting to launch the example using the short module name from the repository root.

I resolved this by using `uvicorn examples.fastapi_tracking:app --reload` from the repository root. I also verified that `uvicorn fastapi_tracking:app --reload` worked from the examples/ directory.

I tested both endpoints using `curl.exe` and confirmed that they returned HTTP 200 with the expected JSON and the `X-Eco-Carbon-Emitted` and `X-Eco-Duration` response headers.

I then ran Python syntax validation and the repository's pytest suite. The tests completed with 239 passed and 2 skipped. I checked the staged Git changes for whitespace errors before committing.

October 29, 2026 - Pull request and merge

I committed the implementation on the `feat/fastapi-example` branch and opened PR #228 against the EcoTrace repository.

The pull request passed 11 GitHub checks, including the SonarQube Quality Gate. The repository owner reviewed the implementation, confirmed that it met the issue requirements, and approved and merged the contribution.

This was my first completed contribution for this assignment, and the review process helped me understand the importance of small, focused changes, accurate documentation, and validating behavior before requesting a merge.

**Toolkit**
- Tool: VS Code, PowerShell, Git, GitHub, Python, pytest, Uvicorn, and `curl.exe`.
- What it produced: A working FastAPI example, validated HTTP responses and tracking headers, successful automated test results, and a merged pull request.
- Difficulties: The original issue description did not match the existing middleware implementation, and the initial Uvicorn launch command caused an import-path problem.
- What changed: I confirmed the correct middleware with the maintainer, adjusted the example's documentation and launch commands, and verified the implementation through local testing and GitHub CI before the contribution was merged.

## Pull Request
PR Link: https://github.com/Zwony/ecotrace/pull/228

PR Description:

I opened PR #228 to address EcoTrace Issue #211 by adding a self-contained FastAPI emissions-tracking reference example.

The pull request introduced `examples/fastapi_tracking.py`, which demonstrates how to integrate EcoTrace's existing `EcoTraceMiddleware` into a FastAPI application.

The example includes:
- A `/health` endpoint for a lightweight health check.
- A `/compute` endpoint that performs a CPU-intensive calculation.
- Middleware registration using `app.add_middleware(EcoTraceMiddleware)`.
- Instructions for installing dependencies and starting the application with Uvicorn.
- Documentation of the `X-Eco-Carbon-Emitted` and `X-Eco-Duration` response headers.
The contribution was intentionally limited to a new example file. No existing core package functionality was modified.

Before opening the pull request, I validated Python syntax, manually tested both endpoints, and ran the repository's pytest suite, which completed with 239 passed and 2 skipped.

Maintainer Feedback:
- Before implementation: I contacted the repository owner to clarify an inconsistency between the issue description and the existing middleware. The maintainer confirmed that I should use `EcoTraceMiddleware` and the existing X-Eco-* response headers.
- During pull request review: The repository owner reviewed the example and positively acknowledged its clean implementation, endpoint structure, docstrings, middleware integration, and alignment with the issue requirements.
- After review: All 11 GitHub checks passed, including the SonarQube Quality Gate. The maintainer approved and merged the pull request. No additional core package changes were required.
Status: Merged

Implementation Commit: https://github.com/Zwony/ecotrace/pull/228/commits/0d6d842

**Toolkit**
- Tool: Git, GitHub pull requests, GitHub Actions, SonarQube, maintainer discussions, and CodePath's PR-monitor with my personal playbook.
- What it produced: A reviewed and merged FastAPI example with 11 passing GitHub checks. On November 3, 2026, the PR-monitor generated `run-report.md` and `drafted-move.md`, confirming that PR #228 was merged and suggesting a follow-up to close Issue #211 if necessary.
- Difficulties: The original issue referenced a different middleware implementation, requiring maintainer clarification. The monitor also could not confirm whether Issue #211 was closed, so its suggested follow-up required independent verification.
- What changed: I used the maintainer-approved middleware and validated the implementation before merging. After running the monitor, I checked Issue #211 using GitHub CLI and confirmed it was closed as completed. Because I had already thanked the maintainer, I declined the unnecessary follow-up rather than posting another comment.

## Learnings and Reflections
**Technical Skills Gained**

Through this contribution, I gained practical experience integrating middleware into a FastAPI application. I learned how `EcoTraceMiddleware` works within the HTTP request lifecycle and how to verify emissions and execution-duration tracking through response headers.

I improved my ability to navigate an unfamiliar Python repository, inspect existing implementations, configure a virtual environment, and troubleshoot Python module import paths. I also gained experience testing API endpoints with Uvicorn and `curl.exe`, validating Python syntax, running pytest, and using GitHub CI results to evaluate a contribution before merging.

**Challenges Overcome**

The biggest challenge was discovering that the original issue description referenced a middleware class and response header that did not match the actual repository. Instead of assuming the issue description was correct, I inspected the source code and asked the maintainer for clarification. This helped me avoid implementing an unnecessary middleware class.

Another challenge was launching the FastAPI example from the correct working directory. I resolved the import problem by adjusting the Uvicorn module path and documenting both supported launch commands.

I also learned that a successful HTTP response alone is not enough to validate middleware integration. I checked the response headers to confirm that emissions and duration tracking were actually present.

**What I'd Do Differently Next Time**

For my next open-source contribution, I would inspect the relevant source files and existing tests earlier, before finalizing an implementation plan. I would also verify the project's execution commands from the repository root and document the expected behavior before writing code.

I would continue communicating with maintainers when requirements are unclear and keep my pull requests focused on one well-defined change. This experience showed me that a useful contribution does not need to be large; it needs to solve the requested problem, be easy to understand, and include evidence that it works.

## Resources Used
The following resources helped me understand the issue, implement the FastAPI example, validate its behavior, and complete the contribution.
- EcoTrace Issue #211: https://github.com/Zwony/ecotrace/issues/211
  I used the issue description to understand the requested example and the maintainer discussion to clarify the correct middleware implementation and response headers.
- EcoTrace Pull Request #228: https://github.com/Zwony/ecotrace/pull/228
  I used the pull request to document my implementation, review automated checks, receive maintainer feedback, and confirm that the contribution was merged.
- EcoTrace Middleware Source Code: https://github.com/Zwony/ecotrace/blob/main/ecotrace/middleware/fastapi.py
  I inspected the existing middleware to identify the correct import path, middleware class, and supported response headers.
- FastAPI Documentation: https://fastapi.tiangolo.com/
  I referred to FastAPI concepts while building the application, registering middleware, and defining HTTP endpoints.
- Uvicorn Documentation: https://www.uvicorn.org/
  I used Uvicorn to run the FastAPI application locally and troubleshoot the module import path.
- pytest Documentation: https://docs.pytest.org/
  I used pytest to run the repository's automated test suite and verify that the existing tests passed.
- GitHub Documentation: https://docs.github.com/en/pull-requests
  GitHub's pull request workflow helped me organize my changes, review CI results, and track the maintainer's approval and merge.
