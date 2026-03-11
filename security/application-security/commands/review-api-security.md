---
description: Audit API design, authentication, rate limiting, and input validation for security gaps.
argument-hint: [API specification (OpenAPI/Swagger) or endpoint list]
---

# Review API Security Command

Chain these steps:

1. Use `api-security-review` to audit API design and security controls
2. Use `web-security-headers` to verify security headers are present
3. Use `content-security-policy` to assess CSP configuration for XSS prevention

Deliverables:

- API security assessment covering authentication, authorization, rate limiting
- Input validation audit for all endpoints
- Security headers checklist and implementation guide
- CSP policy recommendations

After completion, suggest follow-up commands: `test-security`, `scan-dependencies`.
