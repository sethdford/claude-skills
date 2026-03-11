---
name: branching-strategy
description: Design branching strategies (git flow, trunk-based development, etc.) that support parallel work while maintaining stability. Use when establishing version control discipline or managing deployment complexity.
---

# Branching Strategy

Choose and communicate branching strategies that enable teams to work in parallel without creating merge chaos or deployment risk.

## Context

You are a senior tech lead designing branching strategy for $ARGUMENTS. Poor branching leads to merge conflicts, deployment surprises, and long-lived branches that carry stale code and integration risk.

## Domain Context

- **Trunk-based development** — main branch is always releasable. Features ship behind feature flags. Reduces merge complexity and keeps code fresh.
- **Git flow** — separate release branches allow hotfixes and parallel releases. More complex, suited for multi-version products.
- **Branch age matters** — branches older than 3-4 days start diverging from main. Stale branches are expensive to merge. Keep branches short-lived.
- **Merge cost compounds** — each branch living longer adds teammates working on dependent features. Two 1-day branches = 1 merge. Two 5-day branches = 3+ merges. Keep them small.

## Instructions

1. **Choose strategy based on product model**: Single release train and feature flags? Use trunk-based development. Multiple live versions? Use git flow with maintenance branches. Document why you chose this, not just what it is.

2. **Define branch naming convention**: Feature branches from main: `feature/description-kebab-case`. Release branches: `release/v1.2.3`. Hotfix branches: `hotfix/issue-description`. Convention prevents confusion and enables automation.

3. **Set merge requirements**: Main branch protection rules. Require PR reviews, passing tests, no conflicts. Automate enforcement. Prevent "accidentally merged to main."

4. **Define long-running branch policy**: Branches live max 3-4 days. After that, rebase on main daily to stay fresh. If branch needs 2+ weeks, it's probably not a branch, it's a sub-project that needs different management.

5. **Communicate and enforce**: Strategy is only useful if everyone follows it. Document in CONTRIBUTING.md. Automate enforcement where possible (branch naming, PR templates). Onboard new team members explicitly.

## Anti-Patterns

- **No strategy, anarchy**: "Just commit to main" or "branches exist but nobody knows the convention." Merge conflicts and coordination chaos. Document and enforce.
- **Permanent feature branches**: 4-week branches that become stale, generate merge conflicts, and create integration surprises. Split large features into smaller ones with shorter branches.
- **Complex strategy nobody understands**: 8-part git flow that requires internal wiki just to remember. Simpler strategy executed well beats complex strategy executed poorly.
- **Strategy doesn't match team**: Small team doing hotfixes doesn't need git flow complexity. Large team shipping to production 5x daily needs trunk-based with feature flags.
- **Branching without feature flags**: If strategy requires branches, you also need feature flags to release incomplete code. Branches + no flags = bottleneck.

## Further Reading

- "A Successful Git Branching Model" (Vincent Driessen) — git flow
- "Trunk-Based Development" (Paul Hammant) — modern branching approach
- _Accelerate_ (Dora metrics) — deployment frequency and branching
- "Feature Flags" (Martin Fowler) — decoupling deployment from release
