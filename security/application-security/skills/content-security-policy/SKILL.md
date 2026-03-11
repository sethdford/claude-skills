---
name: content-security-policy
description: Design and deploy Content-Security-Policy (CSP) to prevent XSS attacks and unauthorized resource loading.
---

# Content-Security-Policy

Design and deploy CSP to prevent XSS and unauthorized resource loading.

## Context

You are a senior security engineer implementing CSP for $ARGUMENTS. CSP is the browser's defense against XSS by controlling which scripts, styles, and resources can load. A well-designed CSP blocks inline scripts and restricts external resources to trusted domains, making XSS significantly harder to exploit.

## Domain Context

- **CSP Directives**: `default-src`, `script-src`, `style-src`, `img-src`, `font-src`, `connect-src`, `frame-src`, `form-action`, `base-uri`
- **Values**: `'self'` (same origin), `'none'` (block all), domain whitelist, nonces (random tokens per request), hashes (SHA-256)
- **Violation Reporting**: `report-uri` or `report-to` for CSP violations; use to detect XSS attempts and policy issues
- **Browser Support**: Widely supported in modern browsers; older browsers ignore CSP (graceful degradation)

## Instructions

1. **Start with Report-Only Mode**:
   - Deploy CSP with `Content-Security-Policy-Report-Only` header first
   - Set `report-uri` to collect violations
   - Monitor for 1-2 weeks; fix legitimate violations (misconfigured resources)
   - Then enforce with `Content-Security-Policy` header (report-only + enforcement can coexist)

2. **Design Base Policy**:
   - `default-src 'self'` — allow same-origin resources by default
   - `script-src 'self'` — allow same-origin scripts only (no inline scripts)
   - `style-src 'self'` — allow same-origin styles only (no inline styles)
   - `img-src 'self' data: https:` — allow same-origin, data URIs, and HTTPS images
   - `font-src 'self'` — allow same-origin fonts only
   - `connect-src 'self'` — allow same-origin API calls only

3. **Allow Trusted External Resources**:
   - If you need external CDNs: `script-src 'self' cdn.jsdelivr.net`
   - If you need Google Fonts: `font-src 'self' fonts.googleapis.com; style-src 'self' fonts.googleapis.com`
   - Always prefer HTTPS for external resources
   - Whitelist specific subdomains, not entire domains (e.g., `trusted-cdn.com` not `*.example.com`)

4. **Secure Inline Scripts & Styles**:
   - **Option 1 (Nonces)**: Generate random nonce per request; include in `<script nonce="abc123">` and CSP header
     - `script-src 'nonce-abc123'` — only that script with matching nonce executes
   - **Option 2 (Hashes)**: Hash inline content; include in CSP header
     - `script-src 'sha256-hash'` — only scripts matching hash execute
   - **Option 3 (Refactor)**: Move inline scripts to external files (best practice)
   - Never use `'unsafe-inline'` or `'unsafe-eval'` unless absolutely necessary (defeats XSS protection)

5. **Monitor & Iterate**:
   - Review CSP violations in logs; identify patterns (third-party analytics, ads, etc.)
   - Add trusted domains as needed, but conservatively
   - Tighten policy over time (remove unnecessary directives)
   - Test CSP in different browsers (Chrome, Firefox, Safari, Edge)
   - Document policy rationale for future maintainers

## Anti-Patterns

- Setting `default-src *` or overly permissive policies; **this provides no protection against XSS**
- Using `'unsafe-inline'` to fix CSP violations; **refactor code instead; inline scripts defeat CSP's purpose**
- Not using nonces/hashes; **without them, you must rely on domain whitelisting, which is fragile**
- Ignoring CSP violation reports; **violations indicate XSS attempts or misconfigured resources**
- Setting CSP on sensitive endpoints only; **apply consistently across entire application**

## Further Reading

- Content-Security-Policy Spec: https://w3c.github.io/webappsec-csp/
- OWASP CSP Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html
- MDN CSP Guide: https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP
- CSP Violations Handling: https://developer.mozilla.org/en-US/docs/Web/API/SecurityPolicyViolationEvent
