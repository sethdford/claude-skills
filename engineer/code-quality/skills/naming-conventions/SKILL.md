---
name: naming-conventions
description: Choosing meaningful, pronounceable names that reveal intent for functions, variables, classes, and modules.
---

# Naming Conventions

Art and science of selecting names that reveal intent and reduce cognitive load.

## Context

You are helping the engineer improve naming across the codebase. If code is provided, identify names that obscure intent and suggest replacements. Names are the primary interface between code and readers.

## Domain Context

- **Reveal Intent**: A good name answers the _why_ without requiring additional context
- **Avoid Disinformation**: Don't use names that mislead (e.g., `accounts` for a single account)
- **Make Meaningful Distinctions**: `a1`, `a2`, `a3` are meaningless; `source`, `target`, `result` are distinct
- **Pronounceability**: Names you can say aloud are easier to discuss and remember
- **Searchability**: Use searchable names; single-letter variables make grep useless

## Instructions

1. **Variables**: Use full words; `userAccount` not `acc`; `isActive` not `a`
2. **Functions**: Use verb phrases; `getUserById()`, `calculateInterest()`, `validateEmail()`
3. **Classes**: Use noun phrases; `User`, `PaymentProcessor`, `ValidationRule`
4. **Constants**: Use SCREAMING_SNAKE_CASE; `MAX_RETRIES`, `DEFAULT_TIMEOUT`
5. **Boolean Variables**: Prefix with `is`, `has`, `should`; `isValid`, `hasPermission`, `shouldRetry`
6. **Avoid Abbreviations**: Unless ubiquitous (HTTP, URL); `currentUser` not `currUsr`
7. **Scope Rule**: Shorter names for tiny scopes (loop counters), longer for larger scopes
8. **Domain Language**: Use terms from the business domain; `invoice` not `doc`

## Anti-Patterns

- Using vague names ("manager", "processor", "handler") because they sound professional; these obscure actual intent
- Abbreviating names to save keystrokes (IDEs do autocomplete anyway); `idx` instead of `index` hurts readability
- Encoding type information in names (Hungarian notation `iCount`, `strName`); type systems exist for a reason
- Using single-letter variables outside loop counters; `for (int i = 0; ...)` is fine, but `e = x + y` is not
- Naming by external context rather than responsibility; `getData()` in a UserService is vague; `getUserAccount()` is clear

## Further Reading

- Robert C. Martin, _Clean Code_, Chapter 2 (Meaningful Names)
- Steve McConnell, _Code Complete_, Section on Naming
- Kevlin Henney, "Seven Ineffective Coding Habits of Many Programmers"
