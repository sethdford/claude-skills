---
name: query-optimization
description: EXPLAIN PLAN analysis, index selection, join strategies, and slow query debugging.
---

# Query Optimization

Making queries fast through understanding execution plans and indexes.

## Context

You are optimizing slow queries. Use EXPLAIN PLAN to understand execution.

## Domain Context

- **Execution Plan**: How database executes query; cost is estimate
- **Sequential Scan**: Reads all rows; slow on large tables
- **Index Scan**: Uses index; much faster if selective
- **Join Strategy**: Nested loop, hash, sort-merge; tradeoffs
- **Cardinality**: Rows filtered at each step

## Instructions

1. **Identify Slow Queries**: Slow logs, application monitoring
2. **Get EXPLAIN PLAN**: Understand how database executes query
3. **Look for Scans**: Sequential scan on large table = problem
4. **Add Indexes**: On columns in WHERE, JOIN, ORDER BY
5. **Verify Join Order**: Database should join most selective first
6. **Rewrite if Needed**: Sometimes different query is faster
7. **Monitor**: Re-check plan after schema changes

## Anti-Patterns

- Optimizing without EXPLAIN PLAN; guessing is unreliable
- Adding indexes for every column; slows writes, wastes storage
- Not updating stats; optimizer makes bad decisions
- Complex queries database can't optimize; rewrite
- Indexes on queries that return too much (unconstrained)

## Further Reading

- PostgreSQL EXPLAIN documentation
- MySQL EXPLAIN documentation
- SQL Antipatterns (Joe Celko), Chapter on queries
