---
description: Assess organizational compliance against key regulatory frameworks (GDPR, SOC2, PCI-DSS, ISO 27001).
argument-hint: [framework: gdpr, soc2, pci-dss, hipaa, or iso27001]
---

# Assess Compliance Command

Chain these steps:

1. Use `compliance-mapping` to map organizational controls to selected framework
2. Use `gdpr-assessment` if GDPR applies to your organization
3. Use `soc2-controls` if SOC 2 certification is target
4. Use `pci-dss-review` if payment card data is processed
5. Use `data-classification` to inventory and classify data

Deliverables:

- Compliance gap analysis for selected framework(s)
- Control maturity assessment (not implemented, partial, complete)
- Remediation roadmap with priorities
- Certification timeline estimate

After completion, suggest follow-up commands: `prepare-audit`, `classify-data`.
