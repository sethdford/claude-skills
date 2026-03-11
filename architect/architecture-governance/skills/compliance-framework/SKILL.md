---
name: compliance-framework
description: Implement compliance requirements (SOC2, GDPR, HIPAA). Design architecture for regulations. Map technical controls to compliance requirements. Use when building regulated systems.
---

# Compliance Framework

Design systems that meet regulatory requirements and establish continuous compliance monitoring.

## Context

You are implementing compliance for regulated systems. Map regulations to technical controls. Design for audit readiness. Read requirements, existing controls, certification timelines.

## Domain Context

Based on compliance frameworks and regulatory standards:

- **SOC2**: Security, availability, processing integrity, confidentiality. Requires audit trail, access control, encryption.
- **GDPR**: Protects EU citizens' personal data. Requires consent, data portability, right-to-be-forgotten, breach notification.
- **HIPAA**: Health information privacy (US). Requires encryption, audit logs, access controls, business associate agreements.
- **PCI DSS**: Payment card data protection. Requires segmentation, encryption, monitoring, vendor management.

## Instructions

1. **Identify Applicable Standards**: Which regulations apply? GDPR (EU users)? HIPAA (health data)? SOC2 (enterprise customers)? PCI DSS (payment processing)?

2. **Map Controls to Architecture**: For each regulation, what technical controls needed? GDPR: encryption at rest/transit, audit logs, consent tracking. HIPAA: role-based access, encrypted backups, breach detection.

3. **Design for Audit**: Audit logs must be immutable, encrypted, sent to separate system. Log all data access, configuration changes, admin actions. Retention per regulation (GDPR: 3 years minimum).

4. **Build Operational Processes**: Change management: approve all changes, test in staging, audit trail. Incident response: detect, contain, notify (GDPR: 72 hours). Annual training on compliance.

5. **Plan for Verification**: Audit readiness: document controls, gather evidence. Penetration testing annually. Vulnerability scanning continuous. Third-party assessments (SOC2, HIPAA).

## Anti-Patterns

- **Compliance as Afterthought**: Build system, then add compliance controls. Result: hard to retrofit, costly. **Guard**: Design for compliance from start; embed controls in architecture.
- **Over-Compliance**: Implement controls for regulations you don't need. Result: cost, complexity. **Guard**: Identify exact requirements; implement only what's needed.
- **No Automation**: Manual evidence gathering for audits. Result: slow, error-prone. **Guard**: Automate log collection, evidence gathering, control testing.
- **Forgotten After Certification**: Achieve compliance, then relax. Result: drift, recertification failure. **Guard**: Continuous monitoring; treat compliance as ongoing, not one-time.

## Further Reading

- _SOC2 Compliance_ — security audit framework for service providers
- _GDPR Compliance_ — European data protection regulation
- _HIPAA Security Rule_ — health information protection (US)
- _Compliance is Not Security_ by James Ranall — compliance mindset and culture
