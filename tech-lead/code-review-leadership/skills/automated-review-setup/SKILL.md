---
name: automated-review-setup
description: Set up automated code review tools (linters, SAST, dependency scanning) to reduce manual review burden. Use when configuring CI/CD toolchains.
---

# Automated Review Setup

Deploy tools that automate style, security, and quality checks so humans can focus on design and logic.

## Context

You are helping a tech lead configure automated review tooling. If you have language/framework specifics or known pain points, use them.

## Domain Context

- Research: automated tooling catches 60-70% of style and security issues faster than human review
- High-performing teams (Forsgren et al.): automate what you can; humans review design, not formatting
- Tool proliferation is a risk: too many tools create overhead and false positives

Key principles:

1. **Automate the tedious**: Style, formatting, dependency audits—these have obvious correct answers
2. **Humans review the hard stuff**: Design patterns, API contracts, architectural decisions
3. **Signal-to-noise matters**: Tools with high false-positive rates get disabled. Keep tools tuned to your codebase

## Instructions

1. **Choose core tools by language**:
   - Linting: ESLint (JS), pylint (Python), RustFmt (Rust), etc.
   - Formatting: Prettier, black, rustfmt (auto-apply if possible)
   - Testing: Run test suite, check coverage
   - Security: Snyk, OWASP Dependency Check, or language-native tools
   - SAST: SonarQube, CodeQL, or native language tools

2. **Configure autofix**: Format automatically (no human decision), fail linter errors (require human fix)

3. **Add PR automation**: Auto-comment on failures with actionable messages and links to docs

4. **Set up for local development**: Developers should run tools locally before pushing (pre-commit hooks or pre-push)

5. **Don't over-instrument**: More tools = slower CI and more noise. Start with 3-4 core tools; add more only if solving a real problem

6. **Measure tool accuracy**: Track false positives (tool failed, PR approved anyway). If > 30%, tool is miscalibrated or unnecessary

Example minimal setup:

```
Stage 1 (lint, < 2min): Linter, formatter, secrets scan
Stage 2 (test, < 10min): Unit tests, coverage check
Stage 3 (security, < 5min): Dependency audit, SAST
→ All must pass to enable merging
```

## Anti-Patterns

- **Too many tools**: LLMs sometimes recommend 10+ different tools. This creates slow CI and alert fatigue. Focus on the 3-4 that catch real problems
- **Tools that require human interpretation**: "Code review readiness score of 72/100" is vague. Use tools with clear pass/fail criteria
- **Not testing tools against your codebase**: Tools configured generically might fail on your code baseline. Always test tools on main before enforcing
- **Disabling tools instead of fixing code**: Teams that keep disabling tool failures train bad habits. If a tool keeps failing, investigate if the tool is wrong or the code is

## Further Reading

- Martin Fowler's "Continuous Integration" blog: excellent on automation in CI pipelines.
- Kim, Gene et al. "The DevOps Handbook." IT Revolution Press, 2016. Chapter on deployment pipeline design.
- OWASP Top 10: guidance on security tooling and what to scan for.
