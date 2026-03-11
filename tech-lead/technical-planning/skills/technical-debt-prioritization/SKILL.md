---
name: technical-debt-prioritization
description: Evaluate and prioritize technical debt to balance feature velocity with system health. Use when deciding what debt to address in upcoming sprints.
---

# Technical Debt Prioritization

Systematically evaluate debt and decide which to address based on risk, velocity impact, and cost.

## Context

You are helping a tech lead create a technical debt strategy and prioritization framework. If the user has a backlog of debt items or known pain points, use them to ground the analysis.

## Domain Context

- Ward Cunningham (originator of "technical debt" metaphor): debt is a tool; the problem is _unmanaged_ debt
- Larson: paying down debt has zero visible customer value, so it must compete fairly with features. Measure its impact on velocity
- Research shows codebases with high debt experience 40-60% slower development velocity; the paydown usually takes 1-3 quarters to show ROI

Key principles:

1. **Debt is not optional**: All codebases accumulate debt. The question is whether you manage it or let it compound
2. **Debt is a velocity tax**: High-debt systems have higher bug rates, slower deployment cycles, and longer onboarding. Model the cost
3. **Some debt is worth keeping**: Not all debt should be paid. Pay debt that blocks future work or creates unacceptable risk

## Instructions

1. **Create a debt inventory**: List all known technical debt. Ask engineers "what do you wish we'd refactored?" Examples:
   - Monolithic service that's hard to test and deploy (architecture debt)
   - Test suite that's slow (development velocity debt)
   - Documentation that's outdated (onboarding debt)
   - Security practices that are ad-hoc (compliance risk debt)
   - Dependencies that are years out of date (security/support debt)

2. **For each debt item, estimate impact on velocity**:
   - **High**: This debt directly slows down feature work (slow tests, hard to deploy, unclear architecture). Development velocity is 20-30% lower because of it
   - **Medium**: This debt slows development indirectly (missing monitoring, unclear design patterns). Velocity impact ~10%
   - **Low**: This debt doesn't materially impact velocity (minor code smell, one-off workaround)

3. **Estimate cost to pay down**: How much effort to fix? S (1 sprint), M (2-3 sprints), L (4+ sprints)?

4. **Calculate payoff ROI**:
   - Example: slow test suite (high impact, adds 2 hours per developer per day) taking 1 sprint to fix
   - Team of 5: 5 × 5 days × 2 hours = 50 hours saved per sprint
   - If velocity is ~40 points/sprint, that's ~1.25 point-sprints saved per sprint going forward
   - Payoff happens in: 1 sprint (cost) ÷ 0.5 springs/sprint (benefit) = 2 sprints total

5. **Prioritize by impact and payoff**:
   - **Priority 1 (immediate)**: High impact, payoff < 3 sprints
   - **Priority 2 (next quarter)**: Medium impact, payoff < 4 sprints, or high impact that enables future roadmap items
   - **Priority 3 (nice-to-have)**: Low impact or long payoff
   - **Accept**: Some debt is too expensive to fix right now; document why you're keeping it

6. **Build into roadmap**: Reserve 20-30% of capacity for debt. Use technical-roadmap skill to decide when/how to address priority-1 debt

7. **Measure before and after**: After paying down high-impact debt, re-measure velocity. Did it improve? This data is crucial for future decisions

Example format:

```
| Debt | Impact | Velocity Cost | Fix Cost | Payoff | Priority | Owner |
|------|--------|---------------|----------|--------|----------|-------|
| Slow test suite (5 min) | High | 2 hrs/eng/day | 1 sprint | 2 sprints | 1 | QA Lead |
| Monolithic service | High | 15% velocity loss | 4 sprints | 6 sprints | 2 | Backend Lead |
| Outdated docs | Medium | 5 hrs/new eng | 2 days | ongoing | 3 | Tech Lead |
```

## Anti-Patterns

- **Debt without impact modeling**: LLMs sometimes suggest paying down debt because "the code is messy" without measuring velocity impact. Bad debt: your codebase is fine, doesn't need refactoring. Ignore it.
- **Ignoring the "why we kept it" question**: Most debt exists because it was the right trade-off at the time. If you don't understand why it was acceptable, you can't decide if it's still acceptable.
- **Debt payoff that never shows ROI**: Some debt takes 2+ years to pay off (migrating databases, replacing core systems). These are risky bets; make sure the team understands the commitment.
- **Treating technical debt as a team skill issue**: LLMs sometimes frame debt as "engineers didn't do good work." Debt is a _business decision_, not a quality issue. Own it as a tech lead: you made trade-offs, now evaluate if they're still worth it.

## Further Reading

- Cunningham, Ward. "The WyCash Portfolio Management System." 1992 (original "technical debt" paper).
- Larson, Will. "An Elegant Puzzle." Chapter on technical debt and velocity.
- McConnell, Steve. "Code Complete: A Practical Handbook of Software Construction." Microsoft Press, 2004. Chapter on construction practices and technical debt.
