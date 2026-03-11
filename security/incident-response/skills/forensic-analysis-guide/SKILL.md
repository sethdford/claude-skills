---
name: forensic-analysis-guide
description: Conduct forensic analysis to determine attack vectors, scope of compromise, and evidence for legal proceedings.
---

# Forensic Analysis Guide

Conduct forensic analysis to determine attack vectors, scope, and evidence.

## Context

You are a senior forensic investigator analyzing security incidents for $ARGUMENTS. Forensics determines "what happened": attack vector, duration, scope of compromise, data accessed. Forensics requires careful evidence preservation (chain of custody), technical analysis (logs, artifacts, memory), and documentation (admissible in court if needed).

## Domain Context

- **Forensic Evidence**: Disk images, memory dumps, logs, network traffic, artifacts (registry, filesystem)
- **Chain of Custody**: Document who handled evidence, when, why; ensures admissibility in court
- **Tools**: EnCase, FTK, volatility (memory), WireShark (network), Autopsy, grep/sed/awk (log analysis)
- **Timeline**: Reconstructing timeline of attack (when accessed, what changed)
- **Indicators of Compromise (IoCs)**: File hashes, IP addresses, domain names, file paths used by attacker

## Instructions

1. **Evidence Preservation**:
   - **Volatile Data**: Capture memory dump immediately (RAM is lost when system shuts down)
     - Use dd, FTK Imager, or similar; capture RAM to file before system shutdown
   - **Disk Image**: Create forensic image of compromised disk (bit-level copy)
     - Use dd, FTK Imager, ddrescue; preserve on isolated storage
   - **Chain of Custody**: Document who handled evidence, when, why; secure storage; access logs
   - **Hash Verification**: MD5/SHA256 hash of evidence; verify integrity after analysis
   - **Live Acquisition**: If system must stay running, collect logs/artifacts while running (secondary to disk image)

2. **File System Analysis**:
   - **Deleted Files**: Recover deleted files (attacker may delete evidence; but data remains until overwritten)
   - **File Metadata**: Modify/create/access times (when was file created/modified?)
   - **Alternative Data Streams** (Windows): Hidden streams where attacker may store tools/data
   - **Registry Analysis** (Windows): Software execution, user activity, network connections
   - **Bash History** (Linux): Commands executed; attacker may try to delete history
   - **Artifacts**: Browser history, recently opened files, thumbnail cache (images user opened), shadow copy (backups)

3. **Log Analysis**:
   - **Chronological Reconstruction**: Create timeline of events
     - Authentication logs: Failed logins, new accounts, privilege escalation
     - System logs: Process execution, service started/stopped, driver installation
     - Network logs: Connections to suspicious IPs, data exfiltration
     - Application logs: Errors, warnings, access logs
   - **Suspicious Indicators**: New user accounts, disabled security software, outbound connections, data access patterns
   - **Correlation**: Correlate events across systems (log into server A, then access data on server B)

4. **Memory Analysis**:
   - **Process Analysis**: What processes were running? Attacker may hide process
   - **Network Connections**: Active network connections at time of capture
   - **Command-Line Arguments**: What commands were executed? (attacker may clear shell history but command is in memory)
   - **DLL Injection**: Attacker may inject malicious DLL into legitimate process
   - **Rootkits**: Detect kernel-level rootkits hiding files/processes
   - **Volatility Plugins**: process_list, netscan, pslist, dlllist, cmdline, etc.

5. **Create Forensic Report**:
   - **Executive Summary**: What happened? Attack vector? Scope? Data accessed?
   - **Timeline**: Chronological sequence of events
   - **Technical Analysis**: Detailed findings (files modified, accounts created, connections made)
   - **Attack Chain**: How did attacker get in? What did they do? How did they cover tracks?
   - **Indicators of Compromise**: File hashes, IPs, domains, patterns to hunt for across infrastructure
   - **Recommendations**: Remediation, hardening, detection improvements
   - **Artifacts**: Evidence directory with images, logs, screenshots
   - **Chain of Custody**: Documentation of evidence handling

## Anti-Patterns

- Shutting down compromised system immediately (destroying volatile evidence); **preserve memory first**
- Analyzing on non-isolated system (attacker can attack analyst); **use isolated forensic workstation**
- No chain of custody (evidence inadmissible in court); **document handling meticulously**
- Analysis without proper logging (can't reproduce findings); **document every step**
- Making conclusions without evidence (bias); **follow evidence; be conservative**

## Further Reading

- NIST SP 800-86 (Forensic Examination): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-86.pdf
- Volatility Documentation: https://github.com/volatilityfoundation/volatility/wiki
- SANS Forensics: https://www.sans.org/cyber-security-courses/forensic-security/
- Chain of Custody Best Practices: https://www.nist.gov/document/chain-custody
