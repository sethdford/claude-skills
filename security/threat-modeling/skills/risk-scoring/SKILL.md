---
name: risk-scoring
description: Quantify risk using likelihood and impact, apply severity ratings, and prioritize mitigations. Use when prioritizing threats, allocating security budget, and communicating risk to leadership.
---

# Risk Scoring

Quantify and prioritize threats using standardized risk scoring methodologies.

## Context

You are a senior security architect scoring risks for $ARGUMENTS. Risk scoring translates threats into actionable priorities for the security and engineering teams.

## Domain Context

- **Risk = Likelihood × Impact**: Qualitative or quantitative; guides prioritization
- **Likelihood**: Probability that threat will manifest; factors: attacker capability, accessibility, controls, time
- **Impact**: Business consequence if threat succeeds; factors: affected data, disruption, compliance, reputation
- **Risk Rating**: Critical (4-5), High (3), Medium (2), Low (1); commonly mapped to action timelines (Critical: days, High: weeks, Medium: months)
- **Risk Appetite**: Organization's tolerance for residual risk; determines which risks require mitigation vs. acceptance

## Instructions

1. **Define Scoring Scale** (Qualitative):
   - **Likelihood**: Rare (1), Unlikely (2), Possible (3), Likely (4), Almost Certain (5)
   - **Impact**: Negligible (1), Minor (2), Moderate (3), Major (4), Catastrophic (5)
   - **Risk = Likelihood × Impact**: Ranges from 1 (low) to 25 (critical)

2. **Alternatively, Define Quantitative Scoring** (if organization has historical data):
   - **Likelihood**: Probability per year (0.1%, 1%, 10%, 50%, 90%+)
   - **Impact**: Dollar amount ($1K, $100K, $1M, $10M+) or other metric (customers affected, compliance fines, operational hours)
   - **Risk = Likelihood × Impact $ Amount**: Enables ROI calculation for mitigations

3. **For Each Threat, Assess Likelihood**:
   - Is the attack vector accessible? (e.g., public-facing API vs. internal-only database)
   - What attacker skills are required? (e.g., SQL injection requires moderate skill; 0-day requires advanced)
   - What preconditions must be met? (e.g., user social engineering, stolen credential, insecure configuration)
   - Are existing controls already in place reducing likelihood?
   - Has this threat materialized in industry? (real threats are more likely than theoretical)

4. **Assess Impact**:
   - **Data Impact**: How much PII, financial data, or trade secrets are exposed? (1 record vs. millions; revenue impact)
   - **Operational Impact**: Service downtime? Loss of revenue? Customer churn?
   - **Compliance Impact**: GDPR fines (up to 4% of global revenue), PCI-DSS fines, regulatory action?
   - **Reputational Impact**: Will customers learn of the breach? Media coverage?
   - **Cascading Impact**: Does this threat enable follow-on attacks? (e.g., credential compromise → lateral movement → ransomware)

5. **Calculate Risk Score and Prioritize**:
   - **Critical (16-25)**: Mitigate immediately; may halt releases if not addressed
   - **High (9-15)**: Mitigate within sprint/month; block production deployment if not addressed
   - **Medium (4-8)**: Mitigate within quarter; track for future resolution
   - **Low (1-3)**: Accept or defer; document why risk is acceptable

6. **Document Risk Decisions**:
   - **Mitigate**: Implement control to reduce likelihood or impact
   - **Accept**: Risk is acceptable given business context (document why)
   - **Transfer**: Buy insurance, use third-party service
   - **Avoid**: Don't implement the feature or change the architecture

## Anti-Patterns

- Treating all threats equally; **risk scoring explicitly prioritizes, ensuring time/budget goes to highest-impact threats**
- Using only likelihood without impact (or vice versa); **a likely but negligible-impact threat is lower priority than an unlikely but catastrophic threat**
- Scoring without considering existing controls; **a SQL injection threat in a codebase with parameterized queries + WAF is lower likelihood than in unprotected code**
- Inflating severity due to fear; **"what if a nation-state targeted us?" is not a justified threat rating; base scoring on realistic attack vectors**
- Treating risk scores as static; **re-assess quarterly; as controls deploy, threat scores decrease and other threats bubble up in priority**

## Further Reading

- NIST SP 800-30 (Risk Assessment): Formal methodology for likelihood/impact assessment
- ISO/IEC 27005 (Information Security Risk Management): Risk analysis and evaluation
- FAIR Model (Factor Analysis of Information Risk): Quantitative risk scoring
- OWASP Risk Rating Methodology: Application-specific risk scoring for web applications
