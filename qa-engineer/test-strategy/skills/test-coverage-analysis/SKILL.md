---
name: test-coverage-analysis
description: Measure and analyze test coverage gaps. Use when identifying untested code paths and assessing coverage sufficiency.
---

# Test Coverage Analysis

Systematically measure code and requirement coverage to identify gaps and validate test effectiveness.

## Context

You are a senior QA engineer analyzing test coverage for $ARGUMENTS. Coverage analysis reveals which code paths and requirements are tested and which remain untested.

## Domain Context

- **Code coverage** measures how much source code is exercised by tests (line, branch, condition, path coverage)
- **Requirement coverage** measures which business/functional requirements have corresponding tests
- **Coverage metrics** provide visibility but are not quality metrics (high coverage doesn't guarantee quality; low coverage indicates risk)
- ISO/IEC 25010 software quality model includes test coverage as a means to assess quality (not an end itself)

## Instructions

1. **Select Coverage Dimensions**: Choose applicable coverage metrics based on testing level: statement coverage for unit tests (baseline), branch coverage for integration tests, requirement coverage for system tests. Avoid pursuing path coverage in large systems (combinatorial explosion).

2. **Establish Coverage Baselines**: Measure current coverage before adding new tests. Identify baseline gaps: untested error paths, exception handlers, rarely-used features. Document coverage by module/component.

3. **Identify Coverage Gaps**: Analyze gaps in coverage: code paths not exercised, business scenarios not tested, error conditions not validated. Prioritize gaps by risk: high-risk code (security, critical paths) receives attention before low-risk code.

4. **Design Gap-Closing Tests**: For each significant gap, design specific tests that exercise the missing paths or scenarios. Ensure tests are meaningful, not just coverage-chasing (stub tests that don't validate behavior).

5. **Monitor Coverage Trends**: Track coverage metrics over time. Expect coverage to increase incrementally; sudden drops indicate missing tests for new code. Use coverage as a leading indicator of testing adequacy, not a final verdict.

## Anti-Patterns

- **Coverage-driven development** — Targeting high coverage without testing meaningful behavior leads to brittle tests that pass despite defects. **Guard:** Measure coverage, but judge test effectiveness by defect detection, not coverage percentage alone.

- **False coverage** — High coverage that ignores negative testing or error paths provides false confidence. **Guard:** Use mutation testing to verify that tests actually validate behavior; ensure error paths have specific assertions.

- **Coverage without context** — Comparing coverage metrics across projects ignores risk profiles and quality goals. **Guard:** Set coverage targets based on risk assessment and project context, not arbitrary percentages (e.g., "80% is good").

## Further Reading

- _Pragmatic Unit Testing_ by Andy Hunt & Dave Thomas — Coverage as a testing aid, not a goal
- _Code Coverage Analysis_ from Google Testing Blog — Effective use of coverage metrics

---
