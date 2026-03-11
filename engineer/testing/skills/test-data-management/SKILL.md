---
name: test-data-management
description: Creating and managing test data via fixtures, builders, factories, and minimal realistic datasets.
---

# Test Data Management

Strategies for creating and maintaining test data.

## Context

You are designing test data infrastructure. Good test data is realistic but lightweight.

## Domain Context

- **Fixtures**: Pre-built test data sets; inflexible but fast
- **Builders**: Fluent API to construct objects; flexible, readable
- **Factories**: Methods that generate test data; reusable, minimal
- **Realistic**: Use production-like data; but omit sensitive info
- **Minimal**: Only data relevant to the test; avoid clutter

## Instructions

1. **Choose Strategy**: Fixtures (pre-built), Builders (flexible), Factories (reusable)
2. **Use Builders for Complex Objects**: Clear intent; easy to vary specific fields
3. **Create Factories for Common Patterns**: User factory, Order factory
4. **Avoid Shared State**: Each test gets fresh data; no pollution
5. **Seed Data Carefully**: Use realistic but non-sensitive data
6. **Document Defaults**: Default builder state should be valid for most tests
7. **Performance**: Consider test database resets vs. transactions for cleanup

## Anti-Patterns

- Massive fixture files with hundreds of records; hard to understand which data matters
- Global shared test data; tests interfere with each other
- Over-realistic test data (full names, addresses); wastes resources
- Complex object construction in tests; use builders instead
- Test data stored in files separate from tests; couples tests to external state

## Further Reading

- Gerard Meszaros, _xUnit Test Patterns_, on Test Fixture Strategies
- Roy Osherove, _The Art of Unit Testing_, on Test Data
