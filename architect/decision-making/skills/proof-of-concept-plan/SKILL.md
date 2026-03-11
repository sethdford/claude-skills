---
name: proof-of-concept-plan
description: Plan and execute focused POCs to validate architectural decisions before full commitment.
---

# Proof of Concept Plan

Design focused POCs that test assumptions with minimal investment before full-scale commitment.

## Instructions

1. **Define Hypothesis**: What assumption are we testing?
2. **Scope Tightly**: POC solves one problem, not whole system
3. **Time-Box**: 1-4 weeks, fixed scope
4. **Success Criteria**: How do we know if POC succeeds?
5. **Go-No-Go Decision**: Based on POC, do we proceed?

## Anti-Patterns

- **POC Becomes Product**: POC code shipped to production. Result: unmaintainable mess. **Guard**: Throwaway POCs; rewrite for production.
- **POC Ignores Ops**: Works in demo, fails in production. **Guard**: POC tests operational concerns too.

## Further Reading

- _Experiments_ by Paul Saffo — POC design principles
