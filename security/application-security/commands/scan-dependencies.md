---
description: Scan application dependencies for known vulnerabilities and create remediation roadmap.
argument-hint: [project path or package.json/requirements.txt/pom.xml]
---

# Scan Dependencies Command

Chain these steps:

1. Use `dependency-vulnerability-scan` to scan dependencies and identify known CVEs
2. Use `sast-configuration` to verify your SAST tool catches vulnerable dependency usage patterns
3. Use `security-test-plan` to include dependency vulnerability testing in security test plan

Deliverables:

- SBOM (Software Bill of Materials) with all dependencies and versions
- List of vulnerabilities by severity (Critical, High, Medium, Low)
- Remediation roadmap with patching priorities and timelines
- Dependency update recommendations

After completion, suggest follow-up commands: `test-security`, `review-api-security`.
