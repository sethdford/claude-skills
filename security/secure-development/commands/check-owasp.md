---
description: Check application against OWASP Top 10 and identify gaps in critical security controls.
argument-hint: [application name or codebase]
---

# Check OWASP Command

Chain these steps:

1. Use `owasp-top-ten-check` to assess all 10 OWASP risk categories
2. Use `input-validation-patterns` to verify A03 (Injection) controls
3. Use `output-encoding` to verify A07 (XSS) controls
4. Use `authentication-design` to verify A07 (Authentication Failures)
5. Use `authorization-design` to verify A01 (Broken Access Control)
6. Use `cryptography-selection` to verify A02 (Cryptographic Failures)

Deliverables:

- OWASP Top 10 assessment matrix showing compliance per risk
- Prioritized list of gaps (A01-A10) with business impact
- Remediation roadmap with effort estimates
- Test cases for verifying fixes

After completion, suggest follow-up commands: `review-security`, `scan-dependencies`.
