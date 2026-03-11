---
name: multi-region-design
description: Distribute globally across multiple regions for low latency, compliance, and resilience. Plan data replication, failover, and latency optimization. Use when designing global systems.
---

# Multi-Region Design

Architect globally distributed systems with low latency, data sovereignty, and automatic failover.

## Context

You are designing systems spanning multiple regions. Plan data replication, edge caching, latency optimization, and compliance. Read user distribution, latency requirements, and regulatory constraints.

## Domain Context

Based on global infrastructure design (Netflix, Google, Cloudflare):

- **Latency**: User experiences slowness if round-trip > 100ms. Multi-region with CDN typically needed for global audience.
- **Data Replication**: Eventual consistency (asynchronous) for high availability. Strong consistency harder to achieve globally; usually not needed.
- **Compliance**: GDPR requires EU data in EU. PIPL requires China data in China. Design for data residency.
- **Edge Computing**: Run compute near users; offload from central region
- **DNS-Based Routing**: Route users to nearest healthy region using geo-DNS

## Instructions

1. **Map User Distribution**: Where are users? 50% US-East, 30% Europe, 20% Asia? Design regions to minimize latency to majority.

2. **Plan Data Replication**: How quickly must data replicate to other regions? Realtime streaming (DynamoDB global tables) or batch (daily sync)? Cost increases with replication frequency.

3. **Implement Read Replicas**: Let each region read locally. Writes go to primary region, asynchronously replicate to replicas. Handle read-after-write consistency issues.

4. **Set Up Failover**: Primary region fails, automatically route to standby region. Traffic reroutes via DNS or load balancer health checks. Test failover regularly.

5. **Optimize Latency**: CDN caches static content near users. API Gateway in each region. Database read replicas local to region. Monitor latency by region; identify bottlenecks.

## Anti-Patterns

- **Multi-Region Without Plan**: "Let's just replicate everything globally." Result: complexity, cost, hard to debug. **Guard**: Design for specific latency/compliance needs; multi-region is expensive.
- **Strong Consistency Globally**: Require all regions to immediately see writes. Result: latency, complexity. **Guard**: Accept eventual consistency; design application for it.
- **No Failover Testing**: Assume it works. Result: regional failure becomes outage. **Guard**: Monthly failover drills; practice responding to regional incidents.
- **Ignoring Data Residency**: Replicate data to any region for performance. Result: compliance violation. **Guard**: Implement geofences; restrict EU data to EU regions.

## Further Reading

- _The Art of Scalability_ by Martin Abbott and Michael Fisher — global scaling strategies
- _Site Reliability Engineering_ by Google — multi-region deployment patterns
- _High Availability Architecture_ — resilience and failover patterns
