---
name: security-policy-template
description: Develop organization-wide security policies covering access control, data handling, incident response, and vendor management.
---

# Security Policy Template

Develop comprehensive security policies covering organization-wide requirements.

## Context

You are a senior security policy architect developing policies for $ARGUMENTS. Security policies establish organization-wide standards, assign responsibilities, and define consequences. Well-designed policies are clear, enforceable, and aligned with compliance frameworks. Policies without teeth are ineffective; policies that are too burdensome are circumvented.

## Domain Context

- **Policy Types**: Information Security Policy (overarching), Access Control, Data Classification, Incident Response, Business Continuity, Vendor Management
- **Governance**: Policies approved by executive committee; version controlled; reviewed annually
- **Enforcement**: Policies must have consequences (discipline, access revocation); enforcement inconsistency undermines policy
- **Awareness**: Employees must understand policies; training and acknowledgment required

## Instructions

1. **Define Policy Framework**:
   - **Overarching Policy**: Information Security Policy (high-level intent, roles/responsibilities, compliance alignment)
   - **Access Control Policy**: User access provisioning, approval, termination, privilege escalation
   - **Data Classification Policy**: How to classify data (public, internal, confidential, restricted); handling requirements per level
   - **Incident Response Policy**: How to detect, investigate, contain, and recover from incidents
   - **Business Continuity Policy**: Recovery time objectives (RTO), recovery point objectives (RPO), testing requirements
   - **Vendor Management Policy**: Third-party risk assessment, contract requirements, audit rights

2. **Structure Each Policy**:
   - **Purpose**: Why the policy exists (link to compliance/business goals)
   - **Scope**: Who does it apply to? (employees, contractors, third parties)
   - **Policy Statement**: Specific requirements (e.g., "All systems must have MFA enabled")
   - **Responsibility**: Who ensures compliance? (role, department)
   - **Enforcement**: Consequences for non-compliance (varies by severity)
   - **Procedures**: Step-by-step procedures for implementation
   - **Approval**: Approved by executive, board, or compliance committee
   - **Effective Date & Review Cycle**: When effective, when next reviewed

3. **Develop Core Policies**:
   - **Access Control**:
     - Provision: Manager approval required; right of access granted based on job function
     - Approval Workflow: Documented, auditable approval process
     - Termination: Same-day access removal upon departure
     - MFA Required: For all remote access, administrative access
   - **Data Classification**:
     - Public: No restrictions; can be shared externally
     - Internal: Within organization only
     - Confidential: Restricted access; encryption required
     - Restricted: Highest sensitivity; access controls, audit logging, segregation required
   - **Incident Response**:
     - Detection: How to identify incidents (alerts, reports)
     - Notification: Who to notify (CISO, incident commander, executives)
     - Investigation: Forensic preservation, root cause analysis
     - Communication: External notification timeline (regulators, customers, media)
     - Recovery: Restore systems, verify integrity, post-incident review

4. **Enforcement & Governance**:
   - **Accountability**: Clear responsibility for policy compliance
   - **Consequences**: Documented consequences (warning, suspension, termination) for violations
   - **Escalation**: Clear escalation path for violations
   - **Annual Review**: Review policies annually for relevance, effectiveness, compliance alignment
   - **Training**: Mandatory training for all employees; document acknowledgment

5. **Maintain Policies**:
   - **Version Control**: Track policy versions; history of changes
   - **Approval Process**: New/updated policies require executive approval
   - **Communication**: Announce policy changes; training on new policies
   - **Assessment**: Periodic assessment of policy compliance (audits, surveys)
   - **Adjustment**: Update policies based on assessments, incidents, framework changes

## Anti-Patterns

- Policies written by IT without business input; **policies must align with business needs**
- Policies no one knows about; **must be published, trained, acknowledged**
- Policies with no enforcement; **unenforced policies are worthless**
- Policies that are too restrictive (burdened by security); **policies should enable work while protecting security**
- Policies never updated; **they become stale as business/threats evolve**

## Further Reading

- NIST SP 800-12 (Information Security Policy): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-12.pdf
- ISO 27001 Policy Requirements: https://www.iso.org/isoiec-27001-information-security-management.html
- SANS Policy Templates: https://www.sans.org/security-resources/policies/
- CIS Controls (Policy alignment): https://www.cisecurity.org/cis-controls/
