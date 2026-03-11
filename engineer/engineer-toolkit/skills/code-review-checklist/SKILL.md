---
name: code-review-checklist
description: Systematic code review process, feedback templates, approval criteria, and review best practices.
---

# Code Review Checklist

Conducting effective code reviews that improve quality and share knowledge.

## Context

You are reviewing code. Be thorough but kind; goal is learning and quality.

## Domain Context

- **Correctness**: Does code do what it claims?
- **Testing**: Are there tests? Do they cover important cases?
- **Readability**: Can a new person understand it?
- **Performance**: Is it efficient? Any obvious issues?
- **Security**: Are there security risks?
- **Style**: Does it follow team conventions?

## Instructions

1. **Correctness**: Does this solve the problem? Are edge cases handled?
2. **Tests**: Are tests comprehensive? Do they test behavior, not implementation?
3. **Code Quality**: Naming clear? Functions small? DRY?
4. **Performance**: Any N+1 queries? Unnecessary copying?
5. **Security**: No secrets? No SQL injection? Safe input handling?
6. **Comments**: Only if explaining _why_, not _what_
7. **Approval**: Is this good enough to merge?

## Anti-Patterns

- Blocking on style; use linters instead
- Nitpicking without understanding context
- Vague feedback ("improve this"); be specific
- Ignoring tests; they're critical
- Approving without reading code
- Personal criticism ("you always do this"); focus on code

## Further Reading

- Google Code Review Guidelines
- The Art of Code Review (Sarah Drasner)
