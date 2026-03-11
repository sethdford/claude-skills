---
name: rest-api-design
description: REST API design with semantic HTTP methods, status codes, and resource modeling. Use when designing new APIs or reviewing existing API designs.
context: fork
agent: general-purpose
allowed-tools: Read, Grep, Glob, Write, Edit
---

# REST API Design

Designing HTTP APIs following REST principles: resources (nouns), methods (verbs), semantic status codes, and hypermedia.

## Context

You are designing or reviewing a REST API. Your role is to:

- Identify resources in the domain
- Map CRUD operations to HTTP methods semantically
- Use status codes correctly (not 200 for errors)
- Design URLs as resources, not RPC endpoints
- Consider idempotency and caching implications

REST is architectural style, not HTTP CRUD framework. Treat it with discipline.

## Domain Context

Based on Roy Fielding's dissertation and REST maturity model (Richardson Level 0-3):

- **Resources**: Nouns (users, orders, products). Identified by URLs.
- **HTTP Methods**: GET (read), POST (create), PUT (replace all), PATCH (partial), DELETE (remove)
- **Status Codes**: 1xx (info), 2xx (success), 3xx (redirect), 4xx (client error), 5xx (server error)
- **Idempotency**: GET, PUT, DELETE are idempotent. POST is not.
- **Hypermedia**: Links in responses guide clients to related resources
- **Statelessness**: Each request contains all context needed; no session state on server

## When to Use This Skill

- Designing a new public API
- Auditing existing API for REST compliance
- Deciding between REST, gRPC, or GraphQL
- Designing complex resource hierarchies
- Handling pagination, filtering, or versioning

## Prerequisites

- Understand domain entities and relationships
- Know HTTP methods and status codes (or willing to learn)
- Have clear acceptance criteria for API behavior
- Can write test requests (curl, Postman, HTTP client)

## Instructions (Detailed)

### 1. **Identify Resources**

Ask: "What are the nouns in this domain?"

Example (E-commerce API):

- Resource: User, Product, Order, Cart, Review, Inventory

For each resource, define:

- **Identity**: What uniquely identifies it? (id, email, SKU)
- **Relationships**: How does it relate to others? (User → many Orders)
- **Operations**: What actions apply? (CRUD + domain actions)

### 2. **Design Resource Paths**

```
/resource              - collection of resource
/resource/{id}        - individual resource
/resource/{id}/sub    - sub-resource (collection)
/resource/{id}/sub/{id} - individual sub-resource
```

**Good paths**:

```
GET  /users              - list all users
POST /users              - create user
GET  /users/123          - get user 123
PUT  /users/123          - replace user 123
PATCH /users/123         - partially update user 123
DELETE /users/123        - delete user 123

GET  /users/123/orders   - get user 123's orders
POST /users/123/orders   - create order for user 123
```

**Bad paths** (RPC-style, avoid):

```
GET  /getUser?id=123
GET  /user/create
POST /user?action=update
GET  /deleteUser?id=123
```

### 3. **Map HTTP Methods Semantically**

- **GET**: Retrieve without side effects. Safe and idempotent.
- **POST**: Create new resource. Not idempotent (multiple POSTs = multiple resources).
- **PUT**: Replace entire resource. Idempotent (same PUT twice = same result).
- **PATCH**: Partial update. May or may not be idempotent (depends on implementation).
- **DELETE**: Remove resource. Idempotent (delete twice = idempotent; second delete returns 404).

**Example**:

```
POST /orders           - create NEW order → 201 Created
PUT /orders/123        - REPLACE entire order (all fields) → 200 OK
PATCH /orders/123      - UPDATE some fields → 200 OK
GET /orders/123        - RETRIEVE order → 200 OK
DELETE /orders/123     - REMOVE order → 204 No Content (or 200)
```

### 4. **Use Status Codes Correctly**

**Success**:

- `200 OK` - Request succeeded, response includes result
- `201 Created` - Resource created; response includes resource and Location header
- `202 Accepted` - Request accepted for processing (async operations)
- `204 No Content` - Success but no response body (DELETE often returns this)

**Redirection**:

- `301 Moved Permanently` - Resource moved to new URL
- `303 See Other` - Result is at a different URL (use for POST redirect)
- `304 Not Modified` - Resource unchanged since client's If-Modified-Since

**Client Error**:

- `400 Bad Request` - Malformed request (missing field, invalid JSON)
- `401 Unauthorized` - Missing authentication
- `403 Forbidden` - Authenticated but no permission
- `404 Not Found` - Resource doesn't exist
- `409 Conflict` - Request conflicts with current state (e.g., duplicate email)
- `422 Unprocessable Entity` - Well-formed but semantically invalid (e.g., invalid email format)

**Server Error**:

- `500 Internal Server Error` - Server bug, not client's fault
- `503 Service Unavailable` - Server overloaded or down

### 5. **Handle Errors Consistently**

Define a standard error response:

```json
{
  "error": {
    "code": "INVALID_EMAIL",
    "message": "Email address is invalid",
    "details": {
      "field": "email",
      "value": "not-an-email"
    }
  }
}
```

Use same error structure for ALL endpoints. Clients can parse errors consistently.

### 6. **Design for Idempotency**

**Idempotent operations** (safe to retry):

- GET, HEAD, OPTIONS - read-only
- PUT - replacing resource (same result each time)
- DELETE - removing resource (idempotent; second delete returns 404)

**Non-idempotent operations** (retrying causes problems):

- POST - creates new resource; each retry creates duplicate

For non-idempotent operations, require client to provide idempotency key:

```
POST /orders
Idempotency-Key: "550e8400-e29b-41d4-a716-446655440000"
Content-Type: application/json
{ "items": [...], "payment": "credit_card" }
```

Server stores key → response mapping. If client retries with same key, return cached response (no duplicate order).

### 7. **Include Hypermedia Links**

Self-describing API: responses include links to related resources.

```json
{
  "id": 123,
  "name": "John",
  "email": "john@example.com",
  "_links": {
    "self": { "href": "/users/123" },
    "all_users": { "href": "/users" },
    "orders": { "href": "/users/123/orders" }
  }
}
```

Benefits: Clients can discover endpoints without hardcoding URLs.

### 8. **Handle Pagination**

For large collections, paginate:

```
GET /users?page=2&limit=20
GET /users?offset=40&limit=20
GET /users?cursor=abc123&limit=20  (cursor-based, better for distributed systems)
```

Response includes pagination metadata:

```json
{
  "data": [...],
  "pagination": {
    "page": 2,
    "limit": 20,
    "total": 500,
    "next": "/users?page=3&limit=20"
  }
}
```

### 9. **Document with Examples**

Every endpoint needs documentation showing:

- Request method and path
- Request body example
- Response body example (success and common errors)
- Status codes returned

## Output Format

When designing an API, deliver:

1. **Resource List**: What resources does the API expose?
2. **Endpoint Matrix**: Methods × resources
3. **Request/Response Examples**: Concrete JSON examples
4. **Error Handling**: Standard error format
5. **Idempotency Strategy**: How to handle retries
6. **Pagination Strategy**: How to handle large collections

## Worked Example: E-Commerce Order API

**Domain**: Create, update, retrieve orders.

**Resources**: User, Order, OrderItem, Product

**Endpoints**:

```
Users
GET    /users              - list users
POST   /users              - create user
GET    /users/{id}         - get user
PUT    /users/{id}         - replace user
DELETE /users/{id}         - delete user

Orders
GET    /orders             - list orders (paginated)
POST   /orders             - create order
GET    /orders/{id}        - get order
PUT    /orders/{id}        - replace order
DELETE /orders/{id}        - cancel order

Order Items (sub-resource)
GET    /orders/{id}/items  - get order items
POST   /orders/{id}/items  - add item to order
```

**Request Examples**:

```
POST /orders HTTP/1.1
Idempotency-Key: "550e8400-e29b-41d4-a716-446655440000"
Content-Type: application/json

{
  "user_id": 123,
  "items": [
    {"product_id": 456, "quantity": 2},
    {"product_id": 789, "quantity": 1}
  ],
  "shipping_address": {
    "street": "123 Main St",
    "city": "Springfield",
    "zip": "12345"
  }
}
```

**Response** (201 Created):

```json
{
  "id": 999,
  "user_id": 123,
  "status": "pending",
  "created_at": "2026-03-11T14:30:00Z",
  "items": [...],
  "_links": {
    "self": { "href": "/orders/999" },
    "cancel": { "href": "/orders/999", "method": "DELETE" },
    "user": { "href": "/users/123" }
  }
}
```

## Decision Framework

- **REST vs GraphQL?**: REST for simple CRUD APIs; GraphQL for complex queries
- **Versioning?**: Use URL path (`/v1/`) or header (`Accept: application/vnd.api+json;version=1`)
- **Nested resources?**: Keep nesting <3 levels; use query params otherwise
- **Bulk operations?**: POST to collection with array of items
- **Async operations?**: Return 202 Accepted + Location header with status endpoint

## Anti-Patterns

- Using only GET and POST (ignores PUT, DELETE, PATCH)
- Returning 200 for errors (breaks HTTP semantics; use 4xx)
- RPC-style URLs (/getUser instead of GET /users/{id})
- No error standardization (each endpoint has different error format)
- Ignoring idempotency (clients can't safely retry)
- Breaking changes without versioning (consumers break)

## Quality Checklist

- [ ] All resources identified and mapped to nouns
- [ ] HTTP methods match CRUD/domain actions
- [ ] Status codes are semantically correct
- [ ] Error format is standardized across all endpoints
- [ ] Idempotency strategy defined for POST/async operations
- [ ] Pagination implemented for large collections
- [ ] Hypermedia links included where sensible
- [ ] All endpoints documented with request/response examples
- [ ] Edge cases handled (invalid input, resource not found, etc.)
- [ ] API is versioned or designed for backward compatibility

## Further Reading

- Roy Fielding, _Representational State Transfer_ (dissertation, 2000)
- Martin Fowler, _Richardson Maturity Model_ (blog post)
- Microsoft Azure REST API Guidelines
- Google API Design Guide
- RFC 7231 (HTTP/1.1 Semantics and Content)
- RFC 7232 (HTTP/1.1 Conditional Requests)
