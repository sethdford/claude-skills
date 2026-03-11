---
description: Execute comprehensive security testing including SAST, DAST, and penetration testing.
argument-hint: [application URL or codebase path]
---

# Test Security Command

Chain these steps:

1. Use `sast-configuration` to run static analysis on source code
2. Use `dast-test-plan` to design and execute dynamic testing against running application
3. Use `security-test-plan` to execute functional security testing
4. Use `penetration-test-scope` to define scope for penetration testing

Deliverables:

- SAST scan results with vulnerabilities and remediation
- DAST scan results including injection, authentication, and logic flaws
- Security test execution report
- Penetration test findings (if applicable)

After completion, suggest follow-up commands: `review-api-security`, `scan-dependencies`.
