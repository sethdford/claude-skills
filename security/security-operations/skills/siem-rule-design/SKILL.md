---
name: siem-rule-design
description: Design SIEM (Security Information & Event Management) detection rules to identify suspicious activity and attacks.
---

# SIEM Rule Design

Design SIEM detection rules to identify suspicious activity and attacks.

## Context

You are a senior detection engineer designing SIEM rules for $ARGUMENTS. SIEM collects logs from all systems; detection rules analyze logs to find attacks. Well-designed rules detect real threats while minimizing false positives. Poor rules either miss attacks (false negatives) or overwhelm analysts with noise (false positives).

## Domain Context

- **SIEM Tools**: Splunk, ELK Stack, Sumo Logic, IBM QRadar, Rapid7 InsightIDR
- **Data Sources**: Firewalls, IDS/IPS, access logs, application logs, DNS, authentication
- **Detection Logic**: Rules match patterns (regex, keyword search), aggregate events, correlate across systems
- **Alert Fatigue**: Too many false positives cause alert fatigue; analysts ignore alerts; real attacks missed

## Instructions

1. **Understand Attack Patterns**:
   - **Reconnaissance**: Network scanning, WHOIS lookups, port scanning
   - **Initial Compromise**: Phishing email, vulnerable web app, credential stuffing, supply chain compromise
   - **Persistence**: Backdoor, scheduled task, cron job, SSH key, new user account
   - **Lateral Movement**: Compromised credentials, pass-the-hash, lateral scanning, network exploitation
   - **Data Exfiltration**: Large data download, DNS tunneling, SFTP/FTP transfers, cloud uploads
   - **Covering Tracks**: Log deletion, firewall rule changes, account lockouts

2. **Design Rules for Common Attacks**:
   - **Failed Login Attempts**:
     - Rule: >5 failed login attempts from same source within 5 minutes
     - Logic: Count failed authentication events; group by source IP; alert if count > 5
     - Fields: auth_result=failed, eventid=4625 (Windows)
     - Reduce False Positives: Exclude known automated tools, valid users who mistyped password
   - **Privilege Escalation**:
     - Rule: Non-admin user executing admin command
     - Logic: User without admin role runs command with admin privileges
     - Fields: user_role, command, privilege_level
     - Context: Rare but dangerous; alert on all occurrences
   - **New User Account Creation**:
     - Rule: New user account created after hours
     - Logic: Account creation event; exclude scheduled scripts/automation
     - Fields: eventid=4720 (Windows), account_creation_time, business_hours
   - **Data Exfiltration**:
     - Rule: Large file transfer to external IP
     - Logic: Data volume > threshold (100MB) to non-internal IP
     - Fields: source_ip, dest_ip, bytes_transferred, timestamp
     - Reduce False Positives: Exclude known external partners, cloud storage providers

3. **Implement Detection Correlation**:
   - **Multi-Step Attacks**: Correlate events across time to detect attack chains
     - Example: Failed login (reconnaissance) + successful login (compromise) + file access (exfiltration)
     - Logic: If event A then B then C within 1 hour, alert on attack chain
   - **Cross-System Correlation**: Correlate across firewalls, servers, endpoints, cloud
     - Example: Firewall block + endpoint malware alert = potential attack
   - **User Behavior Analysis**: Detect deviations from baseline
     - Example: User normally accesses HR systems; suddenly accessing finance database = suspicious
     - Tools: Machine learning (anomaly detection), statistical analysis

4. **Tune Rules for Accuracy**:
   - **True Positive Rate**: What % of alerts are real attacks? (Target: >80%)
   - **False Positive Rate**: What % are benign? (Target: <20%)
   - **Baseline Analysis**: Run rule against historical data; check for false positives
     - If rule fires on known benign activity, it will fire forever (tune it)
   - **Whitelist/Exclusions**: Exclude known false positives
     - Example: Daily backup process triggers "large data transfer" alert; whitelist known backup IP
   - **Threshold Tuning**: Adjust thresholds based on environment
     - Example: "5 failed logins in 5 minutes" might be too loose (whitelist automated tools) or too strict (users are too fast)

5. **Implement Alerts & Escalation**:
   - **Alert Priority**:
     - Critical: Real attack in progress; page on-call; immediate investigation
     - High: Suspicious but not immediately dangerous; SOC investigates within hours
     - Medium: Warrants investigation; SOC logs for analysis
     - Low: Research, informational
   - **Alert Actions**:
     - Email SOC
     - Create JIRA ticket
     - Page on-call engineer (for critical)
     - Auto-remediate (revoke credentials, block IP, isolate system) for highest confidence rules
   - **Playbook**: Document how to investigate each alert type
     - Questions: Is this a false positive? Is this a real attack? What's the scope?
     - Actions: Who to contact? What to collect? Who approves remediation?

6. **Monitor Rule Effectiveness**:
   - **Metrics**:
     - Detection rate: % of attacks detected by this rule (goal: >90%)
     - False positive rate: % of alerts that are benign (goal: <20%)
     - Alert volume: Are we overwhelming SOC with noise?
     - Time to detect (TTD): How long from attack start to rule firing? (goal: <1 hour)
   - **Feedback Loop**: Adjust rules based on incidents
     - If incident occurred but rule didn't fire: rule is missing detection (improve)
     - If rule fires on benign activity: too sensitive (tune threshold or add exclusions)
   - **Review**: Quarterly review of rule effectiveness; disable unused rules

## Anti-Patterns

- Alert on every possible event (alert fatigue); **prioritize high-confidence detections**
- No tuning (high false positive rate); **baseline against historical data; add exclusions**
- Rules so specific they miss variations (evasion); **balance specificity and generality**
- No testing before deployment (breaks production); **test rules before pushing to production SIEM**
- Rules never updated (miss new attack techniques); **quarterly rule review and update**

## Further Reading

- MITRE ATT&CK Detection Engineering: https://attack.mitre.org/resources/detections-and-signatures/
- Splunk Detection and Response: https://www.splunk.com/en_us/resources/white-papers/enterprise-security.html
- Sigma Rule Format (Open Detection Format): https://github.com/SigmaHQ/sigma
- SANS Detection Engineering: https://www.sans.org/cyber-security-courses/detection-engineering-essentials/
