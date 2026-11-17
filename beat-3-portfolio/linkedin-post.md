My first open-source Python contribution has been merged!

I contributed a working FastAPI example to EcoTrace, an open-source project that helps developers estimate the energy and carbon impact of software.

The most valuable lesson came before I wrote the code.

While reviewing the issue, I discovered that the requested middleware name and response headers didn't match the repository's implementation. Instead of assuming the instructions were correct, I checked the source and asked the maintainer for clarification.

With that guidance, I built a focused 49-line example demonstrating request-level emissions and duration tracking.

I verified both endpoints, confirmed the expected HTTP response headers, and ran the project's test suite: 239 tests passed, with 2 skipped. All 11 GitHub checks passed, and the maintainer merged my pull request on October 29, 2026.

This experience taught me that good engineering isn't just about writing code. It's about understanding existing systems, asking questions early, and validating your work.

I'm grateful to the EcoTrace maintainer for the guidance and review, and to CodePath for helping me build my open-source contribution workflow.

You can see my merged contribution here:
https://github.com/Zwony/ecotrace/pull/228

#OpenSource #Python #FastAPI #CodePath #SoftwareEngineering