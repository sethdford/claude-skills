---
name: test-doubles-strategy
description: Choosing between mocks, stubs, fakes, spies, and dummies based on testing needs.
---

# Test Doubles Strategy

Strategies for replacing real objects with test doubles.

## Context

You are selecting the right test double for the job. Understand the tradeoffs of each approach.

## Domain Context

- **Stub**: Returns canned answers; doesn't care how many times it's called
- **Mock**: Expects specific calls; verifies behavior
- **Fake**: Lightweight working implementation; slower but more realistic than stub
- **Spy**: Records calls; can verify and allow through to real object
- **Dummy**: Placeholder; passed but never used

## Instructions

1. **Stub**: Use when you need predictable return values; database returning test data
2. **Mock**: Use when you need to verify that a dependency was called correctly
3. **Fake**: Use for database or third-party service; test containers are modern fakes
4. **Spy**: Use when you need both verification and real behavior
5. **Dummy**: Use when dependency is required by signature but not used
6. **Avoid Over-Mocking**: If everything is mocked, you're not testing integration
7. **Prefer Fakes**: Modern practice uses test containers over mocks for external services

## Anti-Patterns

- Mocking everything; you need at least some real code to test
- Over-specifying mocks; brittle tests that fail on implementation changes
- Mocking your own code; mock external dependencies, not your logic
- Complex mock setup that's harder than the test; use factories or test builders
- Never testing error paths through mocks; ensure your error handling actually works

## Further Reading

- Martin Fowler, _Test Double_ essay
- Gerard Meszaros, _xUnit Test Patterns_
