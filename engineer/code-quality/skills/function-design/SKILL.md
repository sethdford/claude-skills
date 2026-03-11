---
name: function-design
description: Designing pure functions with single purpose, minimal parameters, clear side effects, and high cohesion.
---

# Function Design

Principles for writing functions that are easy to understand, test, and maintain.

## Context

You are helping the engineer design or refactor functions. If code is provided, assess whether functions follow cohesion, purity, and responsibility principles. A good function is a unit of composition.

## Domain Context

- **Single Purpose**: One reason to change; extract if doing multiple things
- **Pure Functions**: Same input always yields same output; no hidden dependencies
- **Minimal Parameters**: More parameters = harder to test and understand; aim for 0-3
- **High Cohesion**: All statements relate to the function's purpose
- **Clear Side Effects**: Document and minimize; prefer immutability

## Instructions

1. **Identify Purpose**: Can you explain the function in one sentence? If not, it's doing too much
2. **Count Parameters**: Refactor if > 3; use Parameter Object or method extraction
3. **Check for Side Effects**: Does it modify global state? Database? Output? Document explicitly
4. **Verify Purity**: Same inputs = same outputs? If not, document the dependency
5. **Measure Cohesion**: Do all lines support the stated purpose? If not, extract
6. **Review Return Value**: Does it return useful information or just status? Prefer returning data
7. **Check Error Handling**: Are failure cases explicit? Return errors, don't swallow silently
8. **Test Independence**: Can you test this function without mocks or fixtures? If not, refactor

## Anti-Patterns

- Functions that are "almost pure" but read global config; hidden dependencies break reasoning about behavior
- Functions that return status codes (0 = success, -1 = error) instead of explicit exceptions or Result types; callers forget error checks
- Functions with side effects buried inside the logic (logging, database writes); this makes testing impossible
- Very long parameter lists defended with "the function needs all this data"; usually signals missing domain object
- Accepting objects and only reading one field; tightly couples function to the object's structure

## Further Reading

- Robert C. Martin, _Clean Code_, Chapter 3 (Functions)
- Kent Beck, _Smalltalk Best Practice Patterns_, Pattern 19 (Method Object)
- John Hughes, "Why Functional Programming Matters"
