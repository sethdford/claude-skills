---
name: security-awareness-training
description: Develop and deliver security awareness training to build organizational security culture and reduce human risk.
---

# Security Awareness Training

Develop effective security awareness training programs.

## Context

You are a senior security training officer developing awareness programs for $ARGUMENTS. Most breaches involve human error (phishing, weak passwords, misconfiguration); training is cost-effective mitigation. Well-designed training changes behavior; poorly designed training is ignored.

## Domain Context

- **Human Risk**: 90%+ of breaches involve human error (phishing, credential compromise, misconfiguration)
- **Training Content**: Phishing awareness, password security, data handling, incident reporting, compliance requirements
- **Delivery Methods**: In-person, online courses, simulations, newsletters, posters, videos
- **Measurement**: Phishing simulation click rates, training completion, security culture survey
- **Compliance**: GDPR, HIPAA, PCI-DSS require documented security training

## Instructions

1. **Assess Training Needs**:
   - **Audience Segments**:
     - All employees: Foundation training (phishing, passwords, reporting)
     - Developers: Secure coding, OWASP Top 10, supply chain security
     - Admins/DevOps: Infrastructure security, IAM, patch management
     - Finance/HR: Data privacy, insider threat awareness
     - Executives: Risk management, compliance, breach notifications
   - **Baseline**: Phishing simulation (how many employees click phishing links?)
     - Use results to tailor training focus
   - **Compliance Requirements**: What training is mandated?
     - GDPR requires data privacy training
     - HIPAA requires HIPAA-specific training
     - PCI-DSS requires security training

2. **Develop Training Content**:
   - **Phishing Awareness**:
     - How to identify phishing emails (spelling, sender, urgency, suspicious links)
     - Red flags: Unsolicited requests, urgency, unknown sender, unusual requests
     - What to do if suspicious: Don't click, report to security team
     - Hands-on exercise: Review example phishing emails; identify red flags
   - **Password Security**:
     - Strong passwords: Length, complexity, uniqueness, MFA importance
     - Password manager usage
     - What to do if password compromised: Change immediately, report
   - **Data Handling**:
     - Data classification (public, internal, confidential, restricted)
     - Appropriate handling per classification (encryption, access control)
     - What not to do: Don't share confidential data in email, not in shared documents
   - **Incident Reporting**:
     - How to recognize security incident (suspicious activity, unexpected changes)
     - Who to report to (security team email, hotline, trusted manager)
     - What happens after reporting (no retaliation, investigation, follow-up)

3. **Select Delivery Method**:
   - **In-Person Training** (most effective but expensive):
     - Interactive workshops
     - Role-play scenarios (handling phishing email)
     - Q&A with security experts
   - **Online Courses** (scalable, self-paced):
     - Short modules (15 minutes each) for busy employees
     - Interactive quizzes to verify understanding
     - Certificates of completion
   - **Phishing Simulations** (most impactful):
     - Employees receive realistic phishing emails (controlled)
     - Track who clicks; measure improvement over time
     - Provide training to those who click
   - **Posters, Videos, Newsletters** (reinforcement):
     - Monthly security tips
     - Video case studies (recent incident; lessons learned)
     - Posters in common areas

4. **Implement & Schedule**:
   - **Annual Training**: Mandatory for all employees
     - Foundation training (2 hours) for new hires
     - Refresher training (1 hour) annually for all
   - **Role-Specific Training**: Developers, admins, finance; schedule by role
   - **Timing**: Avoid holiday seasons; coordinate with other mandatory training
   - **Tracking**: Maintain records of who completed training (audit trail; compliance)
   - **Enforcement**: Make training mandatory; track completion; enforce consequences for non-completion

5. **Measure & Improve**:
   - **Metrics**:
     - Training completion rate (goal: >95%)
     - Phishing click rate (measure baseline, then target reduction)
     - Post-training test scores (goal: >80% pass)
     - Incident reports related to training (did awareness lead to more reports?)
     - Security culture survey (improved awareness?)
   - **Feedback Loop**: Survey participants on training quality
     - What was most useful? What was boring? What should be added?
   - **Iteration**: Based on feedback, update content annually
     - Add new threats (zero-day, recent attacks)
     - Remove ineffective content
     - Adjust difficulty/length

6. **Build Positive Security Culture**:
   - **Safety First**: Emphasize "no blame" culture for mistakes
     - Employees should report phishing, not delete suspicious emails
     - Mistakes are learning opportunities
   - **Recognition**: Recognize employees who report threats
     - Email recognition for suspicious email reports
     - Rewards for good security behaviors
   - **Executive Modeling**: Leadership models security awareness
     - Executives complete training first
     - Executives don't circumvent policies
   - **Continuous Communication**: Security updates, newsletters, success stories

## Anti-Patterns

- Training compliance box-checking (no real learning); **measure behavior change, not just completion**
- Boring content (employees ignore); **use real examples, interactive elements**
- No measurement of effectiveness (unknown impact); **track metrics; prove value**
- Training once per year (knowledge fades); **regular reinforcement (monthly tips, quarterly refreshers)**
- Blaming humans for mistakes (creates fear); **foster psychological safety; mistakes are learning opportunities**

## Further Reading

- SANS Security Awareness Best Practices: https://www.sans.org/security-resources/policies/
- NIST SP 800-50 (Security Awareness Training): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-50.pdf
- Gartner Security Culture Reports: Trends in effectiveness
- Proofpoint Phishing Simulations: Industry statistics on click rates
