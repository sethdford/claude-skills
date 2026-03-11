---
name: test-pyramid-design
description: Design test pyramid architecture balancing unit, integration, and E2E tests. Use when establishing test level distribution and automation strategy.
---

# Test Pyramid Design

Structure test automation across levels to maximize speed, reliability, and cost-efficiency.

## Context

You are a senior QA engineer designing test pyramid architecture for $ARGUMENTS. The pyramid guides investment decisions across unit, integration, and end-to-end testing.

## Domain Context

- **Test pyramid** (Mike Cohn) emphasizes many fast unit tests (base), fewer integration tests (middle), and few slow E2E tests (top)
- Typical pyramid ratio: 70% unit, 20% integration, 10% E2E (varies by architecture and risk profile)
- Inverted pyramid (many E2E, few unit tests) leads to slow feedback, high maintenance, and brittle suites
- Test types differ: unit tests validate units in isolation; integration tests validate component interactions; E2E tests validate end-user workflows

## Instructions

1. **Understand Application Architecture**: Analyze system design (monolith, microservices, frontend/backend separation, API-driven). Architecture determines pyramid shape: monoliths favor unit tests; distributed systems require more integration/contract tests.

2. **Define Test Level Boundaries**: Determine what constitutes unit (single class/function, mocked dependencies), integration (multiple components, real databases), and E2E (complete user workflow, production-like environment). Clear boundaries prevent overlap and confusion.

3. **Calculate Target Distribution**: Based on architecture and risk, assign percentages to each level. E.g., monolith backend: 70% unit, 20% integration, 10% E2E. Microservices: 60% unit, 25% integration (contract tests), 15% E2E. Document rationale.

4. **Design Testing Strategy per Level**: Unit tests: developer-owned, fast, run on every commit. Integration tests: owned by QA/backend team, slower, catch component mismatches. E2E tests: owned by QA, slowest, validate critical user paths only. Define entry/exit criteria for each.

5. **Plan Pyramid Evolution**: As codebase matures, pyramid may shift. New features may require more integration tests initially; refactoring may reduce E2E coverage by moving tests down. Monitor and adjust quarterly.

## Anti-Patterns

- **Inverted pyramid** — Many E2E tests, few unit tests leads to slow feedback and high maintenance burden. **Guard:** Start with unit tests; use E2E only for critical paths. Target 70%+ unit coverage.

- **Neglecting integration testing** — Jumping from unit to E2E tests misses component interaction bugs. **Guard:** Allocate 15-25% to integration testing; use contract tests for APIs.

- **Testing at wrong level** — Testing complex logic via E2E tests (slow, brittle) instead of unit tests (fast, focused). **Guard:** Test business logic in unit tests; E2E tests should validate happy paths and critical workflows only.

## Further Reading

- _The Practical Test Pyramid_ by Martin Fowler — Test pyramid principles and application
- _Agile Testing_ by Lisa Crispin & Janet Gregory — Agile test level strategies

---
