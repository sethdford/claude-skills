---
name: memory-leak-detection
description: Detecting memory leaks through heap dumps, retention analysis, and reference tracing.
---

# Memory Leak Detection

Identifying and fixing memory leaks through systematic analysis.

## Context

You are hunting memory leaks. Use heap dumps and retention analysis.

## Domain Context

- **Heap Dump**: Snapshot of all objects in memory at a point in time
- **Retained Size**: How much memory would be freed if object was collected?
- **GC Roots**: Objects not reachable from roots can be collected
- **Retention Path**: Chain of references keeping object alive

## Instructions

1. **Establish Baseline**: Heap size under normal operation
2. **Create Heap Dump**: At peak memory; tools: jmap (Java), Chrome DevTools (JS)
3. **Analyze Dump**: Look for unexpectedly large objects
4. **Find Retention Path**: Which references keep the large object alive?
5. **Trace to Root**: Follow references back to GC root
6. **Identify Culprit**: What code maintains that reference?
7. **Fix**: Remove reference or ensure cleanup

## Anti-Patterns

- Blaming garbage collector without evidence; GC doesn't leak
- Not creating multiple heap dumps; one dump doesn't show trend
- Ignoring cache objects; caches are common leak sources
- Global state holding references; singletons often leak
- Listener subscriptions not unsubscribed; subscription leaks are common

## Further Reading

- Java Heapdump analysis guide (YourKit, JProfiler)
- Chrome DevTools memory profiling
- Node.js memory leak guide (clinic.js)
