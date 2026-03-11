---
name: equivalence-partitioning
description: Partition test input domain into equivalence classes to reduce test count. Use when testing multiple similar scenarios.
---

# Equivalence Partitioning

Divide input domain into partitions where all values behave equivalently, allowing representative testing without exhaustive test cases.

## Context

You are a senior QA engineer applying equivalence partitioning for $ARGUMENTS. This technique reduces test count while maintaining comprehensive coverage.

## Domain Context

- **Equivalence partitioning** assumes inputs within partition behave equivalently, so testing one value per partition suffices
- Partitions include: valid values (expected behavior) and invalid values (error handling)
- Combined with boundary value analysis, creates systematic test design
- Reduces test explosion: 100 possible ages reduces to 3-4 partitions

## Instructions

1. **Identify Partitions**: For each input, identify groups where values behave similarly: age (0-17 invalid, 18-65 valid, 66+ invalid); email (valid format, invalid format); status (active, inactive, deleted).

2. **Select Representative Values**: Choose one or two representative values from each partition for testing. Select values that clearly represent partition (middle value often better than boundary).

3. **Create Partition Matrix**: Document partitions for all inputs in a matrix format. Combine input partitions to identify test scenarios. Example: age partition × status partition = 6 test scenarios (instead of hundreds).

4. **Design Test Cases**: Create test cases covering all partitions. Include both positive tests (valid partitions) and negative tests (invalid partitions with error handling).

5. **Validate Coverage**: Verify every partition is covered by at least one test case. Identify gaps (untested partitions) and add tests as needed.

## Anti-Patterns

- **Arbitrary partitions** — Partitioning without clear rationale leads to weak tests. **Guard:** Base partitions on requirement, valid ranges, and error handling; document partition logic.

- **Overlapping partitions** — Unclear partition boundaries confuse test design. **Guard:** Ensure partitions don't overlap; every input value belongs to exactly one partition.

- **Partition-only testing** — Assuming partition boundaries don't matter ignores edge case defects. **Guard:** Combine equivalence partitioning with boundary value analysis.

## Further Reading

- _Equivalence Partitioning_ from ISTQB Syllabus
- _Test Design Patterns_ — Partitioning strategies

---
