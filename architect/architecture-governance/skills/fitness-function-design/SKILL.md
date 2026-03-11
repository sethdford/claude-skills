---
name: fitness-function-design
description: Design metrics that measure architecture health (coupling, modularity, scalability). Automate fitness function checks in CI/CD. Use when establishing quality gates or measuring architectural degradation.
---

# Fitness Function Design

Design quantifiable metrics to measure architecture health and automatically enforce quality standards.

## Context

You are designing fitness functions to measure architectural quality. Create metrics for coupling, modularity, scalability, performance. Automate checks in CI/CD for continuous feedback.

## Domain Context

Based on evolutionary architecture and fitness function research (Thoughtworks):

- **Coupling Metrics**: Layer violations, cyclic dependencies, test isolation
- **Modularity Metrics**: Module fan-in/fan-out, cohesion, abstract instability
- **Scalability Metrics**: Throughput (RPS), latency (p95, p99), resource utilization
- **Security Metrics**: Secrets in code, dependency vulnerabilities, known security patterns
- **Code Quality Metrics**: Complexity (cyclomatic), duplication, test coverage

## Instructions

1. **Identify Key Quality Attributes**: What matters most? Scalability? Security? Testability? Maintainability? Pick 3-4.

2. **Define Metrics for Each Attribute**: Scalability: p99 latency < 200ms, peak RPS capacity. Security: zero secrets in code, all dependencies scanned. Testability: > 80% test coverage, no untestable dependencies.

3. **Set Thresholds**: Below threshold: pass. Above: fail (blocks merge). Make thresholds achievable but stretch. Too strict: teams bypass. Too loose: no effect.

4. **Automate Checks**: Integrate into CI/CD. Run on every PR. Parse test coverage reports, dependency scanners, performance benchmarks. Fail PR if fitness functions breach.

5. **Monitor and Adjust**: Track metrics over time. Are they trending right? Do developers understand why they matter? Adjust thresholds based on feedback and organizational priorities.

## Anti-Patterns

- **Too Many Fitness Functions**: 50 metrics in CI/CD. Result: long builds, false positives, ignored. **Guard**: 5-10 core metrics max. Automate what matters; remove noise.
- **Fitness Functions Without Context**: "Cyclomatic complexity > 10 fails". Developer doesn't understand why. Result: frustrated, rules bypassed. **Guard**: Document rationale; train teams; explain tradeoffs.
- **Static Thresholds**: Set once, never changed. Organization evolves, thresholds stale. Result: metrics become irrelevant. **Guard**: Review quarterly; adjust based on trends and priorities.
- **Metrics Without Action**: Fitness functions fail but no one addresses. Result: technical debt accumulates. **Guard**: Failed checks require action; track and fix root causes.

## Further Reading

- _Evolutionary Architecture_ by Rebecca Parsons, Neal Ford, Patrick Kua — fitness function concepts
- _Building Microservices_ by Sam Newman — quality metrics for distributed systems
- _Accelerate_ by Nicole Forsgren — DORA metrics for deployment performance
