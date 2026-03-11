---
name: threat-library
description: Build and maintain a reusable threat library tailored to your organization, platform, and threat landscape. Use when cataloging threats for future analyses, threat modeling sessions, and architecture reviews.
---

# Threat Library

Create a curated, reusable library of threats relevant to your organization and technology stack.

## Context

You are a senior security architect building a threat library for $ARGUMENTS. A well-maintained threat library accelerates future threat modeling and ensures consistency.

## Domain Context

- **Library Organization**: By STRIDE category, by platform/technology (web app, cloud, mobile), by attack vector (network, social engineering, supply chain), or by attack technique (MITRE ATT&CK)
- **Threat Maturity**: Distinguish between theoretical threats (possible but never observed) and mature threats (known attack patterns, CVEs, public exploits)
- **Customization**: Generic threat libraries exist (OWASP Top 10, MITRE ATT&CK), but organization-specific threats (e.g., "privilege escalation via legacy auth system") are more valuable
- **Versioning & Review**: Threat libraries should be reviewed annually; add new threats as vulnerabilities emerge, remove obsolete threats as mitigations deploy

## Instructions

1. **Define Threat Taxonomy**: Decide how to organize threats:
   - **Option A (STRIDE)**: Organize by threat category; most useful for STRIDE threat modeling
   - **Option B (MITRE ATT&CK)**: Organize by adversary tactic/technique; most useful for defender detection and response
   - **Option C (Technology)**: Organize by platform (web, cloud, mobile, IoT); useful for architecture reviews
   - **Option D (Attack Vector)**: Organize by how threats are introduced (code, network, supply chain, insider); useful for control design

2. **Create Threat Templates**:

   ```
   Threat ID: THREAT-SPOOFING-001
   Name: API Key Compromise
   Category: Spoofing (Identity)
   Description: Attacker obtains valid API key and impersonates legitimate service.
   Attack Preconditions: API key in source code, key shared over unencrypted channel, key used in logs
   Impact: Unauthorized API access, data exfiltration, service abuse
   Likelihood: High (if keys are hard-coded; Low if keys are in secure vault)
   Detection: Unusual API patterns, geographic anomalies, rate limiting violations
   Mitigation: Use credential management system, rotate keys, use short-lived tokens, monitor API usage
   ```

3. **Populate Library from Multiple Sources**:
   - OWASP Top 10 (injection, broken authentication, sensitive data exposure, XXE, broken access control, security misconfiguration, XSS, insecure deserialization, using components with known vulnerabilities, insufficient logging)
   - MITRE ATT&CK (by platform: Windows, macOS, Linux, cloud, mobile)
   - Industry benchmarks (CIS Controls, PCI-DSS, SOC 2)
   - Your incident history (lessons learned from real breaches)
   - Threat intelligence reports (vendor advisories, breach databases, threat actor tactics)

4. **Tailor to Your Stack**:
   - If you use Kubernetes: add container escape, RBAC bypass, CNI vulnerabilities
   - If you process PII: add data exfiltration, insider threats, third-party exposure
   - If you have legacy systems: add exploitation of unpatched software, weak authentication

5. **Maintain the Library**:
   - Review quarterly; add new threats from advisories, remove remediated threats
   - Track threat maturity: "Theoretical" vs. "Known" vs. "Active in wild"
   - Cross-reference with incidents; if a threat manifested, mark it and update likelihood
   - Share with engineering; threat library should inform design reviews and code review guidelines

## Anti-Patterns

- Creating an exhaustive threat library and never updating it; **a stale library becomes useless as your technology and threat landscape evolve**
- Copying OWASP/MITRE wholesale without customization; **generic threats are a starting point; your organization's specific architecture, dependencies, and threat actors may have different threats**
- Library with no clear organization; **if engineers can't find threats in your library during a design review, they'll skip it**
- Threats with no clear mitigations; **a threat list is a compliance checkbox without mitigations; every threat should drive a security requirement**
- Neglecting insider threats or supply chain threats; **these are harder to categorize but often higher impact than commodity cyberattacks**

## Further Reading

- OWASP Top 10 (2021): https://owasp.org/Top10/
- MITRE ATT&CK Framework: https://attack.mitre.org/
- CWE Top 25: https://cwe.mitre.org/top25/
- Verizon DBIR (annual threat landscape report): Real-world threat statistics
- Gartner Critical Capabilities for Security Information & Event Management (SIEM) — threat library coverage metrics
