---
name: api-security-review
description: Review API security including authentication, authorization, rate limiting, input validation, and data exposure.
---

# API Security Review

Review APIs for authentication, authorization, rate limiting, input validation, and data exposure risks.

## Context

You are a senior security architect reviewing API security for $ARGUMENTS. APIs are high-value targets because they often bypass UI validation and directly access backend systems. Common API vulnerabilities: broken authentication, missing authorization, rate limit bypass, input injection, excessive data exposure.

## Domain Context

- **API Authentication**: API keys, OAuth 2.0, JWT, mTLS, basic auth (deprecated)
- **Authorization**: Role-based access control (RBAC), attribute-based access control (ABAC), resource ownership checks
- **Rate Limiting**: Per-user, per-IP, per-endpoint; prevents brute force and DoS
- **Data Exposure**: Over-fetching (returning unnecessary fields), under-fetching (multiple requests), error messages revealing internals
- **API Versioning**: Managing breaking changes, deprecation timelines

## Instructions

1. **Review Authentication**:
   - **API Keys**: Are keys stored securely? Rotated regularly? Can they be revoked?
   - **OAuth 2.0**: Is the correct flow used? (Authorization Code for web apps, PKCE for mobile, Client Credentials for service-to-service)
   - **JWT**: Signed with strong algorithm (RS256, not HS256 unless symmetric key is secure)? Verified on every request? Expiration enforced?
   - **mTLS**: Certificates exchanged, validated, and rotated regularly?

2. **Review Authorization**:
   - **Resource Ownership**: Can user A access user B's resources? Check at query and database levels
   - **Role-Based Access**: Are roles enforced consistently? Can users elevate their role?
   - **Delegation**: If allowing delegated access (e.g., third-party apps), are permissions scoped? Auditable?
   - **Admin Functions**: Do admin endpoints check admin role? Are admin actions logged?

3. **Check Rate Limiting & Abuse Prevention**:
   - **Rate Limits**: Per-user and per-IP limits? Appropriate thresholds to prevent brute force?
   - **Endpoint Protection**: Are resource-intensive endpoints (search, reporting, export) rate-limited?
   - **Captcha/Challenge**: Is fallback protection in place for high-risk operations (login, password reset)?
   - **IP Blocking**: Is there automated blocking or alerting for suspicious IP activity?

4. **Review Input Validation & Output Encoding**:
   - **Input Validation**: All inputs validated (type, length, format)? Whitelist over blacklist?
   - **Injection Protection**: Protected against SQL injection, command injection, XML injection, path traversal?
   - **Output Encoding**: Responses encoded appropriately (JSON escaping, HTML escaping)?
   - **Error Messages**: Do error messages leak sensitive information (user existence, database structure)?

5. **Assess Data Exposure**:
   - **Over-fetching**: Does API return unnecessary fields? (Passwords, internal IDs, sensitive metadata)
   - **Under-fetching**: Do clients need to make many requests to get needed data? (Indicates missing pagination or query optimization)
   - **Pagination**: Are results paginated? Can attacker retrieve entire database?
   - **Sensitive Data**: Are PII, secrets, payment info properly redacted in responses?

## Anti-Patterns

- Using API keys as passwords; **keys should be application-level, not user-level; don't use in user login**
- Trusting OAuth scopes without server-side authorization checks; **always verify permissions server-side**
- Putting secrets in JWT payload (not encrypted); **JWT is signed but not encrypted; don't include secrets**
- Returning all database fields in responses; **explicitly define response schema; exclude sensitive fields**
- No rate limiting; **all APIs should have rate limits to prevent abuse and brute force**

## Further Reading

- OWASP API Security Top 10: https://owasp.org/www-project-api-security/
- RFC 6749 (OAuth 2.0 Authorization Framework): https://tools.ietf.org/html/rfc6749
- RFC 8949 (JWT, JWS, JWE): https://tools.ietf.org/html/rfc8949
- CWE Top 25: Focus on API-relevant vulnerabilities (CWE-89, CWE-79, CWE-200)
