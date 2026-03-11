---
name: containment-strategy
description: Develop containment strategies to isolate compromised systems, prevent lateral movement, and stop ongoing attacks.
---

# Containment Strategy

Develop containment strategies to isolate compromise and stop ongoing attacks.

## Context

You are a senior incident response engineer developing containment strategies for $ARGUMENTS. Containment is the critical phase between detection and investigation: stop the attack, prevent lateral movement, and preserve evidence. Poor containment allows attackers to pivot, exfiltrate data, or cause further damage.

## Domain Context

- **Containment Levels**: Short-term (immediate isolation), medium-term (patching/hardening), long-term (full remediation)
- **Lateral Movement**: After initial compromise, attackers move across network; segmentation limits movement
- **Data Exfiltration**: Attackers often exfiltrate data during incident; network monitoring detects/blocks
- **Evasion**: Attackers may detect containment (firewall blocks, credentials revoked) and attempt escape
- **Business Continuity**: Containment may disrupt services; balance security vs. availability

## Instructions

1. **Isolate Compromised System (Short-term)**:
   - **Network Isolation**: Disconnect from network (disable network port, revoke DHCP, block firewall)
     - Immediate: Disconnect physically or disable network port
     - System stays on: Preserve memory, logs for forensics
   - **Account Isolation**: Revoke compromised user/service account credentials
     - Change password, revoke API keys, revoke OAuth tokens
     - Monitor for re-use (attacker may try to log in again)
   - **Credential Review**: If user account compromised, review what that user can access
     - Are they admin? Can they access secrets? Databases? Customer data?
     - Might need broader isolation if admin account compromised

2. **Prevent Lateral Movement (Short-term)**:
   - **Network Segmentation**: Ensure compromised system can't reach other systems
     - Review firewall rules (between tiers); should deny by default
     - If segmentation is missing, block at firewall: source IP address, destination port
   - **Credential Rotation**: Revoke/rotate credentials accessible from compromised system
     - Database credentials, API keys, SSH keys, service account passwords
     - Attacker may have harvested credentials; rotate to prevent use
   - **Enable Monitoring**: Enhanced monitoring on adjacent systems for signs of lateral movement
     - Failed login attempts, unusual access patterns, process execution, network connections

3. **Investigation While Contained**:
   - **Preserve Evidence**: Before remediation, collect forensic evidence
     - Memory dump, disk image, logs
   - **Analysis**: While systems are isolated, analyze to determine:
     - Attack vector (how did attacker get in?)
     - Duration (how long has attacker had access?)
     - Scope (what systems affected? what data accessed?)
     - Intent (is attacker still active or was this historical?)
   - **Decision**: Based on analysis, decide on remediation approach

4. **Remediation Strategy**:
   - **System Rebuild**: Wipe and rebuild from clean baseline
     - Extract forensic image first
     - Restore from backup or redeploy from Infrastructure as Code
     - Re-apply patches; re-harden
   - **Surgical Remediation**: If feasible, remove attacker without full rebuild
     - Patch vulnerability, disable attacker tools/accounts, monitor for re-infection
     - Requires confidence in analysis; risk of incomplete remediation
   - **Validation**: After remediation, verify system is clean
     - Antivirus scan, HIDS check, forensic re-imaging

5. **Prevent Re-infection & Ongoing Monitoring**:
   - **Patch Vulnerability**: Apply patch to prevent re-exploitation
     - Test patch in staging first; deploy to production post-incident
   - **Monitor for Re-infection**: Enhanced monitoring for 30-90 days
     - Alert on suspicious activity from remediated system
     - Alert on re-use of attacker-associated IPs/domains
   - **Hunt for Related Indicators**: Using IoCs (file hashes, IPs, domains), search for similar activity across infrastructure
     - May find additional compromised systems
   - **Lessons Learned**: Post-incident, determine what allowed compromise and prevent recurrence

## Anti-Patterns

- Insufficient isolation (leaving backdoors/accounts); **thoroughly isolate; audit what needs cleaning**
- Remediation without understanding attack (same vulnerability exploited again); **patch root cause, not symptom**
- No monitoring after remediation (re-infection undetected); **enhanced monitoring for months post-incident**
- Rebuilding too quickly (evidence lost); **preserve evidence before remediation**
- Containment causes business outage (over-reaction); **balance security and business continuity**

## Further Reading

- NIST SP 800-61 (Containment Strategies): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf
- SANS Incident Response (Containment): https://www.sans.org/incident-response/
- CIS Controls (Detection & Response): https://www.cisecurity.org/cis-controls/
- Mitre ATT&CK (Lateral Movement Techniques): https://attack.mitre.org/tactics/TA0008/
