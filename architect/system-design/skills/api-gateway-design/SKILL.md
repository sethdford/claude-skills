---
name: api-gateway-design
description: Design API gateways that route, authenticate, rate-limit, and aggregate backend services. Use when building client-facing APIs or managing service boundaries.
---

# API Gateway Design

Design robust API gateways that handle authentication, rate limiting, routing, and response aggregation for backend services.

## Context

You are designing an API layer. The user is building client-facing APIs, managing multiple backends, or handling cross-cutting concerns like auth and rate limiting. Read their current API structure.

## Domain Context

Based on Sam Newman's API Gateway pattern and Kong/AWS API Gateway reference implementations:

- **Reverse Proxy**: Single entry point routing to multiple backends
- **Protocol Translation**: GraphQL ↔ REST, REST ↔ gRPC
- **Authentication Gateway**: Centralized JWT validation, OAuth2 token exchange
- **Rate Limiting**: Per-user, per-API, per-IP rate limits with backpressure
- **Response Aggregation**: Fan-out to multiple backends, merge responses (avoid N+1 problems)

## Instructions

1. **Define Gateway Responsibilities**: What should the gateway do?
   - Route requests to backends
   - Authenticate and authorize
   - Rate limit and throttle
   - Aggregate responses
   - Transform requests/responses (JSON ↔ Protocol Buffers)

2. **Design Routing Rules**: Map API paths to backend services. Example:

   ```
   /api/users/* → user-service
   /api/orders/* → order-service
   /api/inventory/* → inventory-service
   ```

3. **Implement Authentication**: Centralize JWT validation or OAuth2 token exchange. Avoid pushing auth to every backend. Include refresh token handling.

4. **Configure Rate Limiting**: Per-user limits (1000 req/min) and per-API limits (10k req/min total). Include exponential backoff and retry-after headers.

5. **Handle Response Aggregation**: For queries needing data from multiple services, aggregate at gateway. Example: order detail page fetches from order-service + inventory-service + pricing-service.

## Anti-Patterns

- **Gateway as Business Logic**: Adds validation, transformation, or orchestration logic. Result: gateway becomes bottleneck and single point of failure. **Guard**: Gateway routes and translates; backends own business logic.
- **No Rate Limiting Strategy**: Treats all clients equally. Result: one misbehaving client can starve others. **Guard**: Implement per-user, per-API, per-endpoint rate limits.
- **Synchronous Aggregation Without Timeout**: Gateway waits indefinitely for slow backend. Result: cascading timeout. **Guard**: Set timeout for each backend call; timeout on any exceeding limit.
- **Authentication Token Validation Every Request**: Validates token with auth service on every request. Result: auth service becomes bottleneck. **Guard**: Cache token validation (with TTL); only revalidate on expiry.

## Further Reading

- _Building Microservices_ by Sam Newman — gateway patterns and responsibilities
- _API Design Patterns_ by JJ Geewax — RESTful design and backwards compatibility
- _Kong API Gateway Documentation_ — practical implementation reference
