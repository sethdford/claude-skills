---
name: decision-table-testing
description: Use decision tables to test complex business logic with multiple conditions. Use when testing rules and workflows with many input combinations.
---

# Decision Table Testing

Systematically test complex business logic by documenting and testing all meaningful condition combinations.

## Context

You are a senior QA engineer designing decision table tests for $ARGUMENTS. Decision tables excel at documenting complex rules.

## Domain Context

- **Decision table** (ISTQB) documents inputs, conditions, actions, and rules in tabular format
- Effective for testing business rules, workflows, and complex logic
- Eliminates guessing at which condition combinations matter
- Helps identify missing or conflicting rules

## Instructions

1. **Identify Conditions and Actions**: List all input conditions (age > 18? approved? overdraft?) and corresponding actions (approve, deny, review).

2. **Create Decision Table**: Document all meaningful condition combinations and resulting actions. Eliminate redundant combinations; consolidate where possible.

3. **Design Tests**: Create test case for each rule in decision table. Use decision table values as test data.

4. **Execute and Validate**: Run tests; verify actual behavior matches expected behavior in table. Document discrepancies.

5. **Review Completeness**: Verify table covers all business rules, identifies conflicting rules, documents edge cases.

## Anti-Patterns

- **Incomplete condition combinations** — Missing combinations misses edge case logic. **Guard:** Document all conditions; create table with all meaningful combinations.

- **Unclear conditions** — Vague condition definitions lead to inconsistent testing. **Guard:** Define conditions precisely with measurable criteria.

- **Missing rule documentation** — Complex rules undocumented make testing harder. **Guard:** Use decision tables to document all rules explicitly.

## Further Reading

- _Decision Table Testing_ from ISTQB Syllabus
- _Effective Software Testing_ — Decision table application

---
