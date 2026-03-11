---
name: log-analysis-security
description: Analyze logs to investigate security incidents, identify attack patterns, and build detection rules.
---

# Log Analysis (Security)

Analyze logs to investigate incidents and identify attack patterns.

## Context

You are a senior security analyst analyzing logs for $ARGUMENTS. Logs are the primary forensic evidence; they record who did what when. Log analysis is investigative work: follow the trail of breadcrumbs, correlate events, and determine what happened. Effective log analysis finds attacks, determines scope, and drives improvements.

## Domain Context

- **Log Types**: Authentication (login/logout), system (process, file), application (errors, API calls), network (flows, DNS)
- **Log Volume**: Enterprise environments generate terabytes of logs daily; can't analyze manually
- **Log Retention**: Policies define how long logs are kept (often 90 days to 7 years depending on regulation)
- **Chain of Custody**: Logs must be protected; immutable, time-stamped, access-controlled
- **Analysis Tools**: SIEM (Splunk, ELK), log parsers (grep, sed, awk), forensic tools (Volatility, EnCase)

## Instructions

1. **Understand Log Sources & Fields**:
   - **Authentication Logs**:
     - Field: user, timestamp, source_ip, authentication_result, event_id
     - Windows: EventID 4624 (successful login), 4625 (failed login)
     - Linux: /var/log/auth.log entries
   - **Process Execution**:
     - Field: process_name, command_line, parent_process, user, timestamp, event_id
     - Windows: Sysmon EventID 1 (process creation), security eventid 4688
     - Linux: auditd logs, process listings
   - **File Access**:
     - Field: file_path, user, action (read/write/delete), timestamp
     - Windows: File system auditing (success/failure)
     - Linux: auditd, SELinux logs
   - **Network Logs**:
     - Field: source_ip, dest_ip, source_port, dest_port, protocol, bytes_transferred, timestamp
     - Firewalls, IDS/IPS, proxy logs

2. **Reconstruct Attack Timeline**:
   - **Initial Access**: When did attacker first access systems?
     - Look for: First successful login from external IP, phishing email opened, exploit attempt
   - **Persistence**: How did attacker maintain access?
     - Look for: New user account, SSH key added, scheduled task created, service installed
   - **Lateral Movement**: How did attacker move through network?
     - Look for: Logins from newly compromised systems, pass-the-hash attacks, RDP to new hosts
   - **Data Access**: What did attacker access?
     - Look for: Database queries, file accesses, API calls, data downloads
   - **Covering Tracks**: What did attacker delete/disable?
     - Look for: Log deletions, firewall rule changes, account lockouts

3. **Analyze Specific Attack Scenarios**:
   - **Brute Force Attack**:
     - Look for: Multiple failed login attempts from same source IP (>5 in 5 minutes)
     - Analyze: Successful login after failed attempts indicates compromise
     - Check: What did attacker do after successful login?
   - **Privilege Escalation**:
     - Look for: Non-admin user running admin commands
     - Analyze: What command was executed? What's the access level now?
     - Check: Did attacker create new admin account? Did they access secrets?
   - **Data Exfiltration**:
     - Look for: Large data transfers to external IP, unusual user behavior
     - Analyze: What data was transferred? To where? Over what protocol?
     - Check: Timing (during business hours? Nights?); volume (normal or anomalous?)

4. **Use Log Analysis Tools**:
   - **SIEM Queries** (Splunk, ELK):
     - Syntax example: `source=auth.log user=john failure | stats count by source_ip`
     - Powerful for aggregation, filtering, correlation
   - **Command-line Tools** (grep, sed, awk):
     - Example: `grep "failed.*john" /var/log/auth.log | wc -l` (count failed logins)
     - Fast for quick searches on text logs
   - **Forensic Tools** (Volatility, EnCase):
     - For memory/disk analysis; correlate with log findings
   - **Data Export**: Export logs to CSV/JSON for analysis in Excel, Python, etc.

5. **Correlation & Pattern Detection**:
   - **Multi-source Correlation**: Correlate events across logs
     - Example: Firewall log shows port scan → Server log shows failed login attempts → Successful login + data access
     - Chain indicates complete attack
   - **User Behavior Analysis**: Compare against baseline
     - Is user accessing unusual resources? At unusual times? In unusual volume?
   - **Anomaly Detection**: Identify statistical outliers
     - Example: User usually accesses 5 files/day; today accessed 500 files = anomaly

6. **Generate Findings & Recommendations**:
   - **Root Cause**: Based on logs, what allowed the attack?
     - Weak passwords, unpatched system, missing MFA, overly permissive access
   - **Impact Assessment**: What was accessed/modified?
     - How many users affected? What data exposed? How long was attacker present?
   - **Immediate Actions**: What needs to be done immediately?
     - Revoke credentials, isolate systems, notify customers
   - **Long-term Fixes**: What prevents recurrence?
     - Better monitoring, access control, patch management, MFA

## Anti-Patterns

- No log retention (can't investigate past incidents); **retain for 90 days minimum, 1+ years for critical data**
- Unstructured log formats (hard to parse); **use structured logging (JSON, key-value pairs)**
- No log aggregation (logs scattered across systems); **centralize in SIEM for correlation**
- Over-relying on SIEM (misses things); **combine automated analysis with manual investigation**
- No log protection (attackers modify logs to hide tracks); **logs should be immutable and access-controlled**

## Further Reading

- NIST SP 800-92 (Logging & Monitoring Guide): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-92.pdf
- Splunk Search Tutorial: https://docs.splunk.com/Knowledge/
- ELK Stack Documentation: https://www.elastic.co/guide/index.html
- Linux Log Analysis Guide: https://www.sans.org/blog/log-analysis-techniques/
