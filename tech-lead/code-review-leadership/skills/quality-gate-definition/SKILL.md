---
name: quality-gate-definition
description: Define automated quality gates that enforce standards without manual review. Use when setting up CI/CD checks and blocking criteria.
---

# Quality Gate Definition

Build automated gates that catch issues before review, enabling faster async review cycles.

## Context

You are helping a tech lead design CI/CD quality gates. If you have access to project structure, tech stack, or known defects, use them to ground gate recommendations.

## Domain Context

- SonarQube and similar tools: automated quality gates catch 60-70% of defects that code review would catch, but faster
- CI/CD best practice: gates should fail fast (< 5 minutes) or they get bypassed
- Research: teams that use automated gates spend 30-40% less time in code review

Key principles:

1. **Fail fast or fail never**: Gates that take 20 minutes are skipped. Keep gates under 5 minutes
2. **Be specific, not broad**: "Code quality" is vague. "Cyclomatic complexity > 10" is actionable
3. **Gates should be gating, not advisory**: If a gate fails, the PR cannot merge. Advisory warnings (yellow builds) get ignored
4. **Gates evolve with team maturity**: A junior team might allow 80% coverage; a mature team might enforce 90%

## Instructions

1. **Define gate categories**:
   - Style (linter, formatter) — autofix or block
   - Testing (coverage, execution) — block if below threshold
   - Performance (build time, artifact size) — block if regresses > 10%
   - Security (dependency audit, secrets scan) — block on high severity
   - Architecture (complexity, dependency rules) — block on violations
   - Accessibility (for web/UI) — block on critical issues

2. **For each gate, set thresholds**:
   - Coverage: block if drops below 80% (or your team standard)
   - Linter: block on any errors (warnings can be advisory)
   - Build time: block if > 10% slower than baseline
   - Artifact size: block if > 5% larger
   - Security: block on high/critical, warn on medium
   - Complexity: block if cyclomatic complexity > 10 or > 3 nesting depth

3. **Create bypass criteria**: Emergency/hotfix PRs can bypass some gates if explicitly labeled. Document which gates can bypass and who approves

4. **Test the gates**: Run gates against your main branch. If they fail there, they're broken. Fix gates before enforcing

5. **Make gates visible**: Show results in PR comments, not just build status. Developers should see exactly why a gate failed

6. **Measure false positives**: If more than 20% of gate failures are overridden, the gate is miscalibrated. Lower threshold or remove gate

Example gate configuration:

```
Linter: block on errors, warn on > 5 warnings
Coverage: block if drops > 2%, advisory if drops 0-2%
Build time: advisory if > 10% slower, block if > 30% slower
Secrets: block on any leaked secrets
Dependencies: block on high/critical CVEs
Performance: advisory if bundle > 1MB, block if > 2MB
```

## Anti-Patterns

- **Gates that take forever**: LLMs sometimes recommend running full test suites, security scans, and load tests in gates. If it takes 20 minutes, developers will bypass. Keep gates fast
- **Gates without remediation paths**: "Code quality too low" without saying how to fix it is frustrating. Always include "why" and "how to fix" in gate failure messages
- **Too many gates**: Teams with 15+ gates have slower CI and more bypasses. Focus on gates that catch high-impact issues (security, critical bugs, performance)
- **Gates that don't match reality**: LLMs sometimes recommend coverage thresholds your team can't achieve with existing code. Start with current reality, then increase

## Further Reading

- SonarQube documentation: comprehensive guide to quality gates and thresholds.
- Kim, Gene et al. "The DevOps Handbook." IT Revolution Press, 2016. Chapter on continuous delivery practices.
- Forsgren, Nicole et al. "Accelerate." IT Revolution Press, 2018. Chapter on deployment frequency and automation.
