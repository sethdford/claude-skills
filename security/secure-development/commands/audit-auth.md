---
description: Audit authentication and authorization implementation for compliance with secure design principles.
argument-hint: [authentication code or system description]
---

# Audit Auth Command

Chain these steps:

1. Use `authentication-design` to review password policies, MFA implementation, and password reset flows
2. Use `authorization-design` to examine role-based access control, permission enforcement, and privilege escalation prevention
3. Use `session-management` to verify secure session handling, token generation, and CSRF protection
4. Use `secure-coding-review` to check auth implementation for secure coding patterns

Deliverables:

- Authentication audit report (password strength, MFA support, password reset security)
- Authorization audit (RBAC/ABAC design, permission enforcement, IDOR prevention)
- Session management assessment (token generation, cookie/JWT configuration, expiry)
- List of gaps and remediation priorities

After completion, suggest follow-up commands: `review-security`, `check-owasp`.
