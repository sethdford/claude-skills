---
name: storage-selection
description: Choose the right database technology for specific workloads. Evaluate relational, NoSQL, data warehouses, and search engines. Use when selecting storage systems for new features or optimizing existing ones.
---

# Storage Selection

Choose optimal database technology by analyzing workload characteristics, consistency requirements, and operational complexity.

## Context

You are helping select storage systems for specific data requirements. Analyze access patterns, consistency needs, data volume, and operational constraints. Read any existing schemas or architectural context provided.

## Domain Context

Based on Martin Kleppmann's _Designing Data-Intensive Applications_:

- **Relational Databases**: ACID transactions, schema enforcement, complex queries; limited horizontal scaling
- **Document Databases**: Flexible schema, natural object mapping, good for hierarchical data; transactions often single-document only
- **Key-Value Stores**: Fast reads/writes, simple data model; limited query flexibility
- **Column Family Stores**: Optimized for analytics and time-series; sparse data; distributed
- **Search Engines**: Full-text search, fuzzy matching, aggregations; not transaction-oriented
- **Data Warehouses**: Analytical queries, columnar storage, massive scale; designed for batch not realtime

## Instructions

1. **Catalog Data Requirements**: List primary access patterns (read-heavy? write-heavy? both?), data volume growth rate, consistency needs (strong/eventual?), query types (transactional vs analytical), and operational SLAs.

2. **Match Workload to Storage Type**: Transactional workload with complex queries → PostgreSQL. Document-oriented objects → MongoDB. Time-series metrics → Prometheus or InfluxDB. Full-text search → Elasticsearch. Analytical queries on massive datasets → BigQuery/Redshift.

3. **Evaluate Consistency vs Availability**: Need ACID guarantees across distributed systems? Relational with replication. Can tolerate eventual consistency? DynamoDB/Cassandra. Determine RTO/RPO requirements.

4. **Project Operational Burden**: Managed services (RDS, DynamoDB, BigQuery) reduce ops overhead. Self-hosted databases require backup, monitoring, scaling, tuning expertise.

5. **Cost Analysis**: Storage cost (per GB), compute cost (per hour or per query), backup/replication costs. Cross-reference with projected data growth and query volume.

## Anti-Patterns

- **One Database for Everything**: PostgreSQL solves every problem. Result: poor performance at scale, wrong tool for job. **Guard**: Accept polyglot persistence; different workloads need different databases.
- **Choosing Based on Hype**: Elasticsearch for everything because it's trendy. Result: overly complex infrastructure, unnecessary cost. **Guard**: Choose based on actual access patterns, not marketing.
- **Ignoring Operational Complexity**: Pick distributed database without ops expertise. Result: data loss, network partitions, failed migrations. **Guard**: Account for team operational maturity; managed services are often better than self-hosted.
- **Migrating Without Strategy**: Realize choice was wrong mid-project. Result: painful migration, downtime. **Guard**: Prototype with real data; test failure scenarios before committing.

## Further Reading

- _Designing Data-Intensive Applications_ by Martin Kleppmann — comprehensive storage system analysis
- _Database Internals_ by Alex Petrov — deep dive on storage engines and tradeoffs
- _NoSQL Databases_ by Dan McCreary and Ann Kelly — NoSQL patterns and when to use each type
