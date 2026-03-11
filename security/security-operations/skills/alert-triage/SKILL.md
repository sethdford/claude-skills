---
name: alert-triage
description: Triage security alerts to classify as true/false positives and prioritize investigation and response.
---

# Alert Triage

Triage security alerts efficiently to focus analyst time on real threats.

## Context

You are a senior SOC (Security Operations Center) manager designing alert triage process for $ARGUMENTS. Triage is the critical first step: analysts receive thousands of alerts daily; triage separates signal from noise. Effective triage focuses investigation on true positives and prevents alert fatigue.

## Domain Context

- **Alert Volume**: Enterprise SOCs handle 10,000-1M+ alerts/day; can't investigate all
- **False Positive Rate**: Goal <20%; higher rates cause alert fatigue (analysts ignore alerts)
- **Triage Outcome**: True Positive (investigate), False Positive (log/ignore), Non-Security (not relevant), Duplicate (same alert, multiple times)
- **SLA**: Critical alerts triage within minutes; High within hours; lower priorities within business hours
- **Feedback Loop**: Analysts provide feedback (this alert is always false positive); rules tuned to reduce false positives

## Instructions

1. **Establish Alert Categories**:
   - **Critical Severity**: Investigate immediately; page on-call
     - Confirmed malware execution, credential compromise, active data exfiltration, privilege escalation in progress
   - **High Severity**: Investigate within 1 hour
     - Suspicious process execution, privilege escalation attempt, failed admin access, firewall block of known malicious IP
   - **Medium Severity**: Investigate within business hours
     - Policy violations, suspicious behavior, anomalies, multiple failed logins
   - **Low Severity**: Log for analysis
     - Informational, known false positives, non-urgent suspicious activity

2. **Triage Questions**:
   - **Is this real?**
     - Is alert based on valid detection rule? (Some rules fire on benign activity)
     - Did alert fire before? (If yes, is it false positive?)
     - Validate: Look at raw logs; confirm alert criteria met
   - **Is this actionable?**
     - If benign: False positive (log/suppress)
     - If real but already mitigated: Document; ticket for rule improvement
     - If real and active: Escalate for investigation
   - **What's the scope?**
     - Isolated incident or widespread? (One user or many?)
     - Internal-only or external exposure?
     - Business-critical system or non-critical?
   - **Who responds?**
     - Does alert severity match response priority? (Critical = immediate; Low = backlog)
     - Should this alert page on-call? Or can wait for business hours?

3. **Classify Alert Outcome**:
   - **True Positive**: Real security event requiring investigation
     - Severity assignment, owner assignment, ticket creation
   - **False Positive**: Benign activity that triggered rule
     - Document reason; suppress/update rule to prevent recurring false positive
   - **Non-Security**: Not related to security (performance issue, operational event)
     - Route to correct team (ops, network, application support)
   - **Duplicate**: Same alert multiple times (multiple systems, multiple data sources)
     - Deduplicate; single ticket for investigation
   - **No Action**: Known false positive; suppress and log

4. **Document Triage Decision**:
   - **Alert ID**: Unique identifier for tracking
   - **Detection Rule**: What rule generated alert?
   - **Triage Decision**: TP, FP, non-security, duplicate, no-action
   - **Reasoning**: Why was this classification assigned?
   - **Owner**: Who will investigate (if TP)?
   - **Timestamp**: When was triage decision made?
   - **Evidence**: Screenshots, logs showing decision rationale

5. **Escalation Process**:
   - **Critical Alerts**:
     - Triage immediately (within minutes)
     - If true positive: Escalate to incident commander; activate IR team
     - If false positive: Suppress rule; post-mortem on rule tuning
   - **High Alerts**:
     - Triage within 1 hour
     - Assign to analyst; begin investigation
   - **Medium/Low**:
     - Triage within shift
     - Batch for analysis; investigate if time permits

6. **Feedback & Rule Improvement**:
   - **False Positive Tracking**: Count FP by rule; identify problematic rules
   - **Rule Tuning**: For rules with high FP rate:
     - Increase threshold (fewer alerts fire)
     - Add exclusions (whitelist benign activity)
     - Change logic (AND instead of OR)
   - **Feedback to Rule Authors**: Notify detection engineer of FP rate; request adjustment
   - **Monitoring**: After tuning, verify FP rate improves

## Anti-Patterns

- No triage process (alerts pile up, never investigated); **establish clear SLA for triage**
- No feedback on false positives (same rule fires forever); **collect FP data; tune rules**
- Escalating all alerts as Critical (cry wolf); **severity assignment must reflect actual risk**
- Triage without investigation (mark true positive without verifying); **validate before escalating**
- No tracking of triage decisions (can't improve); **log all decisions for metrics**

## Further Reading

- SANS SOC Maturity Model: https://www.sans.org/security-center/security-operations/
- Alert Tuning Best Practices: https://www.splunk.com/en_us/blog/security/alert-tuning.html
- MITRE ATT&CK Alert Triage: https://attack.mitre.org/resources/
- PagerDuty Incident Response: https://www.pagerduty.com/incident-response/
