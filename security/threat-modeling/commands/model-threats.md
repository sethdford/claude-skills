---
description: Conduct comprehensive threat modeling using STRIDE, attack trees, and risk scoring on a system design or architecture.
argument-hint: [system name, brief architecture description]
---

# Model Threats Command

Chain these steps:

1. Use the `data-flow-diagram-security` skill to map all data flows, storage, and trust boundaries in the system
2. Use the `asset-inventory` skill to enumerate all critical assets and their value to the organization
3. Use the `stride-analysis` skill to systematically identify threats across all six categories (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege)
4. Use the `threat-identification` skill to augment STRIDE analysis with real-world threat patterns from MITRE ATT&CK, CWE/CVE, and industry-specific threat libraries
5. Use the `risk-scoring` skill to quantify likelihood and impact, then prioritize threats by risk level
6. Use the `attack-tree-modeling` skill to decompose the highest-risk threats into attack chains, estimating attacker effort and cost

Deliverables:

- Threat model document with STRIDE analysis per component
- Attack trees for top 3-5 high-risk threats
- Asset inventory with criticality ratings
- Risk register sorted by severity (Critical, High, Medium, Low)
- Mitigation roadmap (immediate, quarter, year)

After completion, suggest follow-up commands: `analyze-attack-surface`, `assess-risk`, `map-trust-boundaries`.
