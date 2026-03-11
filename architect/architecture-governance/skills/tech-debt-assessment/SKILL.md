---
name: tech-debt-assessment
description: Measure, prioritize, and address technical debt. Classify debt by impact and effort. Build paydown roadmap. Use when evaluating system health or planning refactoring.
---

# Tech Debt Assessment

Systematically measure technical debt, prioritize paydown, and track progress.

## Context

You are assessing technical debt in the system. Quantify impact (velocity reduction, risk increase), estimate effort to fix, prioritize based on ROI. Read code, metrics, team feedback.

## Domain Context

Based on technical debt frameworks (Steve McConnell, Martin Fowler):

- **Types of Debt**: Deliberate (knowingly cut corners for speed), accidental (poor design decisions), negligent (avoidable bad practices)
- **Impact**: Slows feature delivery (velocity decrease), increases bugs (quality risk), complicates future changes
- **Interest Payments**: Cost to maintain bad code; time spent working around it; bugs from complexity
- **Paydown**: Refactoring, rewriting, deprecating; costs time/resources upfront but reduces future interest

## Instructions

1. **Catalog Debt Items**: Interview team: "What slows us down?" Common themes: hard-to-test code, tangled dependencies, missing documentation, outdated libraries.

2. **Quantify Impact**: For each debt item, how much does it slow velocity? Example: "Test coverage < 30% makes refactoring 3x slower". Measure days/quarter lost to debt.

3. **Estimate Paydown Effort**: How long to fix? Refactor module: 2 weeks. Rewrite component: 1 month. Replace library: 3 days. Be realistic; add 50% buffer.

4. **Calculate ROI**: Paydown cost vs interest savings. Refactor for 2 weeks (80 hours) to save 5 hours/quarter in reduced bugs and faster changes. Payoff: ~16 quarters (4 years).

5. **Prioritize**: High impact + low effort = do first. High impact + high effort = plan for next quarter. Low impact = defer or accept. Build paydown roadmap: 20% of sprint capacity for debt.

## Anti-Patterns

- **Debt Without Metrics**: "Our code is messy" without quantifying impact. Result: hard to justify paydown. **Guard**: Quantify slowness; track velocity impact.
- **Paydown Without Benefit**: Refactor for refactoring's sake. Result: effort spent, velocity unchanged. **Guard**: Only pay down debt with measurable benefit (fewer bugs, faster changes).
- **Ignoring Debt Accumulation**: Always add features, never refactor. Result: exponential slowdown. **Guard**: Allocate 20% of capacity for debt; enforce discipline.
- **Wrong Prioritization**: Pay down low-impact debt first. Result: effort wasted, high-impact debt still blocking. **Guard**: Prioritize by impact × frequency, not just preference.

## Further Reading

- _Working Effectively with Legacy Code_ by Michael Feathers — managing technical debt
- _Refactoring_ by Martin Fowler — improving design of existing code
- _The Pragmatic Programmer_ by David Thomas and Andrew Hunt — sustainable pace and debt
