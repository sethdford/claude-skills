---
description: Audit existing architecture for resilience and scalability. Produces recommendations.
argument-hint: [current system description or architecture diagram]
---

# Evaluate Architecture

Chain these steps:

1. Use the `monolith-assessment` skill to assess if system should stay monolith or split. Measure deployment frequency, team size, scaling pain.

2. Use the `caching-strategy` skill to identify caching gaps. Where are cache misses causing database spike? Where is stale data causing inconsistency?

3. Use the `data-partitioning` skill to evaluate if data scaling is hitting limits. Identify hotspot partitions, cross-partition queries that hurt performance.

4. Use the `microservices-patterns` skill to audit resilience. Are there cascading failures? Missing circuit breakers, retries, idempotency keys?

5. Use the `service-mesh-patterns` skill to assess observability. Can you trace requests across services? Do you have SLIs for latency, error rate, saturation?

## Deliverables

Produce:

- **Resilience Audit**: Identify single points of failure, cascading failure risks, missing circuit breakers, retry logic, timeout configurations
- **Scalability Audit**: Current QPS, peak QPS capacity, bottlenecks (database, cache, service), cost per request
- **Caching Effectiveness**: Cache hit rates by layer, eviction rates, stale data incidents
- **Partition Health**: Partition size distribution, skew ratio, cross-partition query frequency, rebalancing costs
- **Recommendations Roadmap**: Prioritized fixes by impact and effort. Short-term (1-2 weeks), medium-term (1-3 months), long-term (3-6 months)

## Critical Thinking Prompts

Before recommending changes:

- What's the actual business cost of the identified bottleneck? (missed revenue, support load, user churn)
- How much effort to fix? (dev time, ops time, risk of breaking things)
- Is this the most impactful fix right now, or are there bigger bottlenecks?
- If we fix this, what becomes the new bottleneck?
- Have we measured before making the change? Can we measure improvement after?

## Follow-Up Commands

- `architect-system` — If redesign needed
- `decompose-monolith` — If splitting is recommendation
- `design-infrastructure` — If deployment topology needs change
