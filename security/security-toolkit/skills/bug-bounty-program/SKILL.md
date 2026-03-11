---
name: bug-bounty-program
description: Establish and manage bug bounty programs to leverage external researchers for vulnerability discovery.
---

# Bug Bounty Program

Establish and manage bug bounty programs for external vulnerability discovery.

## Context

You are a security manager establishing a bug bounty program for $ARGUMENTS. Bug bounties engage ethical hackers to find vulnerabilities before attackers. Managed well, bug bounties find critical vulnerabilities at 10% the cost of penetration testing. Poorly managed, they waste money or create liability.

## Domain Context

- **Bug Bounty Platforms**: HackerOne, Bugcrowd, Intigriti, Synack
- **Program Structure**: Scope (what's in/out), reward structure (severity-based), process (submission → triage → remediation → payment)
- **Researcher Types**: Hobbyists (small rewards), professionals (larger programs), teams (enterprise)
- **Legal**: Clear rules of engagement to protect company from liability; researcher confidentiality agreements

## Instructions

1. **Define Program Scope & Rules**:
   - **In-Scope**:
     - Web applications, APIs, mobile apps, infrastructure (if applicable)
     - Specific domains (example.com, api.example.com)
     - Vulnerability types (code flaws, misconfigurations, not physical security)
   - **Out-of-Scope**:
     - Third-party services, vulnerabilities in dependencies (not your code)
     - Denial of service, resource exhaustion attacks
     - Social engineering, phishing
     - Systems without authorization (staging/test only)
   - **Rules of Engagement**:
     - Ethical researchers only; no criminal activity
     - Don't destroy/modify data; test-only access
     - Disclose to us first (responsible disclosure); 90-day embargo before public disclosure
     - No extortion, blackmail, or sale of vulnerabilities

2. **Establish Reward Structure**:
   - **Severity-Based Rewards**:
     - Critical (Remote Code Execution, SQL Injection, Data Breach): $1,000-$10,000+
     - High (Privilege Escalation, XSS, Business Logic Flaws): $500-$2,000
     - Medium (Information Disclosure, Weak Crypto): $100-$500
     - Low (Documentation, minor issues): $10-$100
   - **Factors Affecting Reward**:
     - Severity (CVSS score)
     - Complexity (how easy to exploit?)
     - Impact (how many users affected?)
     - Quality of report (clear reproduction steps?)
   - **Budget**: Allocate annual bug bounty budget (research required; depends on industry/size)
     - Typical: 0.1-1% of security budget

3. **Recruitment & Engagement**:
   - **Platform Selection**: HackerOne (largest), Bugcrowd (enterprise-friendly), Intigriti (European)
   - **Program Launch**: Announce program; recruit researchers
   - **Researcher Retention**: Fast response, fair rewards, recognition
   - **Communication**: Regular updates on program status, thank you to researchers

4. **Submission & Triage Process**:
   - **Submission**: Researcher submits vulnerability report
     - Description, reproduction steps, evidence (screenshots)
   - **Triage** (within 2-5 days):
     - Is it a real vulnerability? (Validate)
     - Is it in scope? (Check scope list)
     - What's the severity? (CVSS scoring)
     - Acknowledge receipt; thank researcher
   - **Verification**:
     - Reproduce vulnerability in test environment
     - Confirm no previous report (no duplicates)
     - Assign severity and reward amount
   - **Communication**: Update researcher on status; timeline for fix

5. **Remediation & Payment**:
   - **Fix Development**: Development team fixes vulnerability
     - Timeline: Critical (1-2 weeks), High (1-4 weeks), Medium/Low (backlog)
   - **Testing**: Verify fix resolves vulnerability
     - Researcher may re-test after fix (optional; adds confidence)
   - **Deployment**: Deploy fix to production
   - **Payment**: After fix is deployed, researcher receives reward
     - Payment method: Direct deposit, check, donation to charity
   - **Disclosure**: After 90 days embargo, researcher can publicly disclose (optional)

6. **Program Metrics & Improvement**:
   - **Metrics**:
     - Vulnerabilities submitted (monthly)
     - Vulnerabilities validated (rate of quality submissions)
     - Severity distribution (are we finding critical issues?)
     - Average time to fix (how quickly are we remediating?)
     - Researcher retention (repeat reporters?)
     - Cost per vulnerability (total spend / number of vulnerabilities)
   - **Improvement**:
     - Quarterly review of program effectiveness
     - Adjust rewards if recruiting/retention issues
     - Update rules if new exploit types emerge
     - Communicate to company: vulnerabilities found, fixes deployed, cost-effective vs. alternatives

## Anti-Patterns

- Unclear rules of engagement (liability risk); **detailed scope document required**
- Underpaying researchers (low quality submissions); **competitive rewards attract quality researchers**
- Slow response/payment (frustrates researchers); **respond within 2-5 days; pay promptly**
- No process for handling malicious researchers (legal issues); **clear rules and enforcement**
- Treating bounty findings as lower priority than internal findings (defeats purpose); **prioritize bounty findings**

## Further Reading

- HackerOne Security Guidelines: https://www.hackerone.com/security-guidelines
- Bugcrowd Resources: https://www.bugcrowd.com/resources/
- OWASP Responsible Disclosure: https://owasp.org/www-community/attacks/Responsible_Disclosure
- Industry Case Studies: Google, Microsoft, Apple bug bounty programs
