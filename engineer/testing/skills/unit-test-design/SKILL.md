---
name: unit-test-design
description: Single-unit tests, isolation via mocks/stubs, Arrange-Act-Assert pattern, one assertion per test.
---

# Unit Test Design

Principles for isolated, focused, maintainable unit tests.

## Context

You are helping the engineer write unit tests. Design each test to verify one piece of behavior in isolation.

## Domain Context

- **Isolation**: Test one method/class; mock dependencies
- **Arrange-Act-Assert**: Setup data, execute behavior, verify results
- **One Assertion per Test**: Focus; easier to understand failure
- **Fast**: Unit tests run in milliseconds; if slow, you have external dependencies
- **Deterministic**: Same result every run; no random data, no timing issues

## Instructions

1. **Identify Unit**: What single behavior are you testing? One method or small class
2. **Mock Dependencies**: Replace real database, HTTP, file I/O with mocks
3. **Arrange**: Setup test data; prepare mocks
4. **Act**: Call the method under test with inputs
5. **Assert**: Verify output or mock invocations
6. **Name Clearly**: `testShouldReturnUserWhenIdExists` not `test1`
7. **Test Edge Cases**: null inputs, empty collections, boundary values

## Anti-Patterns

- Tests that test the mock, not the code; mock returns setup values and test verifies setup
- Massive test fixtures with unneeded setup; each test should setup only what it needs
- Multiple assertions per test; when one fails, don't know which behavior broke
- Exposing implementation details; test behavior, not private methods
- Skipping dependency injection in production code to avoid mocking; if hard to test, architecture is wrong

## Further Reading

- Roy Osherove, _The Art of Unit Testing_
- Michael Feathers, _Working Effectively with Legacy Code_, Part I
