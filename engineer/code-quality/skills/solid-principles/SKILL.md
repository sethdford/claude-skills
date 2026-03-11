---
name: solid-principles
description: SOLID principles (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion) for object-oriented design.
---

# SOLID Principles

Five foundational principles for maintainable, extensible object-oriented design.

## Context

You are helping the engineer apply SOLID principles to their codebase. If code is provided, assess which principles are violated and suggest refactorings. Reference Robert C. Martin's work.

## Domain Context

- **Single Responsibility**: A class should have only one reason to change
- **Open/Closed**: Open for extension, closed for modification (use polymorphism)
- **Liskov Substitution**: Derived classes must be substitutable for base classes
- **Interface Segregation**: Many narrow interfaces better than one fat interface
- **Dependency Inversion**: Depend on abstractions, not concrete implementations

## Instructions

1. **Identify Responsibilities**: Does the class have more than one reason to change? If yes, extract to separate class
2. **Check Inheritance**: Can a subclass substitute for its parent without breaking callers? If not, refactor hierarchy
3. **Review Interfaces**: Are clients forced to depend on methods they don't use? If yes, split the interface
4. **Examine Dependencies**: Does the class directly instantiate its dependencies? If yes, inject them instead
5. **Look for Extensions**: Can you add new behavior without modifying existing classes? If not, apply Open/Closed
6. **Validate Contracts**: Do subclasses strengthen preconditions or weaken postconditions? (Liskov violation)
7. **Measure Cohesion**: Do all methods in a class operate on the same data? Low cohesion signals multiple responsibilities

## Anti-Patterns

- Creating a "God Object" utility class with 50 static methods; violates Single Responsibility and makes testing impossible
- Inheriting from a class just to reuse a method; violates Liskov Substitution (composition over inheritance)
- Building interfaces with 10+ methods; forces clients to implement/mock methods they don't need (Interface Segregation)
- Instantiating dependencies directly in constructors; tightly couples classes and makes mocking impossible in tests
- Applying SOLID religiously to simple scripts; over-engineering creates unnecessary indirection (YAGNI)

## Further Reading

- Robert C. Martin, _Clean Code_ and _Clean Architecture_
- Michael Feathers, _Working Effectively with Legacy Code_
- Gang of Four, _Design Patterns: Elements of Reusable Object-Oriented Software_
