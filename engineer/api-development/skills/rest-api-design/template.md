# REST API Design

## Domain

[E-commerce, payment processing, etc.]

## Resources Identified

- Resource 1: [Noun, identity, relationships]
- Resource 2: [Noun, identity, relationships]
- ...

## Endpoint Matrix

| Method | Path           | Purpose        | Status |
| ------ | -------------- | -------------- | ------ |
| GET    | /resource      | List all       | 200    |
| POST   | /resource      | Create         | 201    |
| GET    | /resource/{id} | Retrieve       | 200    |
| PUT    | /resource/{id} | Replace        | 200    |
| PATCH  | /resource/{id} | Partial update | 200    |
| DELETE | /resource/{id} | Delete         | 204    |

## Example Request

```
POST /resource HTTP/1.1
Content-Type: application/json
Idempotency-Key: [UUID]

{ [fields] }
```

## Example Response (201 Created)

```json
{
  "id": 123,
  "_links": {
    "self": { "href": "/resource/123" }
  }
}
```

## Error Format

```json
{
  "error": {
    "code": "[ERROR_CODE]",
    "message": "[Human-readable message]",
    "details": { [context] }
  }
}
```

## Idempotency Strategy

[How POST/async operations handle retries]

## Pagination Strategy

[How large collections are paginated]
