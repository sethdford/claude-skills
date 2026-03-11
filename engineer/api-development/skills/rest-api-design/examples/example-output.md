# REST API Design: Payment Processing Service

## Domain

Payment processing for e-commerce platform.

## Resources Identified

| Resource      | Identity            | Relationships       |
| ------------- | ------------------- | ------------------- |
| Payment       | id, idempotency_key | belongs_to Order    |
| Order         | id                  | has_many Payments   |
| Refund        | id                  | belongs_to Payment  |
| PaymentMethod | id                  | belongs_to Customer |

## Endpoint Matrix

```
Payments
GET    /payments              - List all payments (admin)
POST   /payments              - Create payment (with idempotency key)
GET    /payments/{id}         - Get payment details
PATCH  /payments/{id}         - Update payment (e.g., add notes)

Refunds
POST   /payments/{id}/refunds - Issue refund for payment
GET    /payments/{id}/refunds - List refunds for payment
```

## Example Requests & Responses

### Request 1: Create Payment

```
POST /payments HTTP/1.1
Host: api.example.com
Content-Type: application/json
Idempotency-Key: "550e8400-e29b-41d4-a716-446655440001"
Authorization: Bearer [token]

{
  "order_id": 12345,
  "amount": 99.99,
  "currency": "USD",
  "payment_method": "credit_card",
  "card": {
    "number": "4111111111111111",
    "exp_month": 12,
    "exp_year": 2027,
    "cvc": "123"
  }
}
```

### Response 1: Payment Created (201 Created)

```json
{
  "id": "pay_abc123def456",
  "status": "succeeded",
  "order_id": 12345,
  "amount": 99.99,
  "currency": "USD",
  "payment_method": "credit_card",
  "last4": "1111",
  "created_at": "2026-03-11T14:30:00Z",
  "processing_fee": 2.97,
  "_links": {
    "self": { "href": "/payments/pay_abc123def456" },
    "refunds": { "href": "/payments/pay_abc123def456/refunds" },
    "order": { "href": "/orders/12345" }
  }
}
```

### Response 1 Error (422 Unprocessable Entity)

```json
{
  "error": {
    "code": "INVALID_CARD",
    "message": "Card number is invalid",
    "details": {
      "field": "card.number",
      "value": "4111111111111112",
      "reason": "Luhn check failed"
    }
  }
}
```

### Request 2: Get Payment

```
GET /payments/pay_abc123def456 HTTP/1.1
Authorization: Bearer [token]
```

### Response 2: Payment Details (200 OK)

```json
{
  "id": "pay_abc123def456",
  "status": "succeeded",
  "order_id": 12345,
  "amount": 99.99,
  "created_at": "2026-03-11T14:30:00Z",
  "processing_fee": 2.97,
  "last4": "1111",
  "_links": {
    "self": { "href": "/payments/pay_abc123def456" },
    "refunds": { "href": "/payments/pay_abc123def456/refunds" },
    "full_refund": {
      "href": "/payments/pay_abc123def456/refunds",
      "method": "POST",
      "body": { "amount": 99.99 }
    }
  }
}
```

### Request 3: Issue Refund

```
POST /payments/pay_abc123def456/refunds HTTP/1.1
Content-Type: application/json
Idempotency-Key: "550e8400-e29b-41d4-a716-446655440002"
Authorization: Bearer [token]

{
  "amount": 99.99,
  "reason": "customer_request",
  "notes": "Customer requested refund due to damaged goods"
}
```

### Response 3: Refund Created (201 Created)

```json
{
  "id": "ref_xyz789abc012",
  "payment_id": "pay_abc123def456",
  "amount": 99.99,
  "status": "succeeded",
  "reason": "customer_request",
  "created_at": "2026-03-11T14:35:00Z",
  "_links": {
    "self": { "href": "/refunds/ref_xyz789abc012" },
    "payment": { "href": "/payments/pay_abc123def456" }
  }
}
```

## Error Format

Standardized for ALL endpoints:

```json
{
  "error": {
    "code": "[SNAKE_CASE_ERROR_CODE]",
    "message": "[Human-readable error]",
    "details": {
      "field": "[field_name_if_applicable]",
      "value": "[actual_value_if_safe]",
      "reason": "[why_it_failed]"
    },
    "request_id": "[unique_id_for_logging]"
  }
}
```

**Common Status Codes**:

- `400 Bad Request` - Malformed JSON, missing required fields
- `401 Unauthorized` - Missing/invalid API key
- `403 Forbidden` - Insufficient permissions
- `404 Not Found` - Payment doesn't exist
- `422 Unprocessable Entity` - Card declined, invalid card, etc.
- `429 Too Many Requests` - Rate limited
- `500 Internal Server Error` - Server bug

## Idempotency Strategy

All POST requests require `Idempotency-Key` header:

```
Idempotency-Key: [UUID v4]
```

Server implementation:

1. Hash idempotency key → check if we've processed it before
2. If yes: return cached response (202 Accepted if still processing, 200/201 if done)
3. If no: process request, cache result, return response

Benefits:

- Clients can safely retry on network failures
- No duplicate charges on payment retries
- Transparent to callers; works automatically

## Pagination Strategy

For list endpoints (e.g., `GET /payments`):

```
GET /payments?limit=20&offset=40
```

Response:

```json
{
  "data": [
    { "id": "pay_1", ... },
    { "id": "pay_2", ... }
  ],
  "pagination": {
    "limit": 20,
    "offset": 40,
    "total": 500,
    "has_more": true,
    "next": "/payments?limit=20&offset=60"
  }
}
```

Alternatively, cursor-based (better for distributed systems):

```
GET /payments?limit=20&cursor=abc123

Response: { "data": [...], "next_cursor": "def456" }
```

## Summary

This API design:

- Uses nouns (payments, refunds), not verbs
- Maps HTTP methods semantically (POST = create, GET = retrieve)
- Uses semantic status codes (201 for creation, 422 for validation)
- Idempotent payment creation (safe retries via idempotency key)
- Standard error format across all endpoints
- Hypermedia links for discoverability
- Paginated list responses for scalability
