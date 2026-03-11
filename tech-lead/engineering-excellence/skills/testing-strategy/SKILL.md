---
name: testing-strategy
description: Design testing strategies (unit, integration, end-to-end, performance) that catch bugs without creating bottlenecks. Use when scaling testing or improving release confidence.
---

# Testing Strategy

Build testing pyramids that catch bugs early without slowing down development.

## Context

You are a senior tech lead establishing testing strategy for $ARGUMENTS. Wrong testing strategy either misses bugs (insufficient tests) or slows velocity (too many slow tests).

## Domain Context

- **Testing pyramid**: Many unit tests (fast, isolated), fewer integration tests (slower, multiple components), few E2E tests (slowest, full system). Inverted pyramid is expensive and slow.
- **Test ROI varies** — unit test finds bug 100% faster than production (milliseconds vs hours). E2E test finds bugs unit tests miss but takes 30 seconds per run.
- **Flaky tests are worse than no tests** — if test fails randomly, team ignores it. Flakiness kills trust. Better to have 10 reliable tests than 50 flaky ones.
- **Test maintenance is real cost** — every test written is code to maintain. As codebase changes, tests break. Test code debt is real debt.

## Instructions

1. **Define pyramid**: Aim for 70% unit tests (fast), 20% integration tests (moderate), 10% E2E tests (slow). Adjust based on system complexity and team size.

2. **Establish quality gates**: "All PRs must pass unit tests (5 min) before code review. Integration tests run in background (20 min), block merge if fail. E2E tests run on main before deploy."

3. **Eliminate flakiness aggressively**: Flaky test found? Invest in fix immediately (same day if possible). If unfixable, remove. Flakiness is trust killer.

4. **Track test metrics**: Coverage (aim for 70%+), execution time, pass rate. If test execution time grows beyond 10 minutes, reduce test scope or parallelize.

5. **Rotate test maintenance**: Don't leave test ownership to one person. All engineers should understand and maintain tests. Distribute knowledge.

## Anti-Patterns

- **Test pyramid inverted**: Tons of slow E2E tests, few unit tests. Feedback loop is 30+ minutes. Slow feedback kills development speed. Invest in unit/integration tests.
- **Coverage obsession**: "We need 95% coverage." But 95% coverage with bad tests (don't actually assert anything) is useless. Aim for meaningful coverage (critical paths) not absolute number.
- **Flaky tests ignored**: Flaky test fails randomly, team ignores it ("it's just flaky"). Eventually nobody trusts any tests. Fix or remove flaky tests immediately.
- **No test maintenance**: Writing tests, then ignoring them. Codebase changes, tests rot, don't run anymore. Plan for ongoing maintenance.
- **Testing as afterthought**: Writing all code, then writing tests at end. Hard to test, creates bad test design. Write tests as you go (TDD or at least test-alongside).

## Further Reading

- "Test Pyramid" (Martin Fowler) — testing strategy overview
- _Xunit Test Patterns_ (Meszaros) — test design and maintenance
- "Flaky Tests" (Google Testing Blog) — diagnosing and fixing flakiness
- _Growing Object-Oriented Software, Guided by Tests_ (Freeman & Pryce) — TDD practices
