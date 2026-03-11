---
name: security-test-plan
description: Develop comprehensive security test plans covering functional security, vulnerability scanning, and attack scenarios.
---

# Security Test Plan

Develop comprehensive test plans that validate security controls and find vulnerabilities.

## Context

You are a senior security engineer designing security test plans for $ARGUMENTS. A well-designed test plan covers multiple testing methodologies (static, dynamic, manual), targets high-risk functions (authentication, authorization, data handling), and verifies both positive (access granted) and negative (access denied) cases.

## Domain Context

- **Testing Types**: Unit security tests (input validation), integration tests (auth flows), system tests (end-to-end), penetration tests (attack scenarios)
- **Test Coverage**: Authentication, authorization, encryption, logging, error handling, business logic
- **Test Cases**: Positive (expected access), negative (denied access), edge cases (boundary values), error cases (failures)
- **Automation**: Unit and integration tests automated in CI/CD; manual penetration tests after features are complete

## Instructions

1. **Define Test Scope**:
   - Identify high-risk features (authentication, payment, admin functions, data export)
   - List security properties to test (confidentiality, integrity, authenticity, non-repudiation, availability)
   - Determine test environment (development, staging, or dedicated security lab)
   - Allocate testing time (security testing is a percentage of overall QA effort)

2. **Design Security Test Cases**:
   - **Authentication**: Valid login, invalid credentials, disabled accounts, session expiry, password reset flow
   - **Authorization**: User access control (can user X access resource Y?), privilege escalation attempts, cross-tenant access
   - **Data Handling**: Encryption at rest/transit, data masking in logs, error messages (no sensitive data), secure deletion
   - **Input Validation**: SQL injection, XSS, command injection, buffer overflow, XML injection, path traversal
   - **Business Logic**: State transitions (can order be approved without payment?), workflow logic, duplicate transactions

3. **Implement Automated Tests**:
   - Write unit tests for input validation functions
   - Write integration tests for authentication/authorization flows
   - Automate SAST and DAST in CI/CD pipeline
   - Include negative test cases (invalid input, access denied)
   - Run automated tests on every commit

4. **Plan Manual Testing**:
   - Penetration testing (attack scenarios, privilege escalation, business logic flaws)
   - Exploratory testing (find unexpected behaviors)
   - Usability of security features (are users protected despite complexity?)
   - Testing with real-world data (if available in staging)

5. **Track & Report Results**:
   - Record pass/fail status and evidence (screenshots, logs, reproduction steps)
   - Categorize failures by severity and component
   - Track remediation (which failures are fixed?)
   - Report metrics: test coverage %, vulnerability density, time-to-remediation

## Anti-Patterns

- Only testing "happy path" (valid input, authorized access); **security testing is about breaking assumptions**
- Relying solely on automated scanning; **manual testing finds business logic flaws that scanners miss**
- Testing after features are "done"; **security should be tested continuously during development**
- Ignoring error paths; **error messages often leak sensitive information; test error handling**
- Not retesting after fixes; **verify that remediation actually works; regression test other features**

## Further Reading

- OWASP Testing Guide: https://owasp.org/www-project-web-security-testing-guide/
- NIST SP 800-53 (Security and Privacy Controls): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- CWE Top 25: https://cwe.mitre.org/top25/ (prioritize testing for these)
- OWASP Top 10: Focus security testing on these vulnerability categories
