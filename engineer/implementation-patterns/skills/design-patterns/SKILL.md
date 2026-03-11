---
name: design-patterns
description: Gang of Four patterns (Creational, Structural, Behavioral) and when to apply them.
---

# Design Patterns

Proven solutions to recurring design problems.

## Context

You are selecting a design pattern for a problem. Understand the tradeoffs of each.

## Domain Context

- **Creational**: How to create objects? (Singleton, Factory, Builder, Prototype)
- **Structural**: How to compose objects? (Adapter, Bridge, Facade, Proxy, Decorator)
- **Behavioral**: How do objects interact? (Observer, Strategy, State, Command, Iterator)

## Instructions

1. **Identify Problem**: What design issue are you facing?
2. **Map to Pattern**: Which pattern solves this?
3. **Understand Intent**: Why does this pattern work?
4. **Consider Tradeoffs**: Complexity, flexibility, testability?
5. **Implement**: Code the pattern; don't memorize, understand
6. **Refine**: Adapt the pattern to your context

## Anti-Patterns

- Applying patterns everywhere (pattern obsession); YAGNI
- Stacking patterns (Factory + Builder + Proxy); complexity without benefit
- Not understanding the pattern before using it; cargo cult programming
- Choosing pattern based on name not problem; same name, different intent
- Over-engineering simple problems with patterns; sometimes direct code is clearer

## Further Reading

- Gang of Four, _Design Patterns_ (the bible)
- Eric Freeman & Elisabeth Freeman, _Head First Design Patterns_
- Refactoring.Guru Design Patterns online
