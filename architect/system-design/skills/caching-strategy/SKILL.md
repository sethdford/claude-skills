---
name: caching-strategy
description: Design multi-layer caching strategies (client, edge, service, database) for performance. Use when optimizing latency or reducing database load.
---

# Caching Strategy

Design multi-layer caching that reduces latency and database load while maintaining consistency and managing invalidation complexity.

## Context

You are optimizing system performance through caching. The user faces latency or database load issues. Read their access patterns and consistency requirements.

## Domain Context

Based on cache patterns in high-performance systems (Facebook, Google, Stripe):

- **Cache Aside**: Application loads from cache; on miss, load from database and populate cache
- **Write-Through**: Write to cache and database atomically; ensures consistency
- **Write-Behind**: Write to cache, asynchronously write to database; risk of data loss
- **Cache Invalidation**: Hard problem; strategies include TTL, explicit invalidation, event-driven
- **Consistency Models**: Strong (everything fresh) vs eventual (stale allowed for period)

## Instructions

1. **Map Access Patterns**: Identify hot data (accessed frequently). Example: user profile read 100x/sec, updated 1x/min. Cache profile with 1-minute TTL.

2. **Design Multi-Layer Cache**:
   - **Client Cache**: Browser/app cache (hours). Compress, use ETags.
   - **CDN Cache**: Static assets (images, CSS) worldwide (days).
   - **Service Cache**: In-memory or Redis (seconds to minutes).
   - **Database Cache**: Query result cache, index caching.

3. **Choose Cache Policy**:
   - **Cache-Aside**: Simple, but requires handling misses. Good for read-heavy.
   - **Write-Through**: Consistent, but slower writes. Good for consistency-critical.
   - **Write-Behind**: Fast writes, risk of loss. Good for analytics.

4. **Define Invalidation Strategy**:
   - **TTL**: Simple, but stale data for TTL duration.
   - **Event-Driven**: On write, invalidate cache. Immediate consistency, complex.
   - **Hybrid**: TTL + event-driven. Cache valid for TTL; on write, invalidate immediately.

5. **Establish Metrics**: Monitor cache hit rate (target >80%), eviction rate, memory usage. Alert on hit rate drop (indicates cache thrashing).

## Anti-Patterns

- **Caching Without TTL**: Cache grows indefinitely, serving stale data forever. **Guard**: Every cache entry has explicit TTL or invalidation trigger.
- **Cache Stampede**: Thundering herd of requests when hot key expires. Result: spike in database load. **Guard**: Use probabilistic TTL or cache warming.
- **Storing Secrets in Cache**: API keys, tokens in cache. Result: exposure in shared cache. **Guard**: Never cache secrets; use separate secure storage.
- **Inconsistent Invalidation**: Different code paths invalidate differently. Result: stale data in some flows. **Guard**: Centralize invalidation logic; test cache invalidation.

## Further Reading

- _Designing Data-Intensive Applications_ by Martin Kleppmann — caching patterns and consistency
- _Redis in Action_ — practical in-memory caching strategies
- _High Performance Browser Networking_ — client-side and CDN caching
