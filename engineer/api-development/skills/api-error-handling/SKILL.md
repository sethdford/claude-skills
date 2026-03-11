---
name: api-error-handling
description: HTTP status codes, error response formats, recovery guidance, and client error handling.
---

# API Error Handling

Communicating errors clearly so clients can recover.

## Context

You are designing error responses. Be specific; help clients recover.

## Domain Context

- **Status Codes**: 4xx (client) vs 5xx (server)
- **Error Format**: Consistent structure across all APIs
- **Specific Codes**: 400 (bad request), 401 (auth), 403 (forbidden), 404 (not found), 429 (rate limited)
- **Retry Guidance**: Transient errors are retryable; permanent are not
- **Request ID**: Include for debugging production issues

## Instructions

1. **Use Right Status Code**: 4xx for client, 5xx for server
2. **Consistent Format**: {"error": {"code": "...", "message": "...", "details": {}}}
3. **Specific Codes**: "INVALID_EMAIL" not "bad request"
4. **Retry Guidance**: Include Retry-After header
5. **Request ID**: Include X-Request-ID for tracing
6. **Human & Machine**: Message for humans, code for machines
7. **Document**: Every error should be documented

## Anti-Patterns

- Same error format for all errors; hard for clients to handle
- 500 for client errors; 4xx/5xx distinction matters
- No error codes; clients parse message strings (fragile)
- No Retry-After header; clients guess when to retry
- Changing error format; breaking change, no warning

## Further Reading

- HTTP status code spec (RFC 7231)
- Problem Details for HTTP APIs (RFC 7807)
- Error handling patterns (Google API Design Guide)
