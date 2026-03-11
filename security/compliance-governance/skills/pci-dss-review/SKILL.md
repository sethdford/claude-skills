---
name: pci-dss-review
description: Review PCI-DSS compliance for payment card data security across network, systems, and processes.
---

# PCI-DSS Review

Review PCI-DSS compliance for payment card data security.

## Context

You are a senior payment security architect reviewing PCI-DSS compliance for $ARGUMENTS. PCI-DSS (Payment Card Industry Data Security Standard) applies to any organization processing, storing, or transmitting payment card data. Non-compliance results in fines, card data breaches, and reputational damage. PCI-DSS is prescriptive and mandatory (not optional).

## Domain Context

- **Scope**: If handling, storing, or transmitting card data (PAN: Primary Account Number), PCI-DSS applies
- **Card Data**: PAN (16 digits), expiration, CVV/CVC, cardholder name, PIN (encrypted only)
- **Compliance Levels**: Level 1 (>6M txns/year, <1% non-compliant), Level 2-4 (smaller merchants)
- **Validation**: Annual external assessment (penetration test) + quarterly vulnerability scan
- **Card Networks**: Visa, Mastercard, Amex, Discover all enforce PCI-DSS

## Instructions

1. **Understand PCI-DSS Requirements (12 Domains)**:
   - **1-4**: Network Security
     - Firewall configuration, no vendor defaults, separation of systems
   - **5-7**: Systems & Access Control
     - Antivirus, change management, access control, identification/authentication
   - **8-10**: Data Protection & Monitoring
     - Encryption, key management, logging, audit trails
   - **11-12**: Testing & Governance
     - Vulnerability management, penetration testing, policies

2. **Review Network Security (Req 1-4)**:
   - **Requirement 1**: Firewall required; firewall rules documented
     - Deny-by-default; explicitly allow necessary traffic
   - **Requirement 2**: Remove/disable unnecessary services; change vendor defaults
     - Inventory: servers, services, ports; justify each one
   - **Requirement 3**: Network segmentation; card data isolated from internet-facing systems
     - DMZ for internet-facing; separate network for card data systems
   - **Requirement 4**: Encryption in transit (TLS 1.2+); no weak ciphers

3. **Review Systems & Access (Req 5-7)**:
   - **Requirement 5**: Antivirus; regular updates; monitoring for active threats
   - **Requirement 6**: Security patches; secure development practices; security testing
   - **Requirement 7**: Access control; need-to-know basis; restricted access to card data
     - Different roles (merchant, processor, administrator); principle of least privilege
   - Test: Regular access reviews; verify access controls are enforced

4. **Review Data Protection (Req 8-10)**:
   - **Requirement 8**: Unique user IDs; strong passwords (12+ chars, complexity); MFA for remote access
   - **Requirement 9**: Physical security; badge access; camera monitoring; visitor logs
   - **Requirement 10**: Logging & monitoring; 1-year retention (3 months online)
     - Log: User access, administrative actions, failed access attempts
     - Monitor: Logs monitored for suspicious activity; alerting configured

5. **Compliance Assessment & Remediation**:
   - **Self-Assessment Questionnaire (SAQ)**: Merchant completes SAQ; identifies compliance status
   - **Qualified Security Assessor (QSA)**: Third-party assessor conducts formal assessment
   - **Penetration Testing**: Annual external pentest (Level 1 merchants); verify no unauthorized access
   - **Quarterly Vulnerability Scans**: Network scanned for vulnerabilities; remediation tracked
   - **Remediation**: Fix non-compliances; submit evidence to acquiring bank/card network
   - **Attestation**: Acquire bank submits compliance certification to card network

## Anti-Patterns

- Trying to comply without understanding requirements; **requirements are prescriptive; follow them literally**
- Deferring remediation; **compliance is ongoing; address findings promptly**
- Assuming encryption is everywhere; **card data in transit AND at rest must be encrypted**
- No logging/monitoring; **you won't detect fraud or unauthorized access**
- Shared credentials (generic admin account); **unique IDs required for accountability**

## Further Reading

- PCI-DSS v3.2.1 Standard: https://www.pcisecuritystandards.org/documents/PCI_DSS_v3-2-1.pdf
- PCI-DSS Testing Procedures: https://www.pcisecuritystandards.org/documents/PCIDSS_v3-2-1_ASV_Guidance.pdf
- Card Network Compliance: https://www.pcisecuritystandards.org/
- Requirements Mapping (NIST): PCI-DSS maps to NIST SP 800-53 controls
