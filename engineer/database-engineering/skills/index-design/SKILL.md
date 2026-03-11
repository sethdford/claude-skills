---
name: index-design
description: B-tree indexes, composite indexes, covering indexes, UNIQUE indexes, and index trade-offs.
---

# Index Design

Strategic indexing for query performance without write overhead.

## Context

You are deciding which indexes to create. Index every query path, but don't overdo it.

## Domain Context

- **B-tree**: Default; works for most queries
- **Composite**: Multiple columns; order matters for range queries
- **Covering**: Includes all columns query needs; avoids table lookup
- **Unique**: Enforce uniqueness; sometimes performance benefit
- **Tradeoff**: Faster reads, slower writes, more storage

## Instructions

1. **Index WHERE Clauses**: Columns filtered
2. **Index JOIN Columns**: Foreign keys and join conditions
3. **Index ORDER BY**: Sorted columns
4. **Composite Order**: Equality first, then range, then sorts
5. **Covering Indexes**: Include SELECT columns; avoid table lookup
6. **Monitor**: Check that indexes are actually used
7. **Remove Unused**: Unused indexes waste storage and slow writes

## Anti-Patterns

- Too many indexes; slows writes, confuses optimizer
- Wrong index order in composite; doesn't help range queries
- Indexes on low-cardinality columns; sequential scan is faster
- Not considering write cost; read optimization kills write performance
- Indexes on every column; shotgun approach

## Further Reading

- PostgreSQL indexes documentation
- MySQL indexes documentation
- SQL Performance Explained (Markus Winand)
