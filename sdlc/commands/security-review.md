---
description: Deep security review of design and implementation.
argument-hint: "[feature name, component, or system to review]"
---

Conduct a comprehensive security review covering design threats, code vulnerabilities, and dependency risks.

## Steps

1. **Security Secure Coding Review** (`security:secure-coding-review`)
   - Input: Code to review
   - Output: Secure coding violations, best practices

2. **Security OWASP Top 10 Check** (`security:owasp-top-ten-check`)
   - Input: Application features (web/API)
   - Output: OWASP Top 10 risks assessment

3. **Security Dependency Vulnerability Scan** (`security:dependency-vulnerability-scan`)
   - Input: Dependency list
   - Output: CVE scan results, remediation plan

4. **Architect Security Architecture** (`architect:security-architecture`)
   - Input: System design
   - Output: Security architecture, control points, defense in depth

## Output

**Security Review Report** containing:

- Secure coding violations and fixes
- OWASP Top 10 risk assessment
- Dependency vulnerabilities and remediation
- Security architecture approval
- Overall security posture and recommendations

## Example
```

/sdlc:security-review "User data export feature"

→ Code Review: 2 SQL injection risks identified (fixed)
→ OWASP Check: A01 Broken Access Control risk (users can export other users' data)
→ Dependency Scan: 3 high CVEs in xlsx library (upgrade available)
→ Security Architecture: Export should be rate-limited, logged, signed

Output: Security Review Report
Secure Coding: 2 issues found, all fixed
OWASP Risks: A01 Access Control (CRITICAL), A04 Insecure Design (MEDIUM)
Vulnerabilities: 3 high CVEs, 2 medium CVEs (plan to upgrade xlsx)
Architecture Approval: CONDITIONAL (requires rate limiting and audit logging)
Overall: NOT APPROVED — Fix access control issue before deployment

```

## Next Steps

- "Address critical security issues before submitting for quality gate."
- "Submit updated code for re-review."