---
description: Analyze the attack surface to identify exposed components, entry points, and potential attack vectors.
argument-hint: [system name or API endpoint list]
---

# Analyze Attack Surface Command

Chain these steps:

1. Use the `data-flow-diagram-security` skill to identify all entry points: external APIs, user inputs, integrations with third parties, admin interfaces
2. Use the `trust-boundary-analysis` skill to map which components are exposed to untrusted users vs. internal-only
3. Use the `threat-identification` skill to catalog known attack vectors for exposed technologies (e.g., OWASP Top 10 for web apps, MITRE ATT&CK for cloud)
4. Use the `attack-tree-modeling` skill to decompose how attackers could reach critical assets from external entry points
5. Use the `abuse-case-design` skill to identify business logic flaws that could be exploited at each entry point

Deliverables:

- Attack surface diagram showing external vs. internal components
- Inventory of public APIs and their authentication requirements
- List of untrusted input points with input validation requirements
- Attack trees for common entry point exploits
- Prioritized list of attack vectors by accessibility and likelihood

After completion, suggest follow-up commands: `model-threats`, `assess-risk`, `review-api-security`.
