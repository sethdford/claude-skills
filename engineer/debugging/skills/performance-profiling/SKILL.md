---
name: performance-profiling
description: CPU/memory profiling, identifying bottlenecks, flame graphs, hotspot analysis.
---

# Performance Profiling

Finding where code spends time and memory.

## Context

You are profiling code to find bottlenecks. Use CPU and memory profilers.

## Domain Context

- **CPU Profiling**: Where does code spend time? Stack sampling at regular intervals
- **Memory Profiling**: What allocates memory? Which objects aren't freed?
- **Flame Graph**: Visual representation; width = time, stacked = call stack
- **Hot Spots**: Functions consuming > 1% of time
- **Allocation Profiling**: Which code allocates the most objects?

## Instructions

1. **Start Profiler**: CPU profiler (perf, pprof, Java Flight Recorder)
2. **Run Under Load**: Profile should see realistic workload
3. **Collect Data**: Run for 10-30 seconds; enough to gather signal
4. **Analyze Output**: Flame graph or profiler GUI
5. **Identify Hot Spots**: Functions consuming most time
6. **Drill Down**: Zoom into hot functions; what calls them?
7. **Measure Impact**: Change code, re-profile, compare

## Anti-Patterns

- Profiling single-threaded code then deploying multi-threaded; lock contention changes profiles
- Optimizing without profiling; "optimization" is just guessing
- Micro-optimizing non-hotspot code; spend time on the hottest functions
- Not considering cache effects; CPU cache profilers show real impact
- Benchmarking without warm-up; first runs hit different code paths

## Further Reading

- Brendan Gregg, _Systems Performance_ and _Flame Graphs_
- Java Flight Recorder documentation (Java)
- pprof documentation (Go)
