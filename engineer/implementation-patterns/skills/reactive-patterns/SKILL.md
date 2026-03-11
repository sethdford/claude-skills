---
name: reactive-patterns
description: Streams, observables, event-driven reactive systems, backpressure, and reactive programming.
---

# Reactive Patterns

Building systems that respond to events and data streams.

## Context

You are designing reactive systems. Understand the reactive manifesto and stream processing.

## Domain Context

- **Streams**: Asynchronous sequences of events/values
- **Observables**: Producers of streams; observers consume them
- **Backpressure**: Consumer can't keep up; producer must slow down
- **Reactive Manifesto**: Responsive, resilient, elastic, message-driven

## Instructions

1. **Model Data as Streams**: Think of updates as event sequences
2. **Use Operators**: Map, filter, reduce; transform streams
3. **Handle Backpressure**: If consumer is slow, producer must slow down
4. **Error Handling**: Streams can fail; plan error propagation
5. **Lifecycle**: When does stream start/stop? Clean up resources
6. **Test**: Use test schedulers; control time in tests

## Anti-Patterns

- Nested observables without flattening (FlatMap confusion)
- Ignoring backpressure; leads to memory exhaustion
- Silent failures in streams; explicitly handle errors
- Hot observables when you need cold; hot ones replay, cold ones don't
- Over-complicated operator chains; keep it readable

## Further Reading

- Reactive Manifesto (Ellis, Kuhn, Meyarivan, Vinoski)
- RxJS documentation (Reactive Extensions)
- Erik Meijer, "The Reactive Manifesto" (video)
