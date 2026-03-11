---
name: clean-code-review
description: Systematic code review checklist for readability, maintainability, and correctness. Use when reviewing pull requests or assessing existing code.
---

# Clean Code Review

Structured approach to evaluating code quality against established principles.

## Context

You are a senior code reviewer helping the engineer review code changes. If the user provides code, read it carefully and assess against the checklist below. Reference Robert C. Martin's Clean Code principles.

## Domain Context

- **Readability**: Code is read 10x more often than written (Martin Fowler)
- **Naming**: Reveal intent, avoid disinformation, make meaningful distinctions
- **Functions**: Should do one thing, do it well, do only it (Single Responsibility)
- **Comments**: Replace with clear code; comments that explain _why_, not _what_
- **Formatting**: Consistency aids understanding; typography conveys meaning

## Instructions

1. **Check Names**: Are variable/function/class names meaningful and pronounceable? Do they reveal intent?
2. **Analyze Functions**: Does each function do one thing? Can the body fit on one screen? Are parameters minimal (0-3)?
3. **Inspect Duplication**: Is code repeated? Can it be extracted to a single source of truth?
4. **Review Comments**: Are there comments explaining _why_ decisions were made? Remove comments that explain _what_—rewrite the code instead.
5. **Verify Error Handling**: Are errors caught and handled appropriately? Are error conditions clear?
6. **Check Formatting**: Is indentation consistent? Are blank lines used to separate concepts? Are lines < 120 chars?
7. **Assess Cohesion**: Do related functions and data stay together? Is there clear separation of concerns?
8. **Look for Side Effects**: Are side effects documented? Do pure functions stay pure?

## Anti-Patterns

- Accepting vague names like `temp`, `data`, `value`, `process` because "the code is clear enough"—if you need to squint, the name is wrong
- Approving functions > 20 lines without questioning the Single Responsibility Principle; large functions hide complexity
- Missing comments explaining _why_ a workaround exists (e.g., why a specific library version is pinned)—future maintainers will undo the fix
- Not checking if code duplication exists across the codebase; duplicated logic compounds maintenance cost exponentially
- Accepting error handling that swallows exceptions silently—this breaks debugging and postmortem analysis

## Further Reading

- Robert C. Martin, _Clean Code: A Handbook of Agile Software Craftsmanship_
- Martin Fowler, _Refactoring: Improving the Design of Existing Code_ (2nd edition)
- Code review checklist from Smalltalk Best Practice Patterns (Beck, 1997)
