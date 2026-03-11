---
name: connection-pool-management
description: Pool sizing, connection lifetime, health checks, and resource exhaustion prevention.
---

# Connection Pool Management

Managing database connections efficiently to maximize throughput and prevent resource exhaustion.

## Context

You are configuring connection pools. Size appropriately; monitor usage.

## Domain Context

- **Pool Size**: How many concurrent connections? Too few = waits; too many = resource exhaustion
- **Connection Lifetime**: How long should connection live? Connections age, become stale
- **Health Checks**: Validate connections before reuse
- **Idle Timeout**: Close unused connections; free resources
- **Queuing**: What happens when all connections are busy?

## Instructions

1. **Min/Max Size**: Min = base connections; Max = peak + buffer
2. **Max = (Number of Cores \* 2) + Extra for I/O**: Rule of thumb
3. **Connection Lifetime**: 30 minutes common; depends on database
4. **Idle Timeout**: 5 minutes; reclaim unused connections
5. **Health Checks**: Ping connection before using; catch stale connections
6. **Queue Size**: What happens if all connections busy? Queue or error?
7. **Monitoring**: Track pool utilization, wait times

## Anti-Patterns

- Pool too small; queries wait forever
- Pool too large; resource exhaustion, slow start
- No health checks; stale connections cause errors
- No idle timeout; connections accumulate, eventually exhaust
- Not monitoring; don't know if pool is too small

## Further Reading

- HikariCP documentation (Java)
- Connection pool best practices (AWS)
- Database connection tuning guides
