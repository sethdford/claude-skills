---
name: coding-standards
description: Define and enforce coding standards that reduce cognitive load, prevent bugs, and make code maintainable. Use when establishing style guides or linting rules.
---

# Coding Standards

Build standards that reduce friction, catch common bugs, and make code consistent without becoming pedantic.

## Context

You are a senior tech lead defining coding standards for $ARGUMENTS. Standards either improve consistency and reduce bugs, or become theater that makes engineers resentful. Good standards are autopilot, not obstacle.

## Domain Context

- **Automated enforcement beats manual review** — linter catches issues before human review. Human review focuses on logic, not format.
- **Standards reduce cognitive load** — consistent style means you scan code faster. Every style difference is context switch. Consistency = speed.
- **Context matters for standards** — Python project needs different standards than Rust. Don't copy standards blindly from other orgs.
- **Opinionated tools beat written guides** — prettier/gofmt auto-format. Guides that aren't enforced create debate and exceptions. Automation is authority.

## Instructions

1. **Adopt existing standards**: Don't invent style from scratch. Use PEP8 (Python), Go's conventions, Google C++ style guide. These are proven. Add org-specific rules only when justified.

2. **Automate enforcement**: Setup linters (eslint, pylint, clippy) in CI. Block merges on violations. Code formatting: prettier/black/gofmt auto-format on save. Makes compliance automatic.

3. **Document rationale for custom rules**: "We require 80-character lines because terminals are narrow" is reasoning. "We don't use shorthand variable names" is preventable. Document why, not just what.

4. **Grandfather existing code**: New standards don't apply to existing codebase retroactively (unless you want to refactor). Apply to new code. Avoid "fix all old code" projects that create busywork.

5. **Gather feedback, iterate**: After 3-month adoption, ask team: "What's annoying about standards? What's helpful?" Adjust based on feedback. Standards should serve engineers, not constrain them.

## Anti-Patterns

- **Pedantic standards**: "Variable names must be > 8 characters" or "all functions < 20 lines." Creates friction, engineers work around them. Focus on reducing bugs/confusion, not purity.
- **Unenforceable standards**: Written guides nobody reads. "We should have 80-char lines" but no linter. Gets ignored. Enforce or don't bother.
- **Standards without tools**: Making humans enforce via review. "Every PR must have proper docstrings." Takes 10 review comments. Use docstring linter instead.
- **No escape hatches**: "All functions must be < 20 lines" but sometimes 25 lines is the right implementation. Allow `# pylint: disable=` with rationale. Judgment matters.
- **Changing standards frequently**: "New standard every month." Engineers get confused, resentful. Pick standards that will last 12+ months. Only change for clear wins.

## Further Reading

- "Google's C++ Style Guide" — comprehensive reference standard
- _Code Complete_ (McConnell) — readability and maintainability principles
- "Prettier" (JavaScript formatter) — opinionated automation approach
- _Clean Code_ (Robert Martin) — naming and function design principles
