---
name: penetration-test-scope
description: Define penetration test scope, objectives, and constraints to align testing with business goals and compliance requirements.
---

# Penetration Test Scope

Define penetration test scope, objectives, rules of engagement, and success criteria.

## Context

You are a senior security architect planning a penetration test for $ARGUMENTS. A well-scoped penetration test has clear objectives, defined targets, agreed-upon constraints, and measurable success criteria. Poor scoping leads to missed testing, false negatives, or testing outside agreed boundaries.

## Domain Context

- **Penetration Test Types**: External (attack from internet), internal (attack from network), social engineering, physical security, supply chain
- **Scope Dimensions**: Systems (servers, applications, networks), data (what's in scope to access?), users (employees, customers, partners?), timeframe
- **Rules of Engagement (RoE)**: What's allowed? Denial of service? Social engineering? Data exfiltration? Which systems are off-limits?
- **Compliance Alignment**: PCI-DSS, HIPAA, SOC 2, ISO 27001 may require annual or periodic penetration testing

## Instructions

1. **Define Test Objectives**:
   - Clarify what you want to learn: "Can attackers access customer data?", "Is our authentication robust?", "Do employees fall for phishing?"
   - Align with business goals: security posture improvement, compliance validation, incident response testing, supply chain risk assessment
   - Specify success criteria: vulnerabilities found, attack chain demonstrated, business impact quantified

2. **Define Test Scope**:
   - **In-Scope Systems**: List all systems to be tested (web app, mobile app, APIs, cloud infrastructure, on-prem servers)
   - **Out-of-Scope Systems**: Systems that are off-limits (production databases, critical infrastructure, third-party systems without permission)
   - **Data Scope**: What data can testers access or exfiltrate? (Avoid accessing real customer PII if possible; use staging data)
   - **Timeline**: When is testing allowed? (Off-hours? Weekends? Avoid critical business events)

3. **Establish Rules of Engagement**:
   - **Destructive Testing**: Are DOS/DDoS attacks allowed? System crashes?
   - **Social Engineering**: Is phishing/pretexting allowed? Which employee groups?
   - **Physical Access**: Can testers attempt physical break-ins?
   - **Reporting**: Who is notified if a critical vulnerability is found? Escalation procedures?
   - **Remediation Access**: Do testers have access to remediation systems, or test-only access?

4. **Identify Constraints & Limitations**:
   - **Environment**: Production, staging, or dedicated test environment?
   - **Approval Required**: What testing requires additional approval (data access, social engineering)?
   - **Testing Intensity**: Full attack simulation vs. lighter assessment?
   - **Regulatory**: Which compliance frameworks apply? (PCI-DSS, HIPAA, SOC 2)

5. **Document Agreements**:
   - Written scope document signed by security team and business stakeholders
   - Penetration test contract with external firm (if applicable) specifying RoE
   - Communication plan (who gets updates, how urgent issues are escalated)
   - Post-test briefing schedule and report expectations

## Anti-Patterns

- Vague scope ("test our security"); **specific, measurable scope prevents misalignment and wasted effort**
- Excluding critical systems from scope; **scope should represent your highest-risk assets**
- Unlimited social engineering (annoying employees, high stress); **social engineering should be targeted and approved**
- Testing production without permission or safeguards; **always get explicit approval; consider staging environment**
- Not documenting RoE; **misunderstandings between tester and organization cause conflicts**

## Further Reading

- PTES (Penetration Testing Execution Standard): http://www.ptes.org/
- NIST SP 800-115 (Technical Security Testing): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf
- OWASP Penetration Testing: https://owasp.org/www-project-web-security-testing-guide/
- CIS Controls: Guidance on penetration testing frequency and scope
