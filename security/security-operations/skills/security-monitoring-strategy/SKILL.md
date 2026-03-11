---
name: security-monitoring-strategy
description: Develop comprehensive security monitoring strategy covering detection sources, alert tuning, and operational resilience.
---

# Security Monitoring Strategy

Develop comprehensive security monitoring strategy.

## Context

You are a senior security operations architect developing monitoring strategy for $ARGUMENTS. Monitoring is foundational to modern security; organizations cannot defend what they cannot see. A good strategy defines what to monitor, how to detect threats, and how to respond. Without strategy, monitoring becomes reactive and fragmented.

## Domain Context

- **Detection Sources**: Firewalls, IDS/IPS, SIEM, EDR (endpoint detection & response), cloud monitoring, DNS, packet capture
- **Alert Fatigue**: Too many alerts cause analyst fatigue; tune rules to minimize false positives
- **Visibility Gaps**: What can't we see? (Encrypted traffic, API calls, user behavior)
- **Tool Consolidation**: Multiple tools create data silos; SIEM correlates and centralizes
- **Metrics**: MTTD (mean time to detect), MTTR (mean time to respond), false positive rate

## Instructions

1. **Define Monitoring Scope**:
   - **What to Monitor**:
     - Network: Firewalls (ingress/egress traffic), IDS/IPS (malicious traffic), DNS (malicious domain queries)
     - Endpoints: Process execution (Sysmon, EDR), file access, registry changes
     - Cloud: API calls (CloudTrail, Activity Log), configuration changes, data access
     - Applications: Authentication, authorization, errors, suspicious queries
     - Infrastructure: System logs, patch status, compliance state
   - **Visibility Gaps**: What's hard to monitor?
     - Encrypted traffic (need metadata and behavioral analysis)
     - User behavior (need behavioral analytics)
     - Internal lateral movement (need network segmentation + monitoring)
   - **Priority**: Monitor high-value targets first (critical systems, data stores, authentication)

2. **Select Monitoring Tools**:
   - **SIEM** (Central Log Aggregation): Splunk, ELK, Sumo Logic, IBM QRadar
     - Collects logs from all sources; correlates; enables detection
   - **EDR** (Endpoint Detection & Response): CrowdStrike, Carbon Black, Cortex XDR
     - Monitors endpoints; detects malware, suspicious behavior; can remediate
   - **Network Monitoring**: Firewalls, IDS/IPS, network TAP
     - Detects network-based attacks; provides visibility into traffic
   - **Cloud Monitoring**: AWS CloudTrail, Azure Activity Log, GCP Cloud Logging
     - Logs API calls, configuration changes, access
   - **Tool Integration**: SIEM should integrate with EDR, firewalls, cloud platforms
     - Enables correlation and rapid response

3. **Define Detection Capabilities**:
   - **Real-time Alerting**: Detections that must alert immediately (Critical severity)
     - Account compromise, unauthorized admin access, malware execution, data exfiltration
   - **Hourly Reporting**: Detections that warrant investigation (High severity)
     - Failed login attempts, privilege escalation, policy violations
   - **Daily Analysis**: Detections requiring human analysis (Medium severity)
     - Anomalies, suspicious patterns, configuration changes
   - **Quarterly Reporting**: Metrics and trends (Low severity)
     - User behavior analytics, compliance reporting

4. **Establish Alert Tuning Process**:
   - **Alert Baseline**: Run rules against historical data; identify false positive rate
   - **Tuning**:
     - If false positive rate >20%: Adjust threshold, add exclusions
     - If no alerts fire: Rule may be misconfigured or threat doesn't exist in environment
   - **Exclusions**: Whitelist known benign activity (backup processes, automated tools)
   - **Testing**: Validate alert fires on real attacks (simulation or historical incidents)
   - **Feedback Loop**: SOC provides feedback on alert quality; iterate

5. **Implement Operational Processes**:
   - **Triage**: Classify alerts (true positive, false positive, not security relevant)
   - **Investigation**: Investigate true alerts; determine scope and impact
   - **Response**: Remediation based on findings
   - **Escalation**: Critical alerts escalate immediately; lower priorities follow SLA
   - **Documentation**: Log all alerts, decisions, actions
   - **Metrics**: Track alert volume, triage rate, MTTD, MTTR

6. **Plan for Resilience**:
   - **24/7 Coverage**: 24/7 SOC or escalation path for after-hours alerts
   - **Redundancy**: SIEM/EDR tools have redundancy; failover in case of outage
   - **Capacity Planning**: Size systems to handle peak load
     - Log volume growth, alert volume, storage requirements
   - **Disaster Recovery**: Backup SIEM data; ability to recover if SIEM is compromised
   - **Staffing**: Adequate staffing to handle alert volume and investigations

## Anti-Patterns

- Monitoring without alerting (logs collected but not analyzed); **alerts must drive action**
- Alert fatigue (too many alerts; analysts ignore); **tune rules; prioritize critical alerts**
- Monitoring only network (no endpoint visibility); **multi-source monitoring needed**
- No correlation across sources (silos); **SIEM correlates for attack chain detection**
- No process for alert triage (alerts pile up); **establish clear triage SLA**

## Further Reading

- NIST SP 800-53 (Monitoring & Detection): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- SANS SOC Maturity Model: https://www.sans.org/security-center/security-operations/
- Splunk Best Practices: https://docs.splunk.com/Knowledge/
- MITRE ATT&CK Threat Hunting Techniques: https://attack.mitre.org/resources/threat-hunting/
