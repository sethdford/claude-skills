---
name: feature-flag-design
description: Designing feature flags for gradual rollouts, A/B testing, and safe feature releases.
---

# Feature Flag Design

Using flags to decouple deployment from release; enable gradual rollouts and fast rollback.

## Context

You are implementing feature flags. Design them carefully; they add complexity.

## Domain Context

- **Kill Switch**: Instantly disable feature if problematic
- **Gradual Rollout**: 1%, 10%, 50%, 100%; monitor each stage
- **Canary Users**: Beta testers; test features early
- **A/B Test**: Compare two implementations; measure impact
- **Audience**: Flags can be per-user, per-region, per-segment

## Instructions

1. **Keep Simple**: Don't over-engineer; flags add complexity
2. **Owner**: Who owns the flag? Who can toggle?
3. **Expiration**: When should flag be removed? Set date
4. **Rollout**: Gradual strategy; start small
5. **Monitoring**: Track flag usage, errors, impact
6. **Cleanup**: Remove flags after rollout complete
7. **Config**: Flags in code, toggled via server; fast toggle

## Anti-Patterns

- Flags everywhere; can't understand code paths
- Permanent flags; accumulate and complicate
- Not monitoring flags; don't know if feature works
- Slow flag propagation; takes minutes to toggle
- Flags without expiration date; forgotten forever

## Further Reading

- LaunchDarkly documentation
- Feature flags best practices
- Flickr's approach to feature deployment
