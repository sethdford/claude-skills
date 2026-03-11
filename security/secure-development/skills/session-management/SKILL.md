---
name: session-management
description: Implement secure session handling with proper token generation, storage, expiry, CSRF protection, and session invalidation.
---

# Session Management

Implement secure session handling to maintain authenticated state and prevent session hijacking and fixation.

## Context

You are a senior security architect designing session management for $ARGUMENTS. Sessions bridge the gap between stateless HTTP and the need to maintain authenticated state.

## Domain Context

- **Session State**: Maintain authenticated user state across HTTP requests
- **Session Tokens**: Cryptographically random, high-entropy identifiers; never sequential or predictable
- **Storage**: HTTPOnly cookies (for web browsers), Bearer tokens (for APIs), or both
- **Expiry**: Short-lived tokens reduce window of compromise; refresh tokens enable longer sessions without exposing long-lived credentials

## Instructions

1. **Session Token Generation**:
   - Use cryptographic randomness (at least 128 bits entropy; 256 bits preferred)
   - Never sequential or predictable (not timestamp-based, not incremental)
   - Libraries: Python `secrets.token_urlsafe()`, Node `crypto.randomBytes()`, Go `crypto/rand`
   - Example: 32-byte random = 256-bit entropy = ~2^256 possible tokens; safe against brute force

2. **Cookie Configuration** (for web):
   - **HTTPOnly**: Prevent JavaScript access (limits XSS impact)
   - **Secure**: HTTPS-only; not sent over HTTP
   - **SameSite=Strict** (ideal) or **SameSite=Lax**: Prevent CSRF attacks
   - **Domain/Path**: Restrict to specific domain/path (not broader than necessary)
   - **Max-Age/Expires**: Short-lived (1-24 hours, not months)
   - Example: `Set-Cookie: sessionid=abc123; HttpOnly; Secure; SameSite=Strict; Max-Age=3600; Path=/`

3. **JWT Token Configuration** (for APIs):
   - Use RS256 (RSA) or ES256 (ECDSA) for signing; never HS256 (symmetric; vulnerable if key is exposed)
   - Include expiry (`exp` claim) and issued-at time (`iat`)
   - Short expiry (5-60 minutes); use refresh token for longer sessions
   - Never include sensitive data (password, secrets) in JWT payload; payload is readable (base64, not encrypted)
   - Example token lifetime: Access token 15 min, Refresh token 7 days

4. **Session Invalidation**:
   - Invalidate on logout (delete cookie or token)
   - Invalidate on password change
   - Invalidate all sessions if suspected breach (user changes password, MFA updated)
   - Server-side session store (Redis, database) to track active sessions; don't rely on JWT alone

5. **Session Fixation Prevention**:
   - Regenerate session ID after login (old ID is discarded)
   - Change session ID on privilege escalation (user → admin)
   - Use CSRF tokens to prevent cross-site request forgery

6. **Concurrent Session Limits**:
   - Limit sessions per user (prevent account sharing, reduce compromise impact)
   - Alert user if new login from unexpected location/device

## Anti-Patterns

- Storing session ID in URL (visible in browser history, logs, referer header); **always use cookies or Authorization header**
- Long session timeouts (weeks or months) without refresh token rotation; **short expiry + refresh tokens is safer**
- Storing sensitive data in JWT payload; **JWTs are signed, not encrypted; anyone can read the payload**
- Using client-side session storage (localStorage); **vulnerable to XSS; HTTPOnly cookies are safer for web**
- Not invalidating sessions on logout; **session tokens should be single-use or server-side revocable**

## Further Reading

- OWASP Session Management Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
- JWT.io (JWT libraries and best practices): https://jwt.io/
- RFC 6265 (HTTP State Management): https://tools.ietf.org/html/rfc6265 (cookie specification)
- OAuth 2.0 Security Best Current Practice: https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics
