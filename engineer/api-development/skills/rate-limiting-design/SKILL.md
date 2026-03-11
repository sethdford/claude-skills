---
name: rate-limiting-design
description: Rate limiting strategies (token bucket, sliding window, quota), DOS protection, and fair usage.
---

# Rate Limiting Design

Protecting APIs from overload and abuse.

## Context

You are designing rate limiting. Choose strategy; balance protection and usability.

## Domain Context

- **Token Bucket**: Smooth spikes; refill at constant rate
- **Sliding Window**: Exact window; more accurate; harder to implement
- **Quota**: Per-day/month limits; common for paid APIs
- **Adaptive**: Adjust limits based on load
- **Fair Use**: Prevent one user from killing service

## Instructions

1. **Set Limits**: How many requests per second? Per user?
2. **Choose Algorithm**: Token bucket (simple), sliding window (accurate)
3. **Communicate Limits**: Headers tell client about remaining quota
4. **Handle Overages**: 429 response; tell client when to retry
5. **Exempt Authenticated**: Different limits for different user types
6. **Monitor**: Track usage; adjust limits if needed

## Anti-Patterns

- Too strict limits; angry users
- Not communicating limits; clients spam, hit limits, get angry
- No backoff guidance; clients retry immediately, making problem worse
- Hitting limits on important operations (payment); loses customers
- No monitoring; surprise outages from limit exhaustion

## Further Reading

- Rate Limiting Pattern (Martin Fowler)
- AWS API Gateway rate limiting
- Stripe rate limiting approach
