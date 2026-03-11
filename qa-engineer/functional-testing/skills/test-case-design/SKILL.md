---
name: test-case-design
description: Design systematic test cases covering valid inputs, invalid inputs, and edge cases. Use when creating manual test suites.
---

# Test Case Design

Create comprehensive, effective test cases that validate application behavior across scenarios.

## Context

You are a senior QA engineer designing test cases for $ARGUMENTS. Each test case must have clear purpose, preconditions, steps, and expected results.

## Domain Context

- **Test case** is a specification of inputs, execution preconditions, expected outputs, and executable steps
- **Test case design** combines multiple techniques: boundary value analysis, equivalence partitioning, decision tables, error guessing
- **Well-designed test cases** are independent, repeatable, clear, and traceability-mapped to requirements
- ISTQB defines test case design as fundamental QA activity across all test levels

## Instructions

1. **Analyze Requirements**: Break down functional requirements into testable scenarios. Identify happy paths (normal operation), alternative paths (variations), and error paths (invalid inputs, exception handling). Document requirement traceability.

2. **Apply Design Techniques**: Use boundary value analysis (test at boundaries: 0, 1, max, max+1), equivalence partitioning (test one value per partition), error guessing (heuristic failure modes). Combine techniques to achieve comprehensive coverage without test explosion.

3. **Create Test Cases**: For each scenario, write test case with: title, preconditions, steps, expected result, test data. Include positive tests (valid inputs, expected behavior), negative tests (invalid inputs, error handling), and edge case tests (boundary conditions).

4. **Review Test Cases**: Validate test cases for clarity (another QA engineer can execute without ambiguity), independence (tests don't depend on each other), and completeness (all requirements covered, all error paths included). Identify redundant tests; consolidate related tests.

5. **Organize Test Cases**: Structure tests in logical groups (by feature, by scenario, by priority). Establish test case numbering/naming convention. Document test case relationships and dependencies. Track traceability between requirements and test cases.

## Anti-Patterns

- **Vague test case steps** — Steps like "enter customer data" leave executors guessing at exact input. **Guard:** Document exact values: "Enter '12345678' in customer ID field", "Select 'Gold' from membership tier dropdown".

- **Test case sprawl** — Creating hundreds of similar test cases without strategy leads to maintenance burden. **Guard:** Use design techniques (BVA, equivalence partitioning) to minimize test count; combine related scenarios into parameterized tests.

- **Missing negative tests** — Testing happy paths only misses error handling defects. **Guard:** For each positive test, create corresponding negative tests: invalid input, missing data, out-of-range values.

## Further Reading

- _Test Case Design Techniques_ from Google Testing Blog
- _ISTQB Foundation Syllabus_ — Test case design fundamentals

---
