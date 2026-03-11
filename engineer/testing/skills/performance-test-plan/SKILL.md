---
name: performance-test-plan
description: Load testing, profiling, SLA verification, bottleneck identification.
---

# Performance Test Plan

Strategy for measuring and verifying performance characteristics.

## Context

You are designing performance tests. Measure baseline, set thresholds, identify bottlenecks.

## Domain Context

- **Load Testing**: How system behaves under expected/peak load
- **Stress Testing**: At what point does system break?
- **Profiling**: Where do CPU/memory/I/O bottlenecks exist?
- **SLA Verification**: Does system meet response time, throughput commitments?
- **Regression Detection**: Did recent changes degrade performance?

## Instructions

1. **Define SLAs**: Response time P99? Throughput? Memory budget?
2. **Create Load Profile**: How many users? What do they do?
3. **Measure Baseline**: Establish baseline metrics before optimization
4. **Profile Hot Paths**: Identify which code consumes CPU/memory
5. **Set Thresholds**: Alert if response time exceeds target
6. **Run Regularly**: Performance tests in CI to catch regressions
7. **Compare Versions**: Before/after comparison for optimization

## Anti-Patterns

- Performance tests that are flaky or environment-dependent; unreliable signals
- Benchmarking without realistic load; lab results don't match production
- Micro-optimizations without profiling; premature optimization is evil
- Ignoring memory leaks in performance tests; good data won't show memory creep
- Setting unrealistic SLAs; know your hardware limits

## Further Reading

- Brendan Gregg, _Systems Performance: Enterprise and the Cloud_
- Martin Fowler, _Profiling_ essay
