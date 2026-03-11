---
name: functional-patterns
description: Higher-order functions, composition, monads, immutability, and functional programming idioms.
---

# Functional Patterns

Using functional programming principles for clearer, more maintainable code.

## Context

You are using functional patterns. Understand functional principles and idioms.

## Domain Context

- **Pure Functions**: No side effects; same input → same output
- **Composition**: Build complex functions from simple ones
- **Higher-Order**: Functions taking/returning functions
- **Immutability**: Data doesn't change; create new versions instead
- **Monads**: Pattern for handling effects (Maybe, Either, IO)

## Instructions

1. **Prefer Pure Functions**: Write functions without side effects
2. **Compose Functions**: Chain simple functions together
3. **Use Higher-Order**: Map, filter, fold; powerful abstractions
4. **Embrace Immutability**: Don't mutate; create new values
5. **Handle Effects**: Use monads or similar for side effects
6. **Test Easily**: Pure functions are trivial to test

## Anti-Patterns

- Treating FP as dogma; some problems need mutation
- Immutability everywhere killing performance; profile before pessimizing
- Monads without understanding; they're useful but not required
- Chaining operations so deeply it's unreadable; readability matters
- Avoiding mutation for simple local data; FP isn't a religion

## Further Reading

- Richard Bird & Philip Wadler, _Introduction to Functional Programming_
- Evan Czaplicki, _Elm guide_ (great FP introduction)
- Brian Lonsdorf, _Mostly Adequate Guide to FP_
