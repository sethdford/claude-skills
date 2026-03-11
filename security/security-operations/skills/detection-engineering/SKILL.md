---
name: detection-engineering
description: Build detection engineering capabilities including threat modeling, detection hypothesis development, and hypothesis testing.
---

# Detection Engineering

Build detection capabilities through threat modeling, hypothesis development, and testing.

## Context

You are a senior detection engineer building detection engineering capabilities for $ARGUMENTS. Detection engineering is a discipline that systematically builds detections for known threats. Rather than reactive rule creation, detection engineering proactively models threats, develops hypotheses on how to detect them, and tests detections.

## Domain Context

- **Detection Hypothesis**: "If an attacker does X, what artifacts will we see in logs/telemetry?"
- **Threat Modeling**: Identify threats relevant to organization (industry, data, critical assets)
- **Telemetry**: What data do we have (logs, network, endpoint, cloud)? Can we detect the threat with current data?
- **Detection Coverage**: How many threats are we detecting? What gaps exist? (Goal: >80% coverage of top threats)
- **MITRE ATT&CK**: Framework for threat modeling; organize detections by tactic/technique

## Instructions

1. **Threat Modeling**:
   - **Industry-Specific Threats**:
     - Finance: Fraud, account takeover, data theft
     - Healthcare: Ransomware, patient data theft, HIPAA violations
     - Manufacturing: IP theft, supply chain compromise, operational technology attacks
   - **Data-Focused Threats**: What would attackers target in your environment?
     - Customer data, financial records, source code, trade secrets, credentials
   - **Critical Assets**: What's most important to defend?
     - Customer-facing systems, payment systems, databases, authentication systems
   - **Threat Actors**: Who might attack you?
     - Nation-states, cybercriminals, insiders, activists, competitors
   - **Attack Objectives**: What do attackers want?
     - Data theft, availability/disruption, espionage, financial gain, sabotage

2. **Map Attacks to MITRE ATT&CK**:
   - **Tactics**: 14 high-level attack phases (Reconnaissance, Initial Access, Execution, Persistence, Privilege Escalation, Defense Evasion, Credential Access, Discovery, Lateral Movement, Collection, Exfiltration, Command & Control, Impact)
   - **Techniques**: Specific attack techniques under each tactic (e.g., Spearphishing, Exploit Public-Facing Application, PowerShell)
   - **Procedures**: How a specific threat actor executes a technique
   - **Mapping**: For each relevant threat, identify MITRE tactics/techniques they use
   - **Coverage Analysis**: For each tactic/technique, determine if we have detection

3. **Develop Detection Hypotheses**:
   - **Attack Scenario**: "Attacker uses spearphishing to compromise user, gains code execution, persists via scheduled task, escalates to admin, exfiltrates data"
   - **Hypothesis**: "If attacker creates scheduled task for persistence, we will see:"
     - Windows event: EventID 106 (Scheduled Task Created)
     - Unusual parent process (not schtasks.exe, not from system account)
     - Task name contains suspicious keyword (mimikatz, reverse shell, beacon, etc.)
   - **Data Sources**: What telemetry can detect this? (Windows event logs, Sysmon, EDR, YARA rules)
   - **Detection Rule**: Build rule based on hypothesis
     - Rule: EventID 106 AND parent_process != schtasks.exe AND task_name matches [malicious keywords]

4. **Assess Detection Capability**:
   - **Current Telemetry**: What data sources do we have?
     - Firewalls (network), IDS/IPS (network), endpoint agents (process execution, file), cloud (API calls)
   - **Gap Analysis**: For each threat/tactic, do we have data to detect it?
     - Example: Can we detect credential access? (Do we log authentication failures? Can we detect password spraying?)
   - **Data Collection**: Identify missing telemetry; prioritize collection
     - Critical: Data for top threats
     - High: Data for high-impact attacks
     - Medium: Data for lower-priority threats
   - **Tool Requirements**: What tools needed to collect/analyze data?
     - EDR (endpoint detection), SIEM (log analysis), Network telemetry, Cloud monitoring

5. **Build & Test Detections**:
   - **Proof of Concept**: Build simple detection rule; test against clean data (verify no false positives)
   - **Historical Analysis**: Run rule against historical logs; verify detection fires on real attacks
   - **Simulation**: Simulate attack; verify detection fires
     - Tools: Atomic Red Team (test framework), Caldera (adversary emulation)
   - **Tuning**: Adjust rule based on testing; balance detection and false positives
   - **Deployment**: Deploy to production SIEM; monitor effectiveness

6. **Measure & Improve**:
   - **Detection Coverage**: For top 50 threats, how many are detected? (Goal: >80%)
   - **Detection Maturity**:
     - Level 1: Awareness (we know threat exists)
     - Level 2: Detection (we have rule, sometimes fires)
     - Level 3: Reliable (detection fires consistently; low false positives)
     - Level 4: Optimized (detection tuned; rapid response)
   - **Gaps**: Which threats are NOT detected? Prioritize detection development
   - **Feedback**: Use incident data to improve detections
     - If incident occurred but detection didn't fire: improve detection

## Anti-Patterns

- Building detections without threat modeling (detecting random threats); **start with threat model**
- High false positive rate (alert fatigue); **tune based on organization's environment**
- No validation of detections (rules that don't work); **test before and after deployment**
- No feedback from incidents (miss detections); **use incidents to improve detection coverage**
- Detection coverage stagnates (new threats not detected); **continuously add detections for new threats**

## Further Reading

- MITRE ATT&CK: https://attack.mitre.org/
- Atomic Red Team: https://atomicredteam.io/
- Detection Engineering Course (SANS): https://www.sans.org/cyber-security-courses/detection-engineering-essentials/
- Threat Hunting Techniques: David Bianco, ATT&CK Framework for Threat Hunting
