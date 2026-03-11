---
name: soc2-controls
description: Implement SOC 2 Trust Services Criteria controls for security, availability, processing integrity, confidentiality, and privacy.
---

# SOC 2 Controls

Implement SOC 2 Trust Services Criteria controls across security, availability, and privacy.

## Context

You are a senior trust services architect implementing SOC 2 for $ARGUMENTS. SOC 2 provides third-party assurance that organizations manage customer data securely and reliably. SOC 2 Type I (point-in-time) is quicker; Type II (operating effectiveness) requires 6+ months of evidence. SOC 2 certification is valuable for customer trust and competitive differentiation.

## Domain Context

- **Trust Services Criteria**: Security (CC), Availability (A), Processing Integrity (PI), Confidentiality (C), Privacy (P)
- **Scope**: Which systems/services in scope? Typically SaaS/cloud services
- **Auditor**: Big Four firms (Deloitte, EY, KPMG, PwC) typically audit SOC 2
- **Timeline**: Type I (1-2 weeks audit), Type II (ongoing monitoring + 6-month observation period + audit)
- **Cost**: $10K-$50K+ depending on complexity

## Instructions

1. **Understand Trust Services Criteria (TSC)**:
   - **Security (CC)**: Logical & physical access controls, encryption, vulnerability management, incident response
   - **Availability (A)**: System availability, performance, disaster recovery, business continuity
   - **Processing Integrity (PI)**: Transactions are authorized, recorded, processed, and reported accurately
   - **Confidentiality (C)**: Confidential information is identified, monitored, protected
   - **Privacy (P)**: Personal information collected for stated purposes, with appropriate consent, rights management
   - Select criteria most relevant to your organization (SC = Security & Confidentiality is common for SaaS)

2. **Design & Implement Controls for Security (CC)**:
   - **CC1**: Organization obtains/generates information to support operation of control activities
     - Inventory: Systems, software, data; classified by risk/sensitivity
   - **CC2-CC5**: Information systems configuration, change management, system monitoring
     - Change control process; testing before deployment; rollback procedure
   - **CC6-CC7**: Restriction of access (authentication, authorization, least privilege)
     - Stronger authentication (MFA), role-based access, periodic access review
   - **CC8-CC9**: Encryption, backup, recovery
     - Encryption at rest/transit; regular backups; tested recovery procedures
   - **CC10**: Incident response procedures; logging & monitoring for detection

3. **Design & Implement Controls for Availability (A)**:
   - **A1**: Availability targets; performance monitoring; capacity planning
     - SLA: 99.9% uptime (9 hours downtime/year); monitoring to detect issues
   - **A2**: System monitoring; alerting; incident response
     - Automated alerts for outages, performance degradation
   - **A3**: Disaster recovery plan; RTO (recovery time), RPO (recovery point); tested recovery
     - Test recovery quarterly; document results
   - **A4**: Configuration management; controlled changes; testing before production

4. **Design & Implement Controls for Processing Integrity (PI)**:
   - **PI1**: Processes for accurate/complete transaction processing
     - Validation: Input validation, output verification, reconciliation
   - **PI2**: System performance monitoring; timely/accurate completion of transactions
   - **PI3**: Exception handling; error detection/correction; re-processing
   - **PI4**: Accurate recording/retention of transactions; audit trails
   - **PI5**: Systems designed for integrity; prevent/detect errors

5. **Prepare for SOC 2 Audit**:
   - **Evidence Collection**: Document controls; collect logs, test results, policies
     - For Type II: 6+ months of evidence (logs, monthly test results, incident reports)
   - **Control Testing**: Auditor tests controls; must demonstrate operating effectiveness
     - Prepare: Design walkthroughs, policy reviews, control testing samples
   - **Management Representation**: Executive attestation that controls are designed, implemented, operating effectively
   - **Auditor Coordination**: Liaison; interviews; follow-up questions
   - **Report**: SOC 2 Type I or II report issued; share with customers/prospects

## Anti-Patterns

- Implementing controls only for audit; **SOC 2 controls should reflect actual practices**
- Scripted interviews with auditors; **auditors interview real staff; answer honestly**
- No evidence for claimed controls; **auditors will find control gaps; better to remediate before audit**
- Overly complex control design; **simpler controls are easier to maintain and audit**
- No continuous monitoring post-certification; **controls degrade; monitor continuously**

## Further Reading

- AICPA SOC 2: https://www.aicpa.org/soc
- SOC 2 Criteria: https://www.aicpa.org/soc/trustmanagement/soc-2-trust-service-criteria
- SSAE 18 (SOC 2 Standard): https://www.aicpa.org/caqfaq/category/ssae-18-attest-engagements
- Security & Availability Guide: https://us.aicpa.org/content/dam/aicpaorg/assets/menu/research-exams-guidance/assurance-services/audit-related/soc/downloadabledocuments/soc-2-security-availability-guide.pdf
