# Secure Code Review Template

## Review Metadata

**Feature**: [Name of feature being reviewed]

**PR/Commit**: [Link to code]

**Reviewer**: [Name and date]

**Components Reviewed**: [List files, modules, or services touched]

---

## OWASP Top 10 Review Checklist

### A01 - Broken Access Control

**Questions to Ask**:

- Are authorization checks performed before sensitive operations?
- Can users access data they shouldn't?
- Are privilege levels enforced consistently?
- Can a user escalate privileges?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A02 - Cryptographic Failures

**Questions to Ask**:

- Is sensitive data encrypted in transit (HTTPS/TLS)?
- Is sensitive data encrypted at rest?
- Are secure hashing algorithms used (bcrypt/scrypt, not MD5/SHA1)?
- Are encryption keys managed securely (never hardcoded)?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A03 - Injection

**Questions to Ask**:

- Could user input be injected into SQL queries?
- Could user input cause command injection (shell execution)?
- Could user input cause XXE (XML External Entity) attacks?
- Are parameterized queries used for all database operations?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A04 - Insecure Design

**Questions to Ask**:

- Are there missing threat model considerations?
- Is rate limiting implemented for sensitive endpoints?
- Are there controls to prevent brute force attacks?
- Is the design resilient to common attack patterns?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A05 - Security Misconfiguration

**Questions to Ask**:

- Are debug/verbose logging flags disabled in production?
- Are security headers configured (CSP, HSTS, X-Frame-Options)?
- Are unnecessary services or ports exposed?
- Are defaults secure (fail-closed, not fail-open)?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A06 - Vulnerable and Outdated Components

**Questions to Ask**:

- Are dependencies up to date?
- Are known vulnerabilities present in dependencies?
- Are security patches applied promptly?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A07 - Authentication & Session Management

**Questions to Ask**:

- Are passwords hashed with strong algorithms?
- Are sessions properly invalidated on logout?
- Are session tokens secure (httpOnly, Secure flags)?
- Is MFA/2FA considered for sensitive operations?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A08 - Software & Data Integrity Failures

**Questions to Ask**:

- Are software updates validated before installation?
- Are dependencies from trusted sources?
- Is data integrity verified (checksums, signatures)?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A09 - Logging & Monitoring

**Questions to Ask**:

- Are security-relevant events logged (auth, access control, errors)?
- Are logs protected from tampering/deletion?
- Are secrets/PII excluded from logs?
- Is there alerting for suspicious activity?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

### A10 - SSRF (Server-Side Request Forgery)

**Questions to Ask**:

- Does code make requests to external/internal URLs based on user input?
- Are requests validated/restricted (e.g., no requests to internal IPs)?
- Is URL parsing done securely?

**Findings**:

- [ ] No findings
- [ ] Low severity findings: [List findings]
- [ ] Medium severity findings: [List findings]
- [ ] Critical/High severity findings: [List findings]

---

## Summary of Findings

| Severity | Count | Details |
| -------- | ----- | ------- |
| Critical | [ ]   | [List]  |
| High     | [ ]   | [List]  |
| Medium   | [ ]   | [List]  |
| Low      | [ ]   | [List]  |

---

## Recommended Actions

**Before Merge**:

- [ ] All Critical/High findings addressed
- [ ] Code re-reviewed after fixes

**Follow-up Issues**:

- [ ] [Issue 1]: [Brief description, optional]
- [ ] [Issue 2]: [Brief description, optional]

---

## Reviewer Notes

[Additional context, risk assessment, or recommendations]

---

## Sign-Off

**Status**: [ ] Approved [ ] Approved with Minor Fixes [ ] Blocked - Resubmit

**Reviewer**: ******\_\_\_\_****** **Date**: ******\_\_\_\_******
