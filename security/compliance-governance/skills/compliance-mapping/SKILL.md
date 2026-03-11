---
name: compliance-mapping
description: Map security controls to compliance framework requirements (NIST, CIS, ISO 27001, PCI-DSS, HIPAA, GDPR, SOC 2).
---

# Compliance Mapping

Map security controls to compliance framework requirements.

## Context

You are a senior compliance architect mapping controls for $ARGUMENTS. Organizations must comply with multiple frameworks (NIST, PCI-DSS, HIPAA, GDPR, SOC 2, ISO 27001); mapping ensures controls address requirements, prevents gaps, and demonstrates compliance. Mapping is foundational for audit preparation and certification.

## Domain Context

- **Frameworks**: NIST SP 800-53 (government), CIS Controls (industry standard), ISO 27001 (international), PCI-DSS (payment card), HIPAA (health), GDPR (privacy), SOC 2 (trust services)
- **Control Hierarchy**: Policies → Procedures → Technical Controls; each level implements framework requirements
- **Maturity Levels**: Control maturity (ad-hoc, repeatable, defined, optimized); frameworks assess maturity
- **Audit**: External auditors verify controls map to requirements and are functioning

## Instructions

1. **Identify Applicable Frameworks**:
   - **NIST SP 800-53**: Government contractors, critical infrastructure
   - **CIS Controls**: Universal baseline (applicable to all organizations)
   - **ISO 27001**: International standard; third-party certification available
   - **PCI-DSS**: Payment card processing organizations
   - **HIPAA**: Health information
   - **GDPR**: EU data processing
   - **SOC 2 Type I/II**: Service organizations; customer trust assurance
   - Document applicability rationale (regulatory requirement, customer requirement, industry standard)

2. **Map Controls to Framework Requirements**:
   - **Control Catalog**: Document all security controls (policies, procedures, technical controls)
   - **Framework Requirements**: For each framework, list all requirements
   - **Mapping Table**: Create matrix mapping controls to requirements (one control may address multiple requirements)
   - **Gap Identification**: Identify requirements with no corresponding control; prioritize implementation
   - **Redundancy**: Identify overlapping controls; consolidate where appropriate

3. **Document Control Implementation**:
   - **Policy**: Written policy defining requirement
   - **Procedure**: Step-by-step procedure for implementation
   - **Evidence**: Documentation, logs, screenshots proving control is operating
   - **Responsibility**: Owner (who ensures control operates?)
   - **Testing**: How is control validated? (audit, test, monitoring)

4. **Plan Remediation for Gaps**:
   - **Severity Assessment**: Critical gaps (high risk, customer requirement) vs. Medium/Low
   - **Implementation Plan**: Detailed plan to implement missing controls
   - **Timeline**: When will control be implemented? (Critical: <30 days)
   - **Resource Allocation**: Who owns implementation? What resources needed?
   - **Validation**: How will you verify control is operating post-implementation?

5. **Maintain Mapping Over Time**:
   - **Annual Review**: Frameworks evolve; review mapping annually
   - **Control Updates**: When control changes, update mapping
   - **New Frameworks**: If organization enters new regulated market, add frameworks
   - **Audit Readiness**: Maintain evidence of control operation (logs, testing results); provide to auditors

## Anti-Patterns

- Mapping controls without understanding requirements; **misalignment causes failed audits**
- Assuming one control covers multiple requirements (false negatives); **verify each requirement is covered**
- Creating redundant controls; **consolidate; reuse controls across frameworks**
- Mapping controls that don't exist (paper controls); **controls must be implemented and functioning**
- No evidence collection; **auditors require proof of control operation; plan evidence collection from the start**

## Further Reading

- NIST SP 800-53 (Security Controls): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- CIS Controls: https://www.cisecurity.org/cis-controls/
- ISO 27001 Standard: https://www.iso.org/isoiec-27001-information-security-management.html
- PCI-DSS: https://www.pcisecuritystandards.org/
- NIST Compliance Framework Mapping: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
