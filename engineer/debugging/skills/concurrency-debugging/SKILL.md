---
name: concurrency-debugging
description: Race conditions, deadlocks, thread analysis, happens-before relationships.
---

# Concurrency Debugging

Identifying bugs caused by concurrent access and timing issues.

## Context

You are debugging concurrency issues. These are the hardest bugs to find and reproduce.

## Domain Context

- **Race Condition**: Two threads access shared data; order matters; result is non-deterministic
- **Deadlock**: Threads waiting for each other; system hangs
- **Happens-Before**: Guarantee that one event completes before another
- **Memory Visibility**: When one thread sees writes from another thread

## Instructions

1. **Reproduce Consistently**: Add logging, delays, thread barriers
2. **Check Synchronization**: Are shared variables protected?
3. **Verify Lock Ordering**: Do all threads acquire locks in same order?
4. **Analyze Thread Dumps**: What is each thread waiting for?
5. **Look for Wait-Free Patterns**: Are threads spinning, not blocking?
6. **Use Tools**: ThreadSanitizer, Helgrind (Valgrind), or language-specific tools
7. **Add Happens-Before**: Use happens-before semantics (memory barriers, atomic ops)

## Anti-Patterns

- Single-threaded debugging then assuming it works threaded; concurrency bugs are different
- Using sleep() for synchronization; racey and slow
- Assuming x++ is atomic; it's not, use atomic operations
- Multiple locks protecting same data; hard to reason about
- Not testing under load; concurrency bugs often need high contention to appear

## Further Reading

- Brian Gorelick, _Concurrency in Practice_
- Java Concurrency in Practice (excellent; applies to other languages too)
- ThreadSanitizer documentation
