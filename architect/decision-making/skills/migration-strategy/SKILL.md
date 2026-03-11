---
name: migration-strategy
description: Plan large-scale migrations from old systems to new architectures. Use when modernizing legacy systems or upgrading infrastructure.
---

# Migration Strategy

Plan phased migrations that minimize risk and disruption while delivering value incrementally.

## Instructions

1. **Assess Current State**: What's working? What's broken?
2. **Define Target State**: New architecture vision
3. **Identify Seams**: Where can you break the system into phases?
4. **Plan Phases**: Each phase delivers value; takes weeks to months
5. **Risk Mitigation**: Parallel running, feature flags, rollback plans
6. **Success Metrics**: How do we measure success of each phase?

## Anti-Patterns

- **Big Bang Rewrite**: Replace everything at once. Result: chaos and failure. **Guard**: Incremental, staged migration.
- **No Parallel Running**: Migrate directly without validation. **Guard**: Run old and new in parallel, validate.

## Further Reading

- _Strangler Fig Pattern_ — incremental replacement
- _Monolith to Microservices_ by Sam Newman
