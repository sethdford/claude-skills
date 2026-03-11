---
name: data-classification
description: Classify organizational data by sensitivity level and define handling, storage, and access requirements.
---

# Data Classification

Classify organizational data by sensitivity and define appropriate handling requirements.

## Context

You are a senior data governance architect designing data classification for $ARGUMENTS. Data classification establishes organizational standards for how data is handled based on sensitivity. Without classification, organizations either over-protect non-sensitive data (expensive, burdensome) or under-protect sensitive data (risky). Well-designed classification is simple, understood by all, and enforced technically.

## Domain Context

- **Classification Levels**: Public, Internal, Confidential, Restricted (varies by organization)
- **Drivers**: Regulatory (GDPR, HIPAA, PCI-DSS), contractual (customer agreements), competitive (trade secrets)
- **Handling Requirements**: Different levels require different encryption, access control, retention, destruction standards
- **Enforcement**: Technical controls (DLP tools, encryption, access control) enforce classification
- **Responsibility**: Data owners assign classification; stewards maintain; custodians enforce

## Instructions

1. **Define Classification Levels**:
   - **Public**: No restrictions; can be shared externally; loss has no impact
     - Examples: Marketing materials, public documentation, press releases
     - Handling: No encryption required; can be accessed by anyone
   - **Internal**: Within organization only; loss has limited impact
     - Examples: Internal policies, team wikis, internal communications
     - Handling: Not encrypted; access limited to employees; not shared externally
   - **Confidential**: Restricted access; loss has significant impact
     - Examples: Customer data, financial records, contracts, employee records
     - Handling: Encrypted at rest/transit; access restricted to need-to-know; audit logging
   - **Restricted**: Highest sensitivity; loss has severe impact
     - Examples: Health records (HIPAA), payment card data (PCI-DSS), trade secrets
     - Handling: Encryption + additional controls (MFA, separation of duties, segregated systems); minimal access; extensive logging

2. **Assign Classification**:
   - **Data Owner**: Business unit leader determines sensitivity; assigns classification
   - **Classification Criteria**:
     - Regulatory: Is data regulated? (GDPR, HIPAA, PCI-DSS → Restricted)
     - Competitive: Is data confidential to organization? (Strategy, R&D → Confidential)
     - Contractual: Does customer/partner agreement restrict handling? (Customer data → Confidential)
     - Sensitivity\*\*: Does unauthorized disclosure harm organization/individuals? (Personal data → Confidential/Restricted)
   - **Documentation**: Document rationale for classification; review annually

3. **Define Handling Requirements Per Level**:
   - **Storage**:
     - Public: Any system
     - Internal: Corporate systems only
     - Confidential: Encrypted storage; access-controlled systems
     - Restricted: Highly secured systems; air-gapped if required
   - **Transmission**:
     - Public: Plain HTTP acceptable
     - Internal: HTTPS required
     - Confidential/Restricted: TLS 1.2+; encrypted end-to-end
   - **Access**:
     - Public: Open
     - Internal: Employees only
     - Confidential: Need-to-know; documented approval
     - Restricted: Minimal access; multi-factor authentication
   - **Retention**:
     - Public: No retention requirement
     - Internal: Organizational retention (typically 1-3 years)
     - Confidential/Restricted: Legal holds (5-7 years); secure deletion after retention expires
   - **Sharing**: Defines who can receive data (internal only, customer, third parties, public)

4. **Implement Technical Enforcement**:
   - **Data Loss Prevention (DLP)**: Tools scan for classified data; prevent exfiltration
   - **Encryption**: Automatically encrypt Confidential/Restricted data at rest and transit
   - **Access Controls**: Grant access based on classification; audit access
   - **Watermarking**: Mark documents as classified (in footers, headers)
   - **Monitoring**: Alert on suspicious access or movement of restricted data

5. **Maintain Classification**:
   - **Training**: All employees understand classification; receive training annually
   - **Audits**: Periodic audit of classification accuracy; verify enforcement
   - **Evolution**: Update classification as business/threat landscape changes
   - **Exceptions**: Document and justify any exceptions to handling requirements
   - **Reporting**: Metrics on classified data volume, trends, enforcement

## Anti-Patterns

- Over-classifying (everything is "Confidential"); **wastes resources; dilutes urgency**
- Under-classifying (sensitive data is "Internal"); **leaves critical data under-protected**
- Classification without enforcement; **if not enforced, classification is useless**
- No training; **employees don't understand classification; mishandle data**
- Classification never changes; **business evolves; classification must evolve**

## Further Reading

- NIST SP 800-188 (Data Classification): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-188.pdf
- ISO 27001 Classification: https://www.iso.org/isoiec-27001-information-security-management.html
- SANS Data Classification Guide: https://www.sans.org/security-resources/policies/data-classification/
- DLP Best Practices: Gartner DLP reports
