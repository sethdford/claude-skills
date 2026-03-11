---
name: maintainability-assessment
description: Assess and design for maintainability. Evaluate code complexity, coupling, and testability. Use when evaluating codebase health or designing for long-term evolution.
---

# Maintainability Assessment

Evaluate and design systems for long-term maintainability through low coupling, high cohesion, and comprehensive testing.

## Context

You are assessing code quality or designing for evolution. The user faces high maintenance costs or slow feature velocity. Read their codebase and team structure.

## Domain Context

Based on Martin Fowler, Michael Feathers, and software engineering research:

- **Coupling**: Dependencies between components. High coupling slows change.
- **Cohesion**: Responsibility focus within component. High cohesion eases understanding.
- **Cyclomatic Complexity**: Number of decision paths. High complexity = hard to test and change.
- **Code Smells**: Patterns indicating deeper problems (long methods, feature envy, rigid hierarchies)
- **Technical Debt**: Shortcuts taken now that cost more later (skipped tests, quick hacks, outdated dependencies)

## Instructions

1. **Measure Code Quality**: Static analysis: cyclomatic complexity (target <10 per function), code duplication (<3%), test coverage (target >80%).

2. **Assess Coupling**: Map dependencies between modules. Are there circular dependencies? Can you change one module without touching others?

3. **Evaluate Testability**: Can components be tested in isolation? Are dependencies injectable? Are there integration tests? Can tests run fast (<5 seconds)?

4. **Identify Tech Debt**: List known quick fixes, outdated dependencies, deferred refactoring. Estimate payoff vs effort to address.

5. **Design for Evolution**: Decouple through interfaces, dependency injection, and events. Small, focused modules. Comprehensive tests provide safety net.

## Anti-Patterns

- **Optimizing for Initial Build**: Architect for speed to first release. Result: unmaintainable mess after 6 months. **Guard**: Design for readability and change, not for speed.
- **Ignoring Test Coverage**: "It works" but no tests. Result: any change risks regression. **Guard**: Tests > code; without tests, refactoring is dangerous.
- **Massive God Objects**: 10,000-line classes doing everything. Result: impossible to understand and change. **Guard**: Split into focused objects; each with single responsibility.
- **No Refactoring Time**: Always shipping features, never paying down debt. Result: velocity slows and stays slow. **Guard**: Reserve 20-30% of time for refactoring and debt paydown.

## Further Reading

- _Clean Code_ by Robert Martin — maintainability through naming, small functions, tests
- _Working Effectively with Legacy Code_ by Michael Feathers — refactoring strategies for messy codebases
- _Refactoring_ by Martin Fowler — techniques for improving code structure
