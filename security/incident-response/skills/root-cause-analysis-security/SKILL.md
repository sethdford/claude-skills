---
name: root-cause-analysis-security
description: Conduct root-cause analysis (RCA) to identify underlying causes of security incidents and prevent recurrence.
---

# Root-Cause Analysis (Security)

Conduct root-cause analysis to identify underlying causes and prevent recurrence.

## Context

You are a senior security engineer conducting root-cause analysis (RCA) for $ARGUMENTS. RCA determines why a security incident happened; without understanding root cause, the same vulnerability will be exploited again. RCA is not blame—it's learning. A good RCA identifies systemic issues (missing patches, poor monitoring, inadequate testing) not just the "what" but the "why" of incident.

## Domain Context

- **Root Causes**: Vulnerability (unpatched, misconfiguration), detection gap (no monitoring, alert misconfigured), process failure (access control bypassed)
- **RCA Techniques**: Five Whys, Fishbone Diagram, Event Tree Analysis
- **Blamelessness**: RCA is about systems, not people; aim for learning and prevention
- **Follow-up**: RCA findings drive remediation; prevention controls prevent similar incidents

## Instructions

1. **Understand the Incident Fully**:
   - **Timeline**: Detailed chronology of events (when did each thing happen?)
   - **Attack Vector**: How did attacker get in? (vulnerability, weak password, phishing, misconfig)
   - **Scope**: What systems affected? What data accessed? How long had attacker access?
   - **Detection**: What alerted you to incident? How long between intrusion and detection (MTTD)?
   - **Impact**: Business impact (revenue loss, downtime, customer trust, regulatory action)
   - **Interviews**: Interview people involved (who detected it? who investigated? what was missed?)

2. **Apply Five Whys Technique**:
   - **Observation**: System was compromised due to unpatched vulnerability
   - **Why 1**: Why was the system vulnerable? Because security patch was not applied
   - **Why 2**: Why wasn't patch applied? Because patch testing didn't include this system
   - **Why 3**: Why wasn't this system in patch testing? Because system inventory was incomplete
   - **Why 4**: Why was inventory incomplete? Because on-boarding process didn't document all systems
   - **Why 5**: Why didn't on-boarding process document systems? Because no process owner assigned
   - **Root Cause**: Lack of process ownership; systems weren't being tracked/managed
   - **Remediation**: Assign process owner; establish/improve system inventory process

3. **Identify Systemic Issues**:
   - **Vulnerability Management**: Are vulnerabilities being tracked? Are patches tested before deployment?
   - **Detection**: Are attacks being detected? How quickly (MTTD)? What's the alert threshold?
   - **Monitoring**: Are suspicious activities being monitored? (Failed logins, privilege escalation, data access)
   - **Access Control**: Is access properly restricted? Are credentials strong? Is MFA enabled?
   - **Segmentation**: Are systems isolated? Can attacker move laterally after initial compromise?
   - **Testing**: Are security controls tested? (penetration tests, vulnerability scans)
   - **Awareness**: Do employees know about threats? Can they identify phishing?

4. **Document Findings**:
   - **Executive Summary**: What happened? Root causes identified
   - **Technical Details**: How incident occurred; attack chain; detection/response timeline
   - **Root Cause Analysis**: Five Whys, systemic issues identified
   - **Contributing Factors**: What else made incident possible? (missing monitoring, weak segmentation)
   - **Recommendations**: Preventive controls to prevent similar incidents
   - **Priority**: Which recommendations are critical? (Must fix before similar incident occurs)

5. **Develop Remediation Plan**:
   - **Prevention Controls**: What will prevent this from happening again?
     - Example RCA: Patch wasn't applied → Remediation: Improve patch management process
     - Example RCA: Attack wasn't detected → Remediation: Improve monitoring/alerting
   - **Detective Controls**: What will help us detect earlier if prevention fails?
     - Example: Enhanced monitoring for exploitation attempts
   - **Priority**: Implement critical controls first
   - **Timeline**: When will each control be implemented? (Critical: <30 days)
   - **Verification**: How will you verify control is effective?

6. **Implement Preventive Measures**:
   - **Process Improvements**: Update patch management, on-boarding, access control processes
   - **Technical Controls**: Add/improve detection (monitoring, alerting), prevention (segmentation, hardening)
   - **Awareness**: Train employees on lessons learned
   - **Testing**: Verify controls work (security test, penetration test)
   - **Metrics**: Track if improvements reduce incident risk

## Anti-Patterns

- Focusing on symptom instead of root cause (patch the vulnerability but don't improve process); **identify systemic issues**
- Blaming individuals (person forgot to apply patch); **focus on systems and processes**
- No follow-up on recommendations (analysis without action); **implement preventive measures**
- Assuming one RCA explains everything (complex incidents have multiple causes); **identify all contributors**
- Not learning from similar incidents (same root cause, different trigger); **look for patterns across incidents**

## Further Reading

- NIST SP 800-61 (Post-Incident Activities): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf
- Blameless Post-Mortem Guide: https://www.pagerduty.com/blog/blameless-post-mortems/
- Five Whys Technique: Toyota Production System, continuous improvement methodology
- Fishbone Diagram: Ishikawa Diagram for cause and effect analysis
