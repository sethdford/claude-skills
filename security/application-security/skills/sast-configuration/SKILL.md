---
name: sast-configuration
description: Configure and deploy Static Application Security Testing (SAST) tools to find vulnerabilities in source code during development.
---

# SAST Configuration

Configure Static Application Security Testing tools to find code vulnerabilities early in development.

## Context

You are a senior security architect implementing SAST for $ARGUMENTS. SAST tools analyze source code without executing it, catching vulnerabilities before deployment.

## Domain Context

- **SAST Tools**: SonarQube, Checkmarx, Semgrep, Fortify, Veracode (commercial), Snyk Code (SaaS), GitHub CodeQL
- **Vulnerability Categories**: Injection flaws, buffer overflows, weak crypto, hardcoded secrets, authentication/authorization bugs
- **Integration Points**: IDE plugins for developers, CI/CD pipeline for automated scanning, artifact repository scanning
- **Tuning**: False positive rates, scan performance, custom rules for organizational patterns

## Instructions

1. **Select SAST Tool**:
   - **Open Source**: Semgrep (flexible, extensible), SonarQube (popular, community edition free)
   - **Commercial**: Checkmarx, Fortify, Veracode (higher accuracy, cost)
   - **Cloud/SaaS**: Snyk Code, GitHub Advanced Security, GitLab SAST
   - Consider: supported languages, integration with your CI/CD, customization needs

2. **Configure Tool**:
   - Install and configure for your tech stack (Java, Python, Go, JavaScript, C++, etc.)
   - Set up custom rules for organizational patterns
   - Define vulnerability severity thresholds
   - Configure to fail builds on Critical/High findings

3. **Integrate into Development**:
   - **IDE Integration**: Developer scanning before commit (Semgrep in IDE, SonarLint)
   - **CI/CD**: Scan on every commit; fail pipeline on security issues
   - **Code Review**: Surface SAST results in pull request/code review tools
   - **Artifact Registry**: Scan dependencies when pulled

4. **Tune for Your Codebase**:
   - Run baseline scan; identify false positives
   - Create custom rules for organizational coding patterns
   - Adjust severity thresholds to balance security/developer friction
   - Establish remediation SLA (Critical: 24 hours, High: 1 week, Medium: sprint)

5. **Measure & Improve**:
   - Track vulnerability trends (are we finding more or fewer vulnerabilities?)
   - Measure remediation rate (what % of findings are fixed?)
   - Collect false positive rate and iterate on rules
   - Annually review tool coverage vs. threat landscape

## Anti-Patterns

- Enabling all SAST rules out-of-the-box; **high false positive rates cause developers to ignore results; start conservative and add rules gradually**
- Running SAST only on main branch; **scan every pull request so developers see issues immediately**
- Treating SAST results as gospel; **SAST finds many false positives; review and categorize findings, don't auto-remediate**
- Not integrating with IDE/CI; **if developers don't see results in their workflow, they won't act on them**
- Never updating rules; **new vulnerability patterns emerge; update rules quarterly based on threat landscape**

## Further Reading

- Semgrep Documentation: https://semgrep.dev/docs/
- SonarQube Community: https://www.sonarqube.org/
- Gartner SAST Magic Quadrant (annually): Vendor comparison and maturity assessment
- OWASP SAST vs. DAST: https://owasp.org/www-community/attacks/Static_vs_Dynamic_Analysis
