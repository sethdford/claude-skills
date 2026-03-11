---
name: dependency-injection
description: Designing loosely coupled code through dependency injection, reducing testability barriers and hidden dependencies.
---

# Dependency Injection

Fundamental pattern for loose coupling and testability.

## Context

You are helping the engineer apply dependency injection. If code is provided, identify tightly coupled dependencies and suggest injection patterns. DI is not optional for testable, maintainable code.

## Domain Context

- **Loose Coupling**: Dependencies are explicit parameters, not hidden inside the class
- **Testability**: You can inject mocks, stubs, or fakes for testing without modification
- **Inversion of Control**: Class doesn't create its dependencies; they're provided
- **Three Patterns**: Constructor Injection (preferred), Setter Injection, Interface Injection
- **Container**: Optional; frameworks like Spring, Guice manage dependency graphs

## Instructions

1. **Identify Hard Dependencies**: What does the class create or reference? httpClient, database, logger?
2. **Declare Dependencies**: Add constructor parameters for each dependency (prefer constructor over setter)
3. **Make Testable**: Can you pass in a mock? If not, you're still too tightly coupled
4. **Use Interfaces**: Depend on abstractions (Logger), not concrete implementations (ConsoleLogger)
5. **Avoid Service Locator**: Don't pass in a container or factory; too implicit
6. **Document Contracts**: Make it clear which dependencies are required vs. optional
7. **Keep Constructors Simple**: Only assign fields; avoid logic or other dependencies
8. **Validate Dependencies**: Check for null; fail fast if required dependency is missing

## Anti-Patterns

- Instantiating dependencies directly in the constructor or methods; you've coupled to the concrete type
- Creating a "service locator" factory and passing it everywhere; defeats the purpose of DI
- Injecting heavy frameworks or containers; inject thin abstractions instead
- Setter injection when constructor injection would suffice; constructor makes requirements explicit
- Circular dependencies; indicates design problem; refactor to break the cycle
- Ignoring dependency lifetime (singleton vs. transient); wrong lifetimes cause bugs

## Further Reading

- Martin Fowler, "Inversion of Control Containers and the Dependency Injection pattern"
- Michael Feathers, _Working Effectively with Legacy Code_, Chapter 20 (Dependency Injection)
- Gang of Four, _Design Patterns_, Strategy and Factory patterns
