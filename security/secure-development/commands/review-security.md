---
description: Conduct a comprehensive security code review examining OWASP Top 10, secure coding patterns, input validation, and cryptography.
argument-hint: [code files or codebase path]
---

# Review Security Command

Chain these steps:

1. Use `secure-coding-review` to audit code for secure coding practices and common vulnerabilities
2. Use `owasp-top-ten-check` to verify protection against OWASP Top 10 risks
3. Use `input-validation-patterns` to examine input handling and validation logic
4. Use `output-encoding` to verify proper output encoding for XSS prevention
5. Use `cryptography-selection` to review any cryptographic operations for correct algorithms and parameters
6. Use `secrets-management` to ensure no secrets are hardcoded or exposed in logs

Deliverables:

- Security code review report with findings by severity (Critical, High, Medium, Low)
- List of OWASP Top 10 gaps with remediation recommendations
- Input/output encoding audit results
- Cryptography assessment
- Secrets scanning results (hardcoded keys, exposed tokens)

After completion, suggest follow-up commands: `audit-auth`, `check-owasp`.
