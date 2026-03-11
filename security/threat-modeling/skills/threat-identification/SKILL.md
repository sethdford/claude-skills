---
name: threat-identification
description: Systematically identify threats from threat libraries, historical CVEs, and attacker tactics. Use when augmenting STRIDE analysis with known threats from MITRE ATT&CK, CWE, or your industry.
---

# Threat Identification

Systematically catalog threats using threat libraries, industry benchmarks, and historical attack patterns.

## Context

You are a senior security architect identifying threats for $ARGUMENTS using threat libraries and historical attack data. This augments STRIDE with real-world attack patterns and known vulnerabilities.

## Domain Context

- **MITRE ATT&CK Framework**: Adversary Tactics, Techniques, and Procedures (TTPs) used across attack lifecycle (reconnaissance, weaponization, delivery, exploitation, C2, exfiltration, impact)
- **CWE/CVE**: Common Weakness Enumeration (software defects) and Common Vulnerabilities & Exploits (specific instances); identify if your stack has known CWEs
- **Industry-Specific Threats**: Payment processing (PCI-related), healthcare (HIPAA/HITECH), financial services (insider trading, fraud), cloud (misconfiguration, privilege escalation)
- **Historical Attack Chains**: Map how real attacks combined TTPs; e.g., phishing → credential theft → lateral movement → data exfiltration

## Instructions

1. **Profile the Attacker**: Consider attacker types (external opportunists, organized crime, nation-state, insiders). Tailor threat identification to likely adversaries.

2. **Reference MITRE ATT&CK**: Browse the tactic-technique matrix for your industry/platform. Identify which tactics are relevant (e.g., cloud services are vulnerable to "Defense Evasion" via misconfiguration; web apps to "Execution" via injection).

3. **Cross-Reference CWE/CVE**: Check if your tech stack (languages, frameworks, libraries) has known CWEs. Identify high-impact vulnerabilities (e.g., SQL injection, SSRF, XXE for your platform).

4. **Add Industry Threats**: Incorporate threats specific to your vertical (e.g., retail: payment card theft; SaaS: multi-tenant data leakage; cloud: overprivileged IAM roles).

5. **Document Attack Chains**: For high-risk scenarios, map multi-step attacks (e.g., "phishing → credentials → MFA bypass → cloud admin access → data exfiltration").

6. **Connect to STRIDE & Assets**: Link each threat back to STRIDE categories and specific assets (databases, keys, APIs, user data).

## Anti-Patterns

- Using threat libraries as a generic checklist; **every threat must connect to your specific architecture, assets, and attack surface**
- Ignoring insider threats because "we trust our employees"; **disgruntled employees, contractor misconduct, and social engineering inside are real vectors**
- Focusing only on external attacks; **supply chain compromise, third-party access, and cloud service misconfigurations are harder to detect**
- Treating all threats equally; **some CVEs are pre-auth remote code execution; others are post-auth denial of service — prioritize accordingly**
- Skipping the "how" when listing threats; **"SQL injection" is not a threat; "attacker injects SQL to exfiltrate customer PII from order table" is actionable**

## Further Reading

- MITRE ATT&CK: https://attack.mitre.org/
- CWE/CVE: https://cwe.mitre.org/ and https://www.cvedetails.com/
- NIST Cybersecurity Framework (CSF): Maps governance, risk management, and detection/response
- Verizon Data Breach Investigations Report (annual): Real-world attack statistics and patterns
