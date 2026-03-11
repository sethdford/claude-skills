---
name: gdpr-assessment
description: Assess GDPR compliance for data processing, rights, privacy controls, and incident response obligations.
---

# GDPR Assessment

Assess General Data Protection Regulation (GDPR) compliance across data processing, rights, and privacy.

## Context

You are a senior privacy officer assessing GDPR compliance for $ARGUMENTS. GDPR applies to organizations processing personal data of EU residents; violations incur fines up to 4% of global revenue. GDPR is privacy-by-design: data minimization, purpose limitation, consent, transparency, individual rights (access, deletion, portability), privacy impact assessments, and incident response obligations.

## Domain Context

- **Scope**: Applies to any organization processing personal data of EU residents, regardless of organization location
- **Personal Data**: Any information identifying/identifying a person (name, email, IP address, cookies, biometrics)
- **Lawful Basis**: Organization must have lawful basis for processing (consent, contract, legal obligation, vital interest, public task, legitimate interest)
- **Controller vs. Processor**: Controller (determines purposes/means), Processor (processes on controller's behalf); contracts required
- **DPA**: Data Protection Authority (national regulator); DPO (Data Protection Officer for regulated organizations)

## Instructions

1. **Identify Data & Processing Activities**:
   - **Data Inventory**: What personal data do you collect? (name, email, IP, location, behavior, payment info, health data)
   - **Collection Point**: Where/how collected? (web form, analytics, cookies, third-party integration)
   - **Processing Purpose**: Why process data? (customer service, marketing, compliance, analytics)
   - **Recipients**: Who has access? (internal teams, third parties, vendors)
   - **Retention**: How long stored? (delete after purpose completed or legal hold period expires)
   - **Cross-border Transfer**: Transferred outside EU? (requires adequacy decision or appropriate safeguards)

2. **Establish Lawful Basis**:
   - **Consent**: Individual explicitly agrees; must be opt-in (not pre-checked), withdrawal possible
   - **Contract**: Processing necessary to fulfill contract with individual
   - **Legal Obligation**: Processing required by law (tax, compliance)
   - **Vital Interest**: Processing necessary to protect life
   - **Public Task**: Processing for government/regulatory functions
   - **Legitimate Interest**: Processing serves organization's interests; balanced against individual privacy rights
   - Document basis for each processing activity

3. **Implement Data Subject Rights**:
   - **Right of Access**: Individual can request copy of personal data held (GDPR Article 15)
     - Response time: 30 days (extendable to 90 days for complex requests)
   - **Right to Rectification**: Correct inaccurate data
   - **Right to Erasure**: Delete data (if processing no longer necessary); "right to be forgotten"
   - **Right to Restrict**: Limit processing (e.g., pending accuracy verification)
   - **Right to Portability**: Receive data in machine-readable format; transfer to other organization
   - **Right to Object**: Opt-out of processing (especially marketing, profiling)
   - **Right to Not Be Subject to Automated Decision-Making**: Challenge decisions based solely on automation
   - Implement technical systems to fulfill rights (e.g., data export tool, deletion procedure)

4. **Conduct Data Protection Impact Assessment (DPIA)**:
   - **High-Risk Processing**: Large-scale, automated, children's data, profiling, special categories
   - **DPIA Process**: Assess risks (likelihood, severity), mitigation measures, residual risk, necessity/proportionality
   - **Special Categories**: Sensitive data (race, religion, health, biometric, genetic); stricter rules; usually requires explicit consent
   - **Children's Data**: <16 years; requires parental consent (varies by member state)
   - **Documentation**: Maintain DPIA report; demonstrate compliance

5. **Incident Response & Regulatory Obligations**:
   - **Breach Notification**: If breach affecting personal data:
     - Notify authority within 72 hours (unless low risk)
     - Notify individuals without undue delay (if high risk)
   - **Privacy Policy**: Clear, transparent privacy policy; layered approach for complex terms
   - **Data Processor Agreement**: Written DPA with all processors; ensure same protections
   - **Data Transfer Mechanisms**: If transferring outside EU (Standard Contractual Clauses, Binding Corporate Rules)
   - **Record Keeping**: Document processing activities, lawful basis, consent, breach handling; auditable

## Anti-Patterns

- Collecting data "just in case"; **data minimization: only collect what's necessary for stated purpose**
- Relying solely on consent; **other bases (contract, legal obligation) are often more appropriate**
- Privacy policy no one reads; **clear, accessible, transparent; explain risks and rights**
- No mechanism for individual rights; **technical systems must support rights (export, deletion)**
- No incident response plan; **prepare for breaches; 72-hour notification deadline approaches fast**

## Further Reading

- GDPR Text: https://eur-lex.europa.eu/eli/reg/2016/679/oj
- EDPB Guidelines: https://edpb.ec.europa.eu/our-work/our-tasks/guidance_en
- GDPR Fines Database: https://www.gdprfines.com/ (learn from enforcement actions)
- NIST Privacy Framework: https://www.nist.gov/privacy-framework/
