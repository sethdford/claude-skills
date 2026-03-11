---
name: data-partitioning
description: Design partitioning and sharding strategies for data at scale. Use when single database hits throughput or storage limits.
---

# Data Partitioning

Design partitioning strategies (sharding, bucketing) to distribute data across multiple databases or nodes, enabling horizontal scaling.

## Context

You are designing data partitioning for large-scale systems. The user faces single database bottlenecks (throughput or storage). Read their data volume, access patterns, and consistency requirements.

## Domain Context

Based on designing data-intensive applications and partition strategies from Dynamo/Cassandra:

- **Range Partitioning**: Partition by key range (UserID 1-1000 on DB1, 1001-2000 on DB2). Simple but uneven load.
- **Hash Partitioning**: Partition by hash(key). Even distribution, but range queries require scatter-gather.
- **Directory-Based**: Maintain mapping of key → partition. Flexible, adds lookup cost.
- **Rebalancing**: When adding nodes, some partitions migrate. Strategy affects availability.
- **Hot Partitions**: Some keys receive disproportionate traffic. Mitigate by splitting hot partition or using caching.

## Instructions

1. **Choose Partition Key**: What key distributes evenly? UserID is obvious for user-centric apps. For IoT, might be (SensorType, RegionID). Avoid keys that hotspot (Country or Status).

2. **Select Partitioning Scheme**:
   - **Range**: If range queries common (time-series data). Risk: uneven distribution.
   - **Hash**: If uniform access. Range queries require scatter-gather.
   - **Directory**: If rebalancing needed frequently. Cost: lookup on every request.

3. **Plan Rebalancing**: How do you add capacity? Manual assignment or automatic? How long to rebalance? Require zero-downtime.

4. **Handle Hot Partitions**: If UserID=1 gets 1000x traffic, split further (UserID=1-A, UserID=1-B). Or use cache in front.

5. **Define Consistency Model**: Within partition, can be strongly consistent. Across partitions, typically eventual consistency. Define what queries require multi-partition reads.

## Anti-Patterns

- **Partition Key Too Fine-Grained**: Each request hits different partition. Result: no cache hits, high latency. **Guard**: Partition key should group frequently-accessed data.
- **Uneven Partition Distribution**: One partition holds 90% of data. Result: that node becomes bottleneck. **Guard**: Measure partition size distribution; rebalance if skew > 2x.
- **Cross-Partition Transactions**: Rely on distributed transactions for consistency. Result: complex, slow, failure-prone. **Guard**: Keep transactions within single partition; accept eventual consistency across partitions.
- **No Plan for Rebalancing**: Cannot add capacity without downtime. **Guard**: Design rebalancing strategy before going to production.

## Further Reading

- _Designing Data-Intensive Applications_ by Martin Kleppmann — comprehensive partitioning strategies
- _Cassandra: The Definitive Guide_ — practical partitioning in distributed systems
- _Google Spanner_ — consistency and partitioning at scale
