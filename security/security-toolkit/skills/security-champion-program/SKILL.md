---
name: security-champion-program
description: Establish security champion program to embed security expertise across teams and improve security culture.
---

# Security Champion Program

Establish security champion program to scale security awareness and expertise.

## Context

You are a senior security leader establishing a security champion program for $ARGUMENTS. Champions are security advocates within teams; they bridge security and development/operations, drive improvements, and escalate issues. Champions scale security without hiring armies of security specialists.

## Domain Context

- **Champion Role**: Non-security employee trained in security; serves as security expert for their team
- **Program Structure**: Recruitment, training, engagement, recognition, metrics
- **Success Factors**: Executive sponsorship, clear expectations, recognition, resources (time, budget)
- **Impact**: Improved security culture, faster issue resolution, better threat awareness

## Instructions

1. **Establish Program Structure**:
   - **Selection**: Identify champions from each team
     - Traits: Technical depth, influence, enthusiasm, trust of peers
     - Roles: Lead developers, senior engineers, team leads (not necessarily security team)
   - **Roles & Responsibilities**:
     - Security subject matter expert for team
     - Review security requirements, code for vulnerabilities
     - Lead security discussions in team meetings
     - Escalate security issues to security team
     - Advocate for security culture improvements
   - **Time Commitment**: 5-10 hours/month (part of job, not additional responsibility)
   - **Compensation**: Recognition, career opportunities, bonuses (depends on org)

2. **Training Champions**:
   - **Core Training** (annual):
     - OWASP Top 10 / CWE Top 25
     - Secure coding practices (input validation, authentication, cryptography)
     - Security testing (SAST, DAST, penetration testing)
     - Incident response basics
   - **Specialized Training** (based on role):
     - DevOps: Infrastructure security, IAM, secrets management, scanning
     - Frontend: XSS, CSRF, CSP, secure dependency management
     - Backend: API security, database security, authentication, authorization
     - Cloud: Cloud-specific threats, misconfigurations, compliance
   - **Ongoing Learning**: Monthly webinars, newsletters, Slack channels
   - **Certification**: Optional security certification (CISSP, CEH, OSSA) with company support

3. **Engagement & Support**:
   - **Regular Meetings**:
     - Monthly champions meeting (security team + champions; discuss threats, improvements)
     - Slack channel for async discussion
     - Quarterly in-person if possible
   - **Escalation Path**:
     - Champion identifies security concern; brings to team discussion
     - If unresolved, escalates to security team
     - Security team aids resolution; champions learn from process
   - **Resources**:
     - Security team dedicated liaision (not champion's manager)
     - Playbooks for common issues
     - Tools and training (SAST, secrets scanning, etc.)

4. **Drive Security Improvements**:
   - **Code Review**: Champions participate in code reviews; catch security issues
   - **Security Requirements**: Champions ensure security requirements are in definition of done
   - **Threat Modeling**: Champions facilitate threat modeling for new features
   - **Vulnerability Management**: Champions track and remediate vulnerabilities in their team's code
   - **Awareness**: Champions lead security discussions; evangelize best practices
   - **Incidents**: When team is involved in security incident, champion participates in response

5. **Recognition & Incentives**:
   - **Public Recognition**:
     - Highlight in security newsletters, all-hands meetings
     - Security champion awards (annual)
     - Social media recognition
   - **Career Development**:
     - Security expertise opens career paths (may lead to security roles)
     - Training/certifications funded by company
     - Performance reviews include security contributions
   - **Tangible Benefits**:
     - Bonus or stipend (depends on company policy)
     - Professional development budget
     - Flex time for security work
   - **Retention**: Career development ensures champions don't leave for security-only roles

6. **Measure Program Success**:
   - **Adoption Metrics**:
     - % of teams with assigned champion
     - Champion retention rate (are they staying?)
     - Training completion rate
   - **Effectiveness Metrics**:
     - Security issues caught by champions (code review)
     - Vulnerability remediation speed
     - Security culture surveys (improved awareness?)
     - Incidents involving champion teams (fewer due to awareness?)
   - **Impact**: Program ROI vs. cost of hiring additional security staff

## Anti-Patterns

- Assigning champion role without training (overwhelmed); **provide comprehensive training**
- No support from security team (champions struggle alone); **security team must support**
- No recognition (champions feel undervalued); **recognize publicly and reward**
- Over-tasking champions (security work piles on); **protect their primary job**
- Treating champions as security team extension (not scalable); **champions are catalysts, not replacements**

## Further Reading

- Building Effective Security Programs (SANS): https://www.sans.org/security-resources/
- Security Culture: Salesforce, Google examples of champion programs
- DevSecOps Best Practices: Gartner reports on security culture
- OWASP Security Champions Guide: https://owasp.org/www-project-security-champions-playbook/
