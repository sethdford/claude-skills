---
name: transaction-management
description: ACID properties, isolation levels, locks, deadlocks, and transaction design.
---

# Transaction Management

Ensuring data consistency through proper transaction design.

## Context

You are designing transactions. Use appropriate isolation level; understand lock behavior.

## Domain Context

- **ACID**: Atomicity, Consistency, Isolation, Durability
- **Isolation Levels**: Read Uncommitted, Read Committed, Repeatable Read, Serializable
- **Locks**: Shared (read), exclusive (write); deadlock possible
- **Deadlock**: Two transactions waiting for each other; database detects and rolls back
- **Consistency**: Invariants maintained; foreign keys, constraints

## Instructions

1. **Identify Invariants**: What must always be true? Enforce with constraints
2. **Transaction Scope**: Minimal; only what needs to be atomic
3. **Isolation Level**: READ_COMMITTED common; SERIALIZABLE for strong consistency
4. **Lock Order**: Acquire locks in same order everywhere; prevents deadlock
5. **Timeout**: Have timeout; if hanging, something is wrong
6. **Error Handling**: Catch and retry on deadlock
7. **Monitoring**: Track transaction time, lock waits

## Anti-Patterns

- Long transactions; hold locks, block other queries
- Wrong isolation level; causes data anomalies
- Deadlocks and retry in app; fix root cause, not symptom
- Not enforcing invariants at DB; data becomes inconsistent
- Ignoring SERIALIZABLE; assumes isolation level is safe

## Further Reading

- Postgres transaction documentation
- ACID properties (Wikipedia or C.J. Date)
- PostgreSQL lock documentation
