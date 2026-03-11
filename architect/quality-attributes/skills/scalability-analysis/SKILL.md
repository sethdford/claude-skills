---
name: scalability-analysis
description: Analyze and predict system scalability. Model growth, identify bottlenecks, project infrastructure costs. Use when planning for growth or investigating performance limits.
---

# Scalability Analysis

Systematically analyze system capacity, model growth scenarios, identify bottlenecks, and project infrastructure costs.

## Context

You are analyzing a system's capacity to handle growth. The user is planning for scale or debugging performance issues. Read their current traffic, growth rate, and performance metrics.

## Domain Context

Based on scalability research from Google, Netflix, and LinkedIn:

- **Amdahl's Law**: Speedup limited by non-parallelizable work; identify bottlenecks first
- **Little's Law**: Latency = Queue Depth / Throughput; understand queueing dynamics
- **Vertical vs Horizontal Scaling**: Add resources to single machine vs add more machines
- **Database Scaling**: Read replicas, sharding, CQRS, polyglot persistence
- **Cache as Scaling Tool**: Reduce database load by caching hot data

## Instructions

1. **Establish Baseline**: Document current traffic (requests/sec), peak traffic, p95 latency, error rate. Ask: "When does it feel slow?"

2. **Project Growth**: Model traffic growth over 6, 12, 24 months. At projected traffic, will current system break? Identify breaking point.

3. **Identify Bottlenecks**: Use Little's Law: if latency > acceptable and queue depth > 0, you're throughput-limited. Measure CPU, memory, database connections, network bandwidth.

4. **Model Scaling Scenarios**:
   - Vertical: Add CPU/memory to single machine. Gives 2-4x capacity typically.
   - Horizontal: Add more machines. Cost scales linearly, complexity higher.
   - Caching: Reduce database load. Example: cache customer data reduces DB load by 80%.

5. **Project Costs**: For each scenario, estimate monthly infrastructure cost. Include compute, database, storage, monitoring. Compare against revenue impact of outage.

## Anti-Patterns

- **Planning for 10x Growth Prematurely**: Design distributed system for traffic that's years away. Result: over-engineering, wasted effort. **Guard**: Solve scaling problem when it exists, not when it theoretically might.
- **Ignoring Database as Bottleneck**: Apps scale but database does not. Result: queries get slower as data grows. **Guard**: Test with realistic data size; identify where queries slow down.
- **Cache Without Strategy**: Cache everything, inconsistency everywhere. Result: stale data bugs. **Guard**: Cache only hot data; use TTL or event-driven invalidation.
- **Not Measuring**: Optimize based on gut feeling. Result: spend effort on wrong bottleneck. **Guard**: Always measure before and after optimization; publish metrics.

## Further Reading

- _The Art of Scalability_ by Martin Abbott and Michael Fisher — comprehensive scaling strategies
- _Designing Data-Intensive Applications_ by Martin Kleppmann — bottleneck identification and scaling patterns
- _Google's Scalability Lessons_ — published case studies and research
