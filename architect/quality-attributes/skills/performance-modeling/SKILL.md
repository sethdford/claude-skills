---
name: performance-modeling
description: Model system performance, predict latency under load, identify bottlenecks. Use when optimizing performance or capacity planning.
---

# Performance Modeling

Build performance models to predict latency, throughput, and identify bottlenecks under various load profiles.

## Context

You are optimizing system performance or planning capacity. The user has latency issues or wants to predict performance. Read their current metrics and workload characteristics.

## Domain Context

Based on queueing theory and performance modeling research:

- **Little's Law**: Latency = Queue Depth / Throughput
- **Queueing Models**: M/M/1 (simple), M/M/c (multi-server) help predict latency distribution
- **Response Time Hierarchy**: Network < Cache < In-Memory < Disk → Database
- **Throughput Ceiling**: Database connections, CPU cores, network bandwidth impose limits
- **Tail Latency**: p99 and p99.9 matter more than average; optimize for tail, not mean

## Instructions

1. **Measure Current Performance**: Establish baseline latency (p50, p95, p99) and throughput (requests/sec). Identify bottleneck component (database, cache, service).

2. **Build Queueing Model**: Model each bottleneck resource (database, cache, API server) as M/M/1 queue. Predict latency at 2x, 5x current load.

3. **Identify Breaking Points**: At what load does latency exceed acceptable threshold? At what load do errors appear? Plot latency vs load curve.

4. **Model Optimizations**: For each identified bottleneck, model impact of optimization:
   - Database: Add read replicas, caching, indexes
   - Network: Add CDN, compression
   - CPU: Add instances, optimize code

5. **Compare Trade-offs**: Cost of optimization (resources, effort) vs latency gain. Choose changes with best ROI.

## Anti-Patterns

- **Optimizing Average Instead of Tail**: p50 is 10ms but p99 is 500ms. Optimize p50 (easy) while ignoring p99 (impacts users). **Guard**: Always track and optimize p99 latency.
- **Missing Measurement Points**: Only measure at entry point, missing internal latency. Result: can't see where time is spent. **Guard**: Measure at every component boundary; trace requests.
- **Modeling Without Validation**: Build model, predict 2x scaling works, it doesn't. **Guard**: Validate model against actual load test; adjust assumptions if wrong.
- **Forgetting Overhead**: Model predicts 50ms latency but actual is 200ms. Result: overhead (GC, context switching) not accounted. **Guard**: Measure wall-clock time including all overhead.

## Further Reading

- _The Art of Computer Systems Performance Analysis_ by Raj Jain — queueing theory and modeling
- _Designing Data-Intensive Applications_ by Martin Kleppmann — performance analysis at scale
- _Google's Performance Optimization_ — case studies and methodologies
