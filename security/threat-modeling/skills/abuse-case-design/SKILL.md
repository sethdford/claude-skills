---
name: abuse-case-design
description: Design abuse cases (negative use cases) showing how attackers misuse system features. Use when identifying attacks that exploit intended functionality or business logic flaws.
---

# Abuse Case Design

Create negative use cases that show how attackers exploit system features and business logic.

## Context

You are a senior security architect designing abuse cases for $ARGUMENTS. Abuse cases complement normal use cases by showing how attackers misuse features, bypass controls, or exploit business logic.

## Domain Context

- **Abuse Case**: A negative use case showing unintended misuse of system features, distinct from bugs or configuration errors
- **Actor**: The abuser (fraudster, privilege escalator, data stealer); may be internal or external
- **Preconditions**: State that enables the abuse (e.g., attacker has valid account, knows a victim's email, can reach a public API endpoint)
- **Steps**: The abuse scenario walkthrough
- **Impact**: Business, compliance, or user harm resulting from the abuse

## Instructions

1. **Enumerate Use Cases First**: List normal use cases (e.g., "User logs in", "User transfers funds", "Admin approves request").

2. **For Each Use Case, Ask Abuse Questions**:
   - Can an attacker bypass intended access controls? (e.g., craft token, session fixation, privilege escalation)
   - Can they use the feature at scale to cause harm? (e.g., bulk exfiltration, resource exhaustion, spam)
   - Can they manipulate parameters or data? (e.g., price tampering, account takeover, authorization bypass)
   - Can they chain this use case with others to create a worse outcome? (e.g., login → password reset → account takeover)

3. **Document Abuse Cases in Standard Format**:
   - **Use Case**: "User transfers funds"
   - **Abuse Case**: "Attacker transfers victim funds without authorization"
   - **Actor**: External fraud ring
   - **Preconditions**: Attacker knows victim email, victim password is weak or reused, MFA is not enabled
   - **Steps**: (1) Attacker obtains credentials via phishing, (2) logs into victim account, (3) submits transfer to attacker account, (4) victim notices charge days later
   - **Impact**: Financial loss, customer trust, regulatory reporting (SOX if public company)

4. **Map to Controls**: For each abuse case, identify which controls should prevent it (authentication strength, MFA, transaction monitoring, etc.).

5. **Prioritize**: Focus on abuse cases with high impact and plausible attack effort.

## Anti-Patterns

- Confusing abuse cases with system bugs or configuration errors; **abuse cases assume the system works as designed, but the attacker misuses it**
- Creating abuse cases only for the happy path; **test and think about less-common features (admin functions, batch operations, API endpoints)**
- Documenting abuse cases without proposed mitigations; **each abuse case should drive a security requirement or control**
- Treating abuse cases as theoretical; **validate them against real attack patterns from your industry and threat intelligence**
- Neglecting business logic flaws in favor of technical vulnerabilities; **authorization bypass via business logic (e.g., "approve own request") is often overlooked**

## Further Reading

- Schneier, B. Threat Modeling (2012). Chapter on abuse cases and negative use cases.
- Jacobson, I. et al. (2020). Use-Case Driven Object Modeling with UML. (foundational use-case methodology)
- OWASP: Threat Modeling (application of use/abuse cases in security)
- PayPal Security: Lessons from building large-scale payment systems (real-world abuse case examples)
