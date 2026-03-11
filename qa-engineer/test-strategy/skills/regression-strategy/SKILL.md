---
name: regression-strategy
description: Develop regression test strategies and maintenance approaches. Use when managing regression risk across releases.
---

# Regression Testing Strategy

Design systematic approaches to detect unintended side effects from code changes.

## Context

You are a senior QA engineer designing regression testing strategy for $ARGUMENTS. Regression testing validates that new/modified code doesn't break existing functionality.

## Domain Context

- **Regression testing** re-executes previously passed tests to detect if changes introduce new failures
- **Regression risk** increases with scope of changes: small bug fixes have low regression risk; large refactors have high regression risk
- **Regression test suite** should include: critical paths, frequently-used features, areas touched by changes, integration points
- Selective regression testing prioritizes tests based on change impact (coverage-based, risk-based, or history-based selection)

## Instructions

1. **Establish Regression Test Baseline**: Define core regression suite including critical user workflows, frequently-used features, and high-risk areas. This baseline runs on every build. Size baseline to fit within acceptable test execution window (e.g., 30-60 minutes for CI/CD).

2. **Implement Change-Based Test Selection**: Analyze code changes and select regression tests that cover affected code paths. Use coverage tools or static analysis to identify related code regions. For small hotfixes, run targeted tests; for large changes, run full regression suite.

3. **Create Regression Test Priorities**: Tier regression tests: priority 1 (critical paths, 100% coverage), priority 2 (important features, frequent use), priority 3 (rare features, nice-to-have). Run P1 on every build; P2 on release branches; P3 before releases.

4. **Automate Regression Tests**: Regression tests must be automated for repeatability and speed. Maintain automation quality: clear assertions, independent tests, reliable execution. Monitor automation health: failing tests, timeouts, flakiness.

5. **Review and Refactor Regularly**: As codebase evolves, regression suite may accumulate redundant or obsolete tests. Quarterly review: remove duplicate tests, consolidate overlapping coverage, add tests for newly fixed bugs. Keep suite maintainable.

## Anti-Patterns

- **Regression suite bloat** — Accumulating tests without pruning leads to long execution times and maintenance burden. **Guard:** Quarterly reviews; remove redundant tests; target execution time of 30-60 minutes for full regression.

- **Regression without automation** — Manual regression testing is slow and error-prone. **Guard:** Automate all regression tests; manual testing should be exploratory, not regression.

- **Ignoring new bug patterns** — Recurring bugs indicate missing regression coverage. **Guard:** When fixing bugs, add regression tests that would have caught them; analyze bug patterns to identify coverage gaps.

## Further Reading

- _Effective Software Testing_ by Effective Software Testing — Regression test design and maintenance
- _ISTQB Syllabus_ — Regression testing principles and approaches

---
