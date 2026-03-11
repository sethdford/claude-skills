---
name: security-documentation
description: Develop comprehensive security documentation including policies, procedures, architecture, and runbooks.
---

# Security Documentation

Develop comprehensive security documentation for governance and operations.

## Context

You are a senior security documentation manager developing documentation for $ARGUMENTS. Documentation is the foundation of security governance: policies define requirements, procedures enable consistent execution, runbooks enable rapid response. Without documentation, security is inconsistent and tribal knowledge.

## Domain Context

- **Documentation Types**: Policies (requirements), procedures (how-to), architecture (system design), runbooks (incident response), guidelines (recommendations)
- **Audience**: Employees (must understand), operators (must execute), auditors (must verify), executives (must govern)
- **Governance**: Policies approved by executive/board; version controlled; annual review
- **Accessibility**: Easy to find, understand, and maintain (wiki > PDF archive)

## Instructions

1. **Define Documentation Framework**:
   - **Policies**: High-level requirements
     - Information Security Policy (overarching)
     - Access Control Policy
     - Data Protection Policy
     - Incident Response Policy
     - Acceptable Use Policy
   - **Procedures**: Step-by-step execution
     - User Provisioning Procedure
     - Incident Response Procedure
     - Patch Management Procedure
     - Change Management Procedure
   - **Architecture**: System design
     - Network Architecture Diagram
     - Cloud Architecture
     - Data Flow Diagram
     - Threat Model
   - **Runbooks**: Quick reference for operations
     - Incident Response Runbook
     - Escalation Procedures
     - Troubleshooting Guides
     - Contact Lists
   - **Guidelines**: Best practices and recommendations
     - Secure Coding Guidelines
     - Password Guidelines
     - API Security Guidelines

2. **Develop Quality Standards**:
   - **Clarity**: Use plain language; avoid jargon (define if necessary)
     - Example: Use "multi-factor authentication" instead of "MFA" on first mention
   - **Structure**: Consistent formatting; easy to scan
     - Use headings, bullet points, numbered lists
     - Include table of contents for long documents
   - **Examples**: Real-world examples; make documentation practical
     - Include screenshots, code samples, templates
   - **Versioning**: Track document versions; maintain change history
     - Version 1.0 (initial), 1.1 (minor update), 2.0 (major revision)
   - **Approval**: Policies/procedures require executive/legal approval before publication

3. **Documentation Content**:
   - **Policy Document**:
     - Purpose (why policy exists)
     - Scope (who it applies to)
     - Policy Statement (specific requirements)
     - Roles & Responsibilities (who ensures compliance)
     - Enforcement (consequences for non-compliance)
     - Related Policies (cross-references)
     - Approval & Dates (who approved, when effective, when next reviewed)
   - **Procedure Document**:
     - Purpose (what process accomplishes)
     - Prerequisites (what must be done first)
     - Step-by-step Instructions (numbered, clear)
     - Screenshots/Examples (visual aids)
     - Common Issues & Troubleshooting (help desk resource)
     - Related Documents (links to policies, runbooks)
   - **Architecture Document**:
     - Overview (what system does)
     - Components (servers, databases, APIs)
     - Data Flows (how data moves through system)
     - Security Controls (how system is secured)
     - Threat Model (what threats system faces)
     - Design Decisions (why architecture chosen)

4. **Organization & Accessibility**:
   - **Central Repository**: Wiki (Confluence, Notion, GitHub) not scattered email attachments
     - Search-enabled; version control; access control
   - **Navigation**: Clear structure; easy to find
     - Security Team section, Policies, Procedures, Runbooks, Architecture
   - **Links**: Cross-references between documents
     - Policy references related procedure
     - Runbook links to escalation list
   - **Audience Filtering**: Different documents for different readers
     - All-employee docs: Policies, User Guidelines
     - Operational docs: Procedures, Runbooks
     - Technical docs: Architecture, Security Controls
   - **Access Control**: Some docs (escalation, vulnerability details) restricted

5. **Maintenance & Updates**:
   - **Annual Review**: Review all documents annually
     - Are they still accurate? Has threat landscape changed?
     - Are policies still aligned with business?
     - Have we learned from incidents that should update docs?
   - **Update Process**:
     - Document proposed change
     - Circulate for review (legal, affected teams)
     - Approve (executive or board per policy)
     - Publish new version; archive old
   - **Notification**: When significant policy changes, notify all affected employees
     - Email + training + acknowledgment

6. **Effectiveness**:
   - **Usage Metrics**: Are people using documentation?
     - Wiki view counts (is it being read?)
     - Support tickets (are questions answered by docs?)
     - Audit findings (are procedures being followed?)
   - **Comprehension**: Do people understand documentation?
     - Quick feedback survey (was this clear? was it helpful?)
     - Support escalations (did doc answer question or escalate to support?)
   - **Compliance**: Are procedures being followed?
     - Audit reviews (are access controls properly approved per procedure?)
     - Incident reviews (did team follow incident procedure?)

## Anti-Patterns

- Documentation no one reads (jargon, too technical); **write for target audience**
- Documentation that contradicts actual practice (trust eroded); **document actual procedures, not ideals**
- Documentation never updated (becomes stale); **annual review mandatory**
- Documentation scattered across platforms (hard to find); **centralize in single repository**
- Too much documentation (overwhelming); **focus on critical docs; link rather than duplicate**

## Further Reading

- NIST SP 800-12 (Security Documentation): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-12.pdf
- SANS Policy Templates: https://www.sans.org/security-resources/policies/
- Google Technical Writing Courses: https://developers.google.com/tech-writing
- Confluence Best Practices: Atlassian documentation
