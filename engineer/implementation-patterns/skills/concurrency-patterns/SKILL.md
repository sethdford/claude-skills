---
name: concurrency-patterns
description: Actor model, CSP (Communicating Sequential Processes), lock-free patterns, async/await.
---

# Concurrency Patterns

Patterns for safe concurrent programming.

## Context

You are choosing a concurrency model. Each has different characteristics.

## Domain Context

- **Shared Memory**: Threads share memory; synchronize with locks
- **Message Passing**: Actors/processes; no shared memory; communicate via messages
- **Async/Await**: Cooperative multitasking; single-threaded event loop
- **Lock-Free**: Use atomic operations instead of locks

## Instructions

1. **Shared Memory**: Use for tightly-coupled code; sync with locks or atomic ops
2. **Actor Model**: Isolated actors, message-based; scale to many cores easily
3. **CSP**: Goroutines + channels; lightweight, composable
4. **Async/Await**: Single-threaded; good for I/O-bound workloads
5. **Lock-Free**: Complex; use only where locks are provably bottleneck
6. **Choose Wisely**: Wrong model makes everything harder

## Anti-Patterns

- Shared memory + locks everywhere; locks are error-prone
- Message passing when you need shared mutable state; forces unnecessary copies
- Async/await for CPU-bound work; won't help
- Lock-free without deep understanding; very easy to get wrong
- Mixing concurrency models in same codebase; confuses reasoning

## Further Reading

- Carl Hewitt, _Actor Model_ (original paper)
- Go documentation on Goroutines and Channels
- Rust documentation on Async/Await
