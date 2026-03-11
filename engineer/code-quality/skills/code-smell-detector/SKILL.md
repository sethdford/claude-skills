---
name: code-smell-detector
description: Identify code smells like long methods, duplication, low cohesion, and high coupling. Use when assessing code health.
---

# Code Smell Detector

Heuristics to spot problematic code patterns that indicate deeper design issues.

## Context

You are helping the engineer identify code smells. If code is provided, scan for telltale signs of design problems. Reference Martin Fowler's Code Smell catalog.

## Domain Context

- **Code Smell**: Surface-level indicator of a deeper problem (not always a bug, but warrants investigation)
- **Long Method**: Methods > 20 lines usually violate Single Responsibility
- **Duplicated Code**: Multiple copies of similar logic = bug multiplication
- **Long Parameter List**: > 3 parameters suggests missing abstractions
- **Data Clumps**: Related data that travels together should be objects

## Instructions

1. **Long Methods**: Count lines; extract when > 20 or when logic is not immediately obvious
2. **Duplicated Code**: Scan for copy-pasted logic; consolidate to single source
3. **Long Parameter Lists**: Group > 3 related params into Parameter Object
4. **Data Clumps**: Group data fields that travel together into dedicated class
5. **Switch Statements**: Consider replacing with polymorphism (Strategy, Visitor patterns)
6. **Primitive Obsession**: Replace primitives with domain objects (Money, Date, etc.)
7. **Lazy Classes**: Remove classes that do little; consolidate with neighbors
8. **Comments**: Dense comments may indicate unclear code; refactor instead

## Anti-Patterns

- Ignoring smells because "the code works"; smells indicate maintenance problems that compound over time
- Eliminating all smells immediately; some smells are acceptable in simple utility functions (YAGNI)
- Confusing code smell with performance problem; a smell is about maintainability, not speed
- Generating code to "fix" smells rather than understanding root cause; generated code often creates more smells
- Creating abstractions based on isolated smells; wait for patterns (Rule of Three) before extracting

## Further Reading

- Martin Fowler, _Refactoring: Improving the Design of Existing Code_ (Code Smell catalog)
- Kent Beck, _Smalltalk Best Practice Patterns_
- Michael Feathers, _Working Effectively with Legacy Code_
