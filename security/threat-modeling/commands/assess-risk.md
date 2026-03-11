---
description: Quantify organizational risk from identified threats using likelihood, impact, and risk scoring methodologies.
argument-hint: [threat list or risk register]
---

# Assess Risk Command

Chain these steps:

1. Use the `asset-inventory` skill to confirm what critical assets are at stake and their business value
2. Use the `threat-identification` skill to verify threats are documented with realistic attack scenarios
3. Use the `risk-scoring` skill to quantify each threat with likelihood and impact, generating risk ratings
4. Use the `attack-tree-modeling` skill to estimate attacker effort and cost, informing likelihood assessment
5. Synthesize findings into a risk register: list all threats, their scores, and recommended actions (mitigate, accept, transfer, avoid)

Deliverables:

- Risk register with all identified threats ranked by severity
- Risk scoring matrix showing likelihood vs. impact
- Executive summary of top 5 critical risks and business impact
- Mitigation roadmap with priorities and timelines
- Risk acceptance documentation for medium/low-risk items

After completion, suggest follow-up commands: `model-threats`, `map-trust-boundaries`, `respond-to-incident` (if incidents discovered).
