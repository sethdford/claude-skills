---
name: web-security-headers
description: Configure security HTTP headers to mitigate XSS, clickjacking, MIME sniffing, and other browser-based attacks.
---

# Web Security Headers

Configure HTTP security headers to mitigate browser-based attacks.

## Context

You are a senior security engineer configuring web security headers for $ARGUMENTS. Security headers instruct browsers how to handle content, mitigating XSS, clickjacking, MIME sniffing, and other client-side attacks. Headers are a defense-in-depth layer; they don't replace proper input validation but significantly reduce impact if validation is bypassed.

## Domain Context

- **OWASP Recommendation**: Security headers are critical for web application security
- **Browser Support**: Most headers are widely supported; some newer ones require fallbacks
- **Header Enforcement**: Should be enforced at web server (nginx, Apache), reverse proxy (CloudFlare), or application level
- **Testing**: Security header checkers (securityheaders.com, Mozilla Observatory) provide grading and guidance

## Instructions

1. **Implement Critical Headers**:
   - **Content-Security-Policy (CSP)**: Restrict script sources (prevents inline script injection)
     - `default-src 'self'; script-src 'self' trusted-cdn.com; style-src 'self' fonts.googleapis.com`
     - Gradually tighten by removing `'unsafe-inline'` and `'unsafe-eval'`
   - **X-Content-Type-Options**: Prevent MIME sniffing
     - `X-Content-Type-Options: nosniff`
   - **X-Frame-Options**: Prevent clickjacking
     - `X-Frame-Options: DENY` (or `SAMEORIGIN` if embedding is necessary)
   - **Strict-Transport-Security (HSTS)**: Force HTTPS
     - `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`

2. **Implement Additional Headers**:
   - **X-XSS-Protection**: Legacy XSS filter (older browsers; CSP is modern approach)
     - `X-XSS-Protection: 1; mode=block`
   - **Referrer-Policy**: Control what referrer information is sent
     - `Referrer-Policy: strict-origin-when-cross-origin`
   - **Permissions-Policy** (formerly Feature-Policy): Restrict browser APIs
     - `Permissions-Policy: geolocation=(), microphone=(), camera=()`
   - **X-Permitted-Cross-Domain-Policies**: Restrict cross-domain Flash/PDF access
     - `X-Permitted-Cross-Domain-Policies: none`

3. **Configure Content-Security-Policy (CSP) Properly**:
   - Start with report-only mode: `Content-Security-Policy-Report-Only: ...`
   - Gradually tighten by removing `'unsafe-inline'` and `'unsafe-eval'`
   - Use nonces for inline scripts: `<script nonce="random-value">`
   - Set `report-uri` to collect CSP violations: `report-uri https://security.example.com/csp-report`
   - Monitor violations; iterate on policy

4. **Test & Validate Headers**:
   - Use curl to verify headers: `curl -I https://example.com`
   - Check all pages (homepage, login, API responses) for header consistency
   - Use Mozilla Observatory: https://observatory.mozilla.org/
   - Use securityheaders.com for A/B comparison with peers

5. **Maintain Headers**:
   - Document why each header is present (rationale, threats mitigated)
   - Review headers quarterly (new headers, browser capability changes)
   - Monitor CSP violations; adjust policy based on legitimate violations
   - Test header behavior in supported browsers (Chrome, Firefox, Safari, Edge)

## Anti-Patterns

- Setting overly permissive CSP (e.g., `default-src *`); **this disables CSP's protection**
- Using CSP alone without input validation; **headers are defense-in-depth; validation is primary defense**
- Setting HSTS for a short duration; **use 1-2 years minimum (31536000 seconds); long duration prevents accidental downgrade**
- Not testing CSP before enforcing; **report-only mode is essential to catch legitimate violations before breaking functionality**
- Adding `'unsafe-inline'` to workaround CSP violations; **refactor code instead (use external scripts, event listeners)**

## Further Reading

- OWASP Secure Headers Project: https://owasp.org/www-project-secure-headers/
- MDN Web Security Headers: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers
- Content-Security-Policy Spec: https://w3c.github.io/webappsec-csp/
- Strict-Transport-Security Preload: https://hstspreload.org/
