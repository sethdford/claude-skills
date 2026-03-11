---
description: Identify and document trust boundaries in the architecture, showing where privilege levels, security contexts, or threat models change.
argument-hint: [system architecture or component list]
---

# Map Trust Boundaries Command

Chain these steps:

1. Use the `data-flow-diagram-security` skill to identify all system components and the data flows between them
2. Use the `trust-boundary-analysis` skill to identify where privilege levels, security contexts, or authority changes occur
3. Use the `stride-analysis` skill to focus STRIDE analysis on threats that cross trust boundaries (highest-risk locations)
4. Use the `abuse-case-design` skill to identify how attackers could cross or bypass trust boundaries (e.g., privilege escalation, lateral movement)
5. Document control requirements at each boundary: authentication, authorization, encryption, integrity, logging, error handling

Deliverables:

- Architecture diagram with trust boundaries clearly marked
- Trust zone definitions (External, DMZ, Internal, Admin, etc.)
- Control matrix showing authentication, authorization, encryption, logging per boundary
- List of privilege escalation and lateral movement risks
- Recommendations for boundary hardening (mTLS, network segmentation, audit logging)

After completion, suggest follow-up commands: `model-threats`, `review-iam`, `audit-cloud`.
