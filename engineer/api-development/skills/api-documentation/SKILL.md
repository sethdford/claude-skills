---
name: api-documentation
description: OpenAPI/Swagger, schema-driven documentation, examples, and interactive API docs.
---

# API Documentation

Creating accurate, useful API documentation from schemas.

## Context

You are documenting an API. Use schema-driven docs; keep them in sync with code.

## Domain Context

- **OpenAPI/Swagger**: Standard format for REST APIs
- **Schema-Driven**: Docs generated from schema; always in sync
- **Examples**: Include request/response examples for every endpoint
- **Interactive**: Tools like Swagger UI let clients try the API
- **Clarity**: Document error cases, rate limits, auth requirements

## Instructions

1. **Write OpenAPI Spec**: Define paths, parameters, responses
2. **Include Examples**: Show request/response for common cases
3. **Document Errors**: What 4xx/5xx responses are possible?
4. **Explain Auth**: How do clients authenticate? Token format?
5. **Rate Limits**: What are the limits? How to handle 429?
6. **Generate Docs**: Use tools to create HTML docs
7. **Test Docs**: Verify examples actually work

## Anti-Patterns

- Handwritten docs that drift from code; automated is better
- No examples; "see code" isn't helpful for API users
- Incomplete error documentation; clients don't know how to handle failures
- Not documenting required auth; clients struggle in production
- Not versioning docs; old clients can't find docs for their version

## Further Reading

- OpenAPI specification
- Swagger/OpenAPI tools (SwaggerUI, Redoc)
- API documentation best practices
