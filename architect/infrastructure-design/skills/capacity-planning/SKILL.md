---
name: capacity-planning
description: Forecast infrastructure resource needs (compute, storage, network). Model growth scenarios and utilization targets. Use when planning infrastructure investments or optimizing costs.
---

# Capacity Planning

Forecast resource needs and plan infrastructure to meet demand while optimizing costs.

## Context

You are planning infrastructure capacity. Model growth, forecast peak load, size infrastructure for headroom. Read historical metrics, growth trends, and business projections.

## Domain Context

Based on capacity planning and performance modeling:

- **Utilization Target**: 70-80% typical for servers (avoid 100% - no headroom). Database: 70-80%. Network: 60-70% to avoid congestion.
- **Headroom**: Plan for 2-3x growth before re-architecture. At 70% utilization with 10% monthly growth, capacity lasts ~6 months.
- **Seasonality**: Traffic varies by season (Black Friday 10x normal). Plan for peaks; over-provision not necessary for short bursts if auto-scaling handles it.
- **Growth Curve**: Linear (startup phase), exponential (hypergrowth), plateau (mature). Different forecasting strategies per phase.

## Instructions

1. **Establish Baseline**: Measure current usage (CPU, memory, storage, network bandwidth). Peak vs average. Growth rate over past 6-12 months.

2. **Project Growth**: Based on growth rate and business projections. Linear extrapolation for stable growth. Exponential model for hypergrowth startups. Add margin for uncertainty.

3. **Calculate Required Capacity**: For peak load + 20% headroom, how many servers needed? At 70% CPU utilization per server, peak_load / 0.7 = servers needed.

4. **Model Scenarios**: Best case (fast growth, more servers). Worst case (slow growth, fewer servers). Plan investment for mid-case; be ready to scale up/down.

5. **Plan Upgrades**: When do you need additional capacity? In 6 months? Plan lead time for procurement, setup, migration. Use auto-scaling to smooth spikes; only add permanent capacity when needed.

## Anti-Patterns

- **Over-Provisioning**: Buy capacity for 5 years of growth. Result: underutilized, wasted cost. **Guard**: Plan for 1-2 years; cloud enables rapid scaling.
- **No Growth Plan**: Assume current load is constant. Result: surprised by capacity limits. **Guard**: Monitor trends; forecast quarterly.
- **Ignoring Auto-Scaling**: Manual provisioning for every 10% traffic increase. Result: operational burden, missed peaks. **Guard**: Auto-scaling for predictable load variations; manual provisioning for structural growth.
- **No Utilization Monitoring**: Assume servers fully utilized. Result: under-utilization, wasted cost. **Guard**: Monitor and right-size; consolidate low-utilization servers.

## Further Reading

- _Capacity Planning_ by Neil J. Gunther — quantitative capacity planning
- _The Art of Scalability_ by Martin Abbott and Michael Fisher — growth strategies
- _AWS Cost Optimization_ — rightsizing and utilization analysis
