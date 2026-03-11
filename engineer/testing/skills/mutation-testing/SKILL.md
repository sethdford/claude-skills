---
name: mutation-testing
description: Measuring test quality by mutating code and checking if tests catch mutations.
---

# Mutation Testing

Technique to measure how well tests detect bugs by injecting mutations.

## Context

You are using mutation testing to validate test quality. High mutation score means tests actually verify behavior.

## Domain Context

- **Mutation**: Small code change; operator flip, boundary change, constant modification
- **Killed**: Test fails on mutation; test is effective
- **Survived**: Test passes on mutation; gap in test coverage
- **Goal**: 80%+ mutation score indicates strong tests
- **Tools**: PIT (Java), Stryker (JavaScript), Mutant (Ruby)

## Instructions

1. **Run Baseline**: Execute test suite; note coverage
2. **Inject Mutations**: Tool modifies code (< becomes <=, true becomes false)
3. **Run Tests**: Check if tests catch each mutation
4. **Identify Survivors**: Which mutations did tests miss? Why?
5. **Strengthen Tests**: Add tests for survivor scenarios
6. **Repeat**: Run mutation testing again; iterate until satisfied

## Anti-Patterns

- Ignoring mutation testing; high code coverage doesn't guarantee good tests
- Trying to reach 100% mutation score; diminishing returns after 80%
- Adding tests just to kill mutations; tests should be meaningful
- Slow mutation testing blocking development; run on critical paths
- Not understanding why mutations survived; just adding tests blindly doesn't help

## Further Reading

- Richard Lipton, "The Fault-Based Testing (FBT) Paradigm"
- PIT documentation (Java mutation testing)
- Stryker documentation (JavaScript/TypeScript mutation testing)
