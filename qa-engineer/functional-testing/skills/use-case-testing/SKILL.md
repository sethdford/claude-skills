---
name: use-case-testing
description: Derive test scenarios from use case specifications to validate end-to-end user workflows including main success, alternate, and exception paths. Use for acceptance testing and requirements validation.
---

# Use Case Testing

Derive comprehensive test scenarios from use case specifications, ensuring every main success path, alternate flow, and exception path is exercised end-to-end as a real user would experience it.

## Context

You are a senior QA engineer designing use case tests for $ARGUMENTS. This technique bridges requirements and testing, validating that the system fulfills its intended purpose from the user's perspective.

## Domain Context

- **ISTQB Foundation Syllabus (4.2.5)**: Use case testing is a black-box technique that derives tests from use case descriptions, covering main and alternative scenarios
- **Alistair Cockburn's _Writing Effective Use Cases_**: Defines the standard use case template — actor, preconditions, main success scenario, extensions (alternate/exception paths), postconditions, and guarantees
- **ISO/IEC 25010**: Functional appropriateness measures whether functions facilitate task completion — use case testing directly validates this
- **Requirements traceability** (IEEE 830): Each test case should trace back to a specific use case step, providing bidirectional coverage evidence

## Instructions

1. **Enumerate use cases**: List all use cases for the feature under test. For each, identify the primary actor, preconditions, trigger, and postconditions. If formal use cases don't exist, derive them from user stories, PRDs, or stakeholder interviews
2. **Map the main success scenario**: Walk through the happy path step by step. Each step becomes a test step with a specific assertion. The postcondition is the final assertion
3. **Extract alternate paths**: For each step in the main scenario, identify alternate paths — valid variations that still succeed (e.g., paying with credit card vs. PayPal). Each alternate path needs its own test scenario
4. **Extract exception paths**: For each step, identify what can go wrong — invalid input, timeout, permission denied, resource unavailable, concurrent modification. Each exception needs a test verifying:
   - The system displays an appropriate error
   - No data corruption occurs
   - The user can recover (return to a valid state)
5. **Compose end-to-end scenarios**: Combine paths into realistic user journeys that cross multiple use cases (e.g., register → browse → add to cart → checkout → receive confirmation). These integration-level tests catch handoff defects between features
6. **Build a use case / test matrix**: Create a traceability matrix mapping each use case path (main + alternates + exceptions) to test cases. Identify any paths without test coverage.

## Anti-Patterns

- **Happy-path-only testing** — LLMs generate thorough main success scenarios but produce superficial alternate and exception paths (often just "invalid input returns error"). **Guard:** Count paths — a well-specified use case typically has 3-8 extension paths per main scenario step. If your test suite has fewer exception tests than happy-path tests, coverage is insufficient.
- **Synthetic user behavior** — LLMs invent use case flows that look logical but don't match real user behavior (e.g., testing account deletion before testing account creation). **Guard:** Validate use case priority against analytics data or user research. Test the flows users actually follow, not just the flows that are logically possible.
- **Missing actor variations** — LLMs default to a single actor type and miss that the same use case behaves differently for admin vs. regular user vs. guest vs. API consumer. **Guard:** Enumerate all actor types and test each relevant use case with each actor role.

## Further Reading

- Alistair Cockburn, _Writing Effective Use Cases_ — Definitive guide to use case structure and levels
- ISTQB Foundation Level Syllabus, Section 4.2.5 — Use case testing as a specification-based technique
- Glenford Myers, _The Art of Software Testing_ — Systematic test derivation from specifications
- Karl Wiegers, _Software Requirements_, 3rd Edition — Requirements specification and traceability to testing

---
