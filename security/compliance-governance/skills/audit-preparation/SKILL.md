---
name: audit-preparation
description: Prepare for compliance audits by collecting evidence, organizing documentation, and coordinating with auditors.
---

# Audit Preparation

Prepare for compliance audits by organizing evidence and coordinating audit activities.

## Context

You are a senior audit manager preparing for $ARGUMENTS. External audits validate compliance with frameworks (SOC 2, ISO 27001, PCI-DSS, HIPAA) and provide customer assurance. Poor preparation leads to failed audits, failed certifications, and customer trust loss. Well-prepared organizations demonstrate compliance efficiently and professionally.

## Domain Context

- **Audit Types**: External (third-party), Internal (self), Continuous (real-time), Biennial (every 2 years)
- **Audit Process**: Planning → Evidence Collection → On-site Audit → Findings Review → Remediation → Certification
- **Common Findings**: Control gaps (missing control), design deficiency (control exists but poorly designed), operating deficiency (control broken)
- **Remediation**: Implement controls, test, provide evidence; auditors re-test before certification

## Instructions

1. **Establish Audit Timeline & Plan**:
   - **Kickoff**: 6-12 months before audit; engage auditor; define scope
   - **Scoping**: Which systems/processes in scope? (entire org, specific facilities, specific applications)
   - **Engagement**: Fixed timeline; usually 1-3 weeks on-site for comprehensive audits
   - **Remediation**: 3-6 months after audit to implement findings; auditor re-tests
   - **Certification**: Issued after successful remediation
   - **Cost**: Budget for audit fees, remediation costs, internal staff time

2. **Organize Documentation & Evidence**:
   - **Control Narrative**: For each control, documented description of how it operates
   - **Policies**: All relevant policies (access control, incident response, data protection, etc.)
   - **Procedures**: Step-by-step procedures for each control
   - **Evidence Artifacts**: Logs, screenshots, test results, training records proving control operation
   - **Calendar**: Documentation of when controls were tested, who tested, results
   - **Segregation**: Organized by framework requirement (NIST 800-53 family, PCI-DSS requirement, etc.)

3. **Prepare Control Evidence**:
   - **User Access Control**: User provisioning requests, approval workflow, access termination logs
   - **Configuration Management**: Change logs, testing results, approval records
   - **Vulnerability Management**: Scan results, remediation tracking, patch testing
   - **Logging & Monitoring**: Log retention policy, monitoring alerts, incident response logs
   - **Encryption**: Encryption policy, key management procedures, testing results
   - **Incident Response**: Past incidents, investigation files, remediation tracking
   - **Training**: Training records, test results, acknowledgments

4. **Coordinate Audit Activities**:
   - **Audit Liaison**: Designate single point of contact for auditor
   - **Audit Room**: Provide auditor with secure office space, systems access, network access
   - **Interview Scheduling**: Schedule staff interviews; prepare staff on what to expect
   - **Data Provision**: Organize and provide requested logs, reports, test results
   - **Follow-up**: Manage auditor follow-up questions; provide clarifications
   - **Debrief**: Attend findings debrief; understand all findings; discuss remediation

5. **Manage Post-Audit Remediation**:
   - **Findings Categorization**: Prioritize findings by criticality (Critical, High, Medium, Low)
   - **Remediation Plan**: Detailed plan to address each finding; assign owners; set deadlines
   - **Implementation**: Build/fix/configure; test; document evidence
   - **Re-test**: Provide evidence to auditor; auditor re-tests to verify remediation
   - **Certification**: After successful remediation, auditor issues certification
   - **Continuous Improvement**: Post-audit review; lessons learned; process improvements

## Anti-Patterns

- Scrambling at audit time to create evidence; **evidence collection must be ongoing (from control design)**
- Over-documenting (500-page evidence binders); **evidence should be concise, focused on control operation**
- Not understanding control failures; **if auditor finds a gap, understand root cause and fix properly**
- Treating audit as one-time event; **continuous monitoring between audits prevents surprise findings**
- Defensive posture with auditor; **auditors are consultants; collaborate to ensure robust controls**

## Further Reading

- SOC 2 Audit Guide: https://www.aicpa.org/soc
- ISO 27001 Audit Guide: https://www.iso.org/isoiec-27001-information-security-management.html
- PCI-DSS Audit Process: https://www.pcisecuritystandards.org/
- NIST SP 800-53 Assessment Guide: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53Ar5-assessmentprocedures.pdf
