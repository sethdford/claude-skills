---
name: owasp-top-ten-check
description: Audit application architecture and code against OWASP Top 10 vulnerabilities. Use when assessing application security posture and prioritizing fixes.
---

# OWASP Top Ten Check

Systematically audit applications against the OWASP Top 10 risks.

## Context

You are a senior security architect checking $ARGUMENTS against OWASP Top 10. This provides a baseline security assessment covering the most common and impactful web application risks.

## Domain Context

- **OWASP Top 10 (2021)**: A01-A10 representing consensus on most critical web application security risks
- **Prevalence vs. Impact**: Some risks are common but low-impact; others rare but catastrophic; prioritize by business risk, not prevalence
- **Architecture-Level Risk**: Some OWASP risks (e.g., insecure design) require architectural changes; others (input validation) are code-level

## Instructions

1. **A01: Broken Access Control**
   - Can users access resources they don't own? (files, database records, API endpoints)
   - Can privilege escalation occur? (user → admin, contractor → employee data)
   - Are permissions checked on every action? (not just on page load)
   - Test: Try accessing `/admin`, `/user/{other_user_id}`, deleting someone else's data

2. **A02: Cryptographic Failures**
   - Is sensitive data encrypted in transit (TLS 1.2+) and at rest (AES-256)?
   - Are weak algorithms used? (MD5, SHA1, DES, RC4)
   - Is hashing used for passwords? (Argon2, bcrypt, PBKDF2 with high iteration)
   - Are secrets hardcoded? Logged? Exposed in error messages?

3. **A03: Injection**
   - SQL queries concatenated with input? (test: `' OR '1'='1`)
   - Command injection? (test: `; cat /etc/passwd`)
   - Template injection? LDAP injection? XPath injection?
   - Use parameterized queries; avoid string concatenation with user input

4. **A04: Insecure Design**
   - Were security requirements defined upfront? Threat modeling done?
   - Are there security test cases in the test suite?
   - Are sensitive operations (payments, password resets) protected against abuse?
   - Does the application rate-limit? Implement CAPTCHA for brute force?

5. **A05: Security Misconfiguration**
   - Default credentials still enabled? (admin/admin, test/test)
   - Debugging enabled in production? (verbose error messages, debug endpoints)
   - Unnecessary services running? (old APIs, admin interfaces)
   - Cloud buckets public? Database open to internet?

6. **A06: Vulnerable Components**
   - Are dependencies up-to-date? Use `npm audit`, `pip check`, `cargo audit`
   - Are known CVEs in use? Check NVD, CVE databases
   - Are security patches applied promptly?
   - Is there an SLA for patching high-severity CVEs? (days, not months)

7. **A07: Authentication Failures**
   - Are passwords validated (length, complexity)? Enforced on change?
   - Is MFA/2FA implemented? Enforced for high-privilege accounts?
   - Are sessions secure? (HTTPOnly cookies, CSRF tokens)
   - Is password reset secure? (email verification, time-limited tokens)

8. **A08: Software & Data Integrity Failures**
   - Can attackers upload files? (executable validation, storage outside web root)
   - Is deserialization used? (dangerous; prefer JSON)
   - Are CI/CD pipelines secured? (code signing, artifact verification)
   - Is data integrity verified? (checksums, signatures)

9. **A09: Logging & Monitoring Failures**
   - Are authentication attempts logged? (failed logins, privilege escalation)
   - Are sensitive operations logged? (data access, configuration changes)
   - Are logs protected from tampering and deletion?
   - Is there alerting for suspicious activity? (brute force, unusual access patterns)

10. **A10: SSRF (Server-Side Request Forgery)**
    - Can attackers make the server request internal resources? (metadata services, databases, file systems)
    - Are redirects to user-supplied URLs validated?
    - Is internal IP access blocked at the application level?

## Anti-Patterns

- Treating OWASP Top 10 as exhaustive; **it's a starting point, not a complete security model**
- Fixing A03 (Injection) but ignoring A01 (Broken Access Control); **all 10 are critical**
- Assuming "all projects use HTTPS so A02 is fine"; **data at rest encryption, secret management, and algorithm selection are equally important**
- Creating a checklist and marking boxes; **each item requires testing and verification; understanding why matters more than checking boxes**
- Delaying fixes for "lower-ranked" items; **A04 (Insecure Design) often requires architectural changes; start early**

## Further Reading

- OWASP Top 10 2021: https://owasp.org/Top10/
- OWASP Testing Guide: https://owasp.org/www-project-web-security-testing-guide/
- PortSwigger Web Security Academy: https://portswigger.net/web-security (interactive labs for each OWASP risk)
- CWE/SANS Top 25: https://cwe.mitre.org/top25/ (broader vulnerability perspective)
