---
name: change-impact-analysis
description: Predict impacts of architectural changes on dependent systems. Trace dependencies, assess risk, plan rollout. Use when making major changes or analyzing blast radius.
---

# Change Impact Analysis

Systematically analyze impacts of architectural changes to predict risk and plan safe rollout.

## Context

You are analyzing impact of a major change. Trace affected systems, identify risks, plan mitigation. Read current dependency graph, deployment practices, system health metrics.

## Domain Context

Based on change management and impact analysis frameworks:

- **Direct Impact**: System directly modified. Code changes, performance changes, behavior changes.
- **Indirect Impact**: Dependent systems affected. Database schema change affects clients. Service API change affects all callers. Message format change affects consumers.
- **Risk Assessment**: What could go wrong? Cascading failures? Data loss? Performance regression? Unavailability of critical path?
- **Rollback Plan**: If change goes wrong, can you revert quickly? What data consistency issues might occur?

## Instructions

1. **Trace Dependencies**: What systems depend on the component you're changing? Use dependency graph tools (source analysis, API scanning). Interview teams.

2. **Assess Direct Impact**: For the component itself, what's changing? Behavior? Performance? Data model? How does change affect invariants, contracts, SLAs?

3. **Assess Indirect Impact**: For each dependent system, how does change affect it? Can they continue working with new interface? Will they need code changes? Testing?

4. **Calculate Risk Score**: How many systems affected? (x10 multiplier per additional system). How critical are those systems? (x5 for customer-facing, x2 for internal). Estimate blast radius.

5. **Plan Mitigation**: For high-risk changes, plan phased rollout (10% users, 50%, 100%). Parallel run (old and new simultaneously). Comprehensive testing and monitoring. Runbook for quick rollback.

## Anti-Patterns

- **Change Without Impact Analysis**: Architect makes change unilaterally. Result: breaks production, cascading failures. **Guard**: Mandatory impact analysis before major changes; design review.
- **Underestimating Blast Radius**: Assume only 1-2 systems affected. Result: surprises. **Guard**: Systematic dependency tracing; interview teams; over-estimate.
- **No Rollback Plan**: Assume change succeeds. Result: stuck if it fails. **Guard**: Practice rollbacks; measure rollback time; have detailed procedure.
- **Ignoring Monitoring**: Make change, wait for problems to surface. Result: incidents. **Guard**: Comprehensive monitoring; metrics for correctness, performance, errors; alert on anomalies.

## Further Reading

- _The Phoenix Project_ by Gene Kim — change management and deployment discipline
- _Release It!_ by Michael Nygard — failure modes and impact analysis
- _Site Reliability Engineering_ by Google — safe change practices in production
