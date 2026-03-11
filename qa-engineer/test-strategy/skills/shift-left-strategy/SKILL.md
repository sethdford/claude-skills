---
name: shift-left-strategy
description: Design shift-left testing strategies to catch defects early. Use when planning early involvement of QA in development.
---

# Shift-Left Testing Strategy

Integrate testing earlier in the development cycle to detect and prevent defects before they reach later stages.

## Context

You are a senior QA engineer designing a shift-left strategy for $ARGUMENTS. Shift-left emphasizes early quality assurance, developer testing, and proactive defect prevention.

## Domain Context

- **Shift-left** means moving QA activities earlier in development: from post-development testing to concurrent/pre-development involvement
- Cost of defect increases exponentially across stages: unit (cheapest) → integration → system → production (most expensive)
- Shift-left practices: test-driven development (TDD), continuous integration, pair programming, code review, developer-owned unit tests
- ISTQB recognizes shift-left as critical to modern quality assurance

## Instructions

1. **Assess Current Test Timing**: Map where testing currently occurs relative to development (TDD during coding, code review post-coding, system testing post-integration). Identify late-stage test activities candidates for shifting left.

2. **Design Developer Testing Program**: Establish expectations for unit test ownership (developers must write and maintain unit tests). Provide TDD training or pair programming sessions. Define coding standards including test coverage minimums (e.g., critical paths must have unit tests).

3. **Integrate QA in Design Phase**: Have QA participate in design reviews and architecture decisions. Identify testability concerns early: unclear requirements, hard-to-test designs, missing error paths. Propose alternatives that improve testability.

4. **Establish Quality Gates**: Create entry/exit criteria for each development stage: code review gates (e.g., 80% code coverage), integration gates (e.g., all tests pass), feature gates (e.g., exploratory testing complete). Automate gates where possible.

5. **Measure Shift-Left Impact**: Track metrics that indicate early quality: defects found in unit tests vs. system tests, defect density per stage, escape rate (defects reaching production). A successful shift-left shows higher early detection rates.

## Anti-Patterns

- **Eliminating later-stage testing** — Shifting left doesn't mean eliminating system or exploratory testing; it means adding early testing, not replacing comprehensive testing. **Guard:** Maintain all test levels; shift-left adds rigor earlier, not fewer tests later.

- **Overloading developers** — Expecting developers to be test automation experts without training leads to poor-quality automated tests. **Guard:** Provide TDD training, pair programming support, and tools; start with unit testing before expanding expectations.

- **False security from early tests** — Unit tests passing doesn't guarantee system works. **Guard:** Shift-left complements, not replaces, system and exploratory testing; maintain comprehensive test coverage across levels.

## Further Reading

- _Test Driven Development: By Example_ by Kent Beck — TDD as foundational shift-left practice
- _Agile Testing_ by Lisa Crispin & Janet Gregory — Shift-left in agile teams

---
