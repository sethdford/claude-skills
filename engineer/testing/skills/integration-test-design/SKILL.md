---
name: integration-test-design
description: Testing multiple components together; contract verification; real I/O (database, HTTP). Use when testing component interactions.
---

# Integration Test Design

Tests that verify components work together correctly.

## Context

You are designing integration tests. These test real interactions with databases, APIs, or file systems.

## Domain Context

- **Real Dependencies**: Use real database, HTTP server, file system (or test containers)
- **Contracts**: Verify that components' assumptions about each other are correct
- **Fewer Tests**: Integration tests are slower; test key flows, not all paths
- **Setup Cost**: Creating realistic data is expensive; consider test factories
- **Flakiness Risk**: Real I/O introduces timing, concurrency issues

## Instructions

1. **Identify Interactions**: Which components must work together?
2. **Start with Real Dependencies**: Use test containers (Docker) for databases, caches
3. **Create Test Factories**: Build realistic data efficiently
4. **Test Key Flows**: Happy path + one or two error scenarios
5. **Verify Contracts**: Does the consumer of an API get what it expects?
6. **Handle Cleanup**: Reset state between tests to avoid flakiness
7. **Accept Slowness**: Slower is OK; integration tests are fewer and farther between

## Anti-Patterns

- Too many integration tests; they're slow, use resources, and should be rare
- Mocking the database in integration tests; defeats the purpose
- Shared test state; tests interfere with each other
- Ignoring cleanup; leftover data causes flaky tests
- Testing all code paths in integration tests; unit tests cover logic, integration tests cover plumbing

## Further Reading

- Martin Fowler, _Microservice Testing_, on integration testing
- Sam Newman, _Building Microservices_, on testing strategies
