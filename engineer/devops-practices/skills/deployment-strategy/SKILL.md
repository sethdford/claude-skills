---
name: deployment-strategy
description: Blue-green, canary, rolling deployments, traffic shifting, and safe release strategies.
---

# Deployment Strategy

Safe deployment patterns that minimize downtime and risk.

## Context

You are planning how to deploy code. Choose strategy based on risk tolerance.

## Domain Context

- **Blue-Green**: Two environments; switch traffic atomically
- **Canary**: Roll out to small % first; monitor; increase if good
- **Rolling**: Gradually replace instances; no downtime
- **Feature Flags**: Deploy code inactive; enable gradually

## Instructions

1. **Blue-Green**: Two prod environments; instant rollback
2. **Canary**: Send 5% to new version; monitor errors/latency
3. **Rolling**: Replace 10% at a time; gradual, safe
4. **Feature Flags**: Deploy off, turn on for users gradually
5. **Monitor**: Watch error rates, latency, business metrics
6. **Rollback**: Quick rollback if something goes wrong
7. **Incidents**: Have runbook for deployment failures

## Anti-Patterns

- No rollback plan; stuck if deploy goes bad
- Deploying without monitoring; don't know if it broke
- 100% traffic shift; any bug affects all users
- Manual deployments; error-prone, slow
- No canary; catch bugs by deploying to everyone

## Further Reading

- Google Cloud deployment strategies
- Progressive delivery (LaunchDarkly)
- Kubernetes deployment strategies
