---
name: dast-test-plan
description: Design and execute Dynamic Application Security Testing (DAST) test plans to find runtime vulnerabilities in web applications.
---

# DAST Test Plan

Design and execute dynamic security testing to find runtime vulnerabilities in running applications.

## Context

You are a senior security engineer designing DAST test plans for $ARGUMENTS. DAST tests applications at runtime by sending payloads and analyzing responses, catching vulnerabilities that static analysis misses (authentication logic, business logic, server misconfigurations).

## Domain Context

- **DAST Tools**: Burp Suite, OWASP ZAP, Acunetix, Fortify WebInspect, Rapid7 InsightAppSec, Stackhawk
- **Attack Surface**: HTTP/HTTPS endpoints, APIs, authentication flows, session management, file uploads, redirects
- **Vulnerability Types**: SQL injection, XSS, CSRF, broken authentication, authorization flaws, business logic bugs
- **Environment Requirements**: Disposable test environment (staging or isolated), test data cleanup, approval for security testing

## Instructions

1. **Scope Definition**:
   - Identify all endpoints/workflows to test (authentication flows, user interactions, admin functions)
   - Define out-of-scope areas (payment processing, customer PII) to avoid
   - Create test user accounts and test data
   - Document baseline application behavior (what is "normal"?)

2. **Configure DAST Tool**:
   - Select DAST tool based on application tech stack (Burp for web, ZAP for open-source, Acunetix for enterprise)
   - Configure authentication (provide credentials so scanner can test authenticated endpoints)
   - Set crawl depth and request throttling (avoid DoS-like behavior)
   - Configure SSL/TLS certificate handling for test environment

3. **Execute Scan**:
   - Run baseline crawl to map application attack surface
   - Run active scanning with payloads (SQLi, XSS, command injection, etc.)
   - Test specific workflows: login flow, privilege escalation, file upload, API calls
   - Verify application responds correctly to malicious input (errors, logs, etc.)

4. **Analyze Results**:
   - Review all findings; categorize by severity and accuracy
   - Verify true positives (is the vulnerability real or false positive?)
   - Check for missed coverage (endpoints not scanned, authentication bypass bypassed?)
   - Correlate DAST findings with SAST results

5. **Report & Remediate**:
   - Document reproducible steps for each vulnerability
   - Assign to development team with remediation SLA
   - Verify fixes in retesting
   - Track metrics: total vulnerabilities, time-to-remediation, repeat findings

## Anti-Patterns

- Running DAST on production without approval or safeguards; **always test on staging or isolated environment**
- Scanning without proper authentication context; **many vulnerabilities only surface when authenticated**
- Ignoring false positives and false negatives; **manual verification is essential; DAST has blind spots (business logic bugs)**
- Testing at too-high throttle (making application unavailable); **coordinate with ops; use conservative settings**
- Not cleaning up test data; **test accounts and data should be removed after scanning**

## Further Reading

- OWASP ZAP Guide: https://www.zaproxy.org/docs/
- Burp Suite Methodology: https://portswigger.net/burp/documentation
- OWASP Top 10: https://owasp.org/www-project-top-ten/ (target these in DAST scans)
- NIST SP 800-115: Technical Testing and Assessment guidance
