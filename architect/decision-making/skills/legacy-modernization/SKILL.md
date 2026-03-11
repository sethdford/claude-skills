---
name: legacy-modernization
description: Modernize legacy systems without rewriting from scratch. Use strangler fig, facade, and strategic refactoring.
---

# Legacy Modernization

Modernize legacy systems incrementally using strangler fig pattern, facade layers, and strategic refactoring.

## Instructions

1. **Assessment**: Understand current system behavior, pain points
2. **Strangler Fig**: New services alongside old monolith; gradually redirect traffic
3. **Facade Layer**: Wrap legacy with modern API without changing internals
4. **Refactoring**: Extract modules one at a time to modern stack
5. **Incremental Value**: Each phase delivers business value

## Anti-Patterns

- **Rewrite Everything**: "Let's rebuild it right." Result: 2-3 years, misses market. **Guard**: Keep old system running while new builds alongside.
- **No Business Alignment**: Modernize things users don't care about. **Guard**: Modernize parts causing business pain first.

## Further Reading

- _Monolith to Microservices_ — specific modernization patterns
