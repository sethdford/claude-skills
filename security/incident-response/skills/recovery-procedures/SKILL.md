---
name: recovery-procedures
description: Establish recovery procedures to restore systems, verify integrity, and validate business continuity after incidents.
---

# Recovery Procedures

Establish recovery procedures to restore systems and verify integrity post-incident.

## Context

You are a senior incident recovery engineer designing recovery procedures for $ARGUMENTS. Recovery is the phase after containment where systems are restored and services resume. Poor recovery leads to re-infection, undetected compromises, or continued data exfiltration. Recovery must be thorough: wipe/rebuild from clean baseline, verify integrity, monitor for re-infection.

## Domain Context

- **Recovery Strategies**: Clean rebuild (safest), surgical remediation (faster but riskier), hybrid (critical systems rebuilt, others patched)
- **Verification**: Before declaring recovery complete, verify systems are clean (scans, forensics, monitoring)
- **Testing**: Test critical workflows before resuming production
- **Monitoring**: Enhanced monitoring post-recovery for signs of re-infection

## Instructions

1. **Plan Recovery Strategy**:
   - **Full Rebuild (Recommended)**:
     - Wipe disk; restore from clean backup or redeploy from Infrastructure as Code
     - Most thorough; requires pre-built baselines and good backups
     - Time: Hours to days depending on system complexity
   - **Surgical Remediation**:
     - Patch vulnerability; remove attacker tools/accounts; harden
     - Faster but risks incomplete remediation
     - Only if confident in scope analysis
   - **Hybrid Approach**:
     - Critical systems: full rebuild
     - Non-critical: surgical remediation
   - **Decision**: Based on incident severity, system importance, available baselines/backups

2. **Execute Rebuild/Remediation**:
   - **Pre-Remediation**:
     - Extract forensic evidence (memory dump, disk image)
     - Document current state (screenshots, logs, configuration)
   - **Remediation**:
     - If full rebuild:
       - Deploy from clean baseline (VM template, Infrastructure as Code)
       - Restore data from clean backup (before compromise)
       - Re-apply patches (to prevent re-exploitation)
     - If surgical:
       - Apply patch to fix vulnerability
       - Remove attacker-installed tools, files, accounts
       - Change credentials (passwords, keys)
       - Disable attacker access points (backdoors, persistence mechanisms)
   - **Configuration Verification**:
     - Verify system is hardened per baseline
     - Check security settings (firewall, antivirus, logging)
     - Verify no unnecessary services enabled

3. **System Validation**:
   - **Security Scanning**:
     - Vulnerability scan (missing patches, misconfigurations)
     - Malware scan (antivirus, malware bytes)
     - Port scan (open ports, unexpected services)
     - Log review (no suspicious activity post-remediation)
   - **Functional Testing**:
     - Critical workflows: Can the system do its job?
     - Data integrity: Are backups complete and correct?
     - Connectivity: Does system connect to other systems as expected?
     - Performance: Is system performing at baseline?
   - **Forensic Validation**:
     - Re-image remediated system; compare to forensic image
     - Verify attacker artifacts are gone
     - Verify clean files are restored correctly

4. **Testing & Validation**:
   - **Unit Testing**: Test individual system functions
   - **Integration Testing**: Test system interaction with other systems
   - **End-to-End Testing**: Test critical user workflows
   - **Load Testing**: Verify system can handle normal load
   - **Security Testing**: Penetration test to verify vulnerabilities fixed
   - **Regression Testing**: Ensure remediation didn't break anything else
   - Document test results; identify any issues

5. **Production Resumption**:
   - **Staged Rollout**: Resume gradually (not all at once)
     - Internal testing first, then pilot users, then general availability
     - Monitor for issues; rollback if problems arise
   - **Communication**: Notify customers/stakeholders of resumption
     - Incident is over; systems are restored; here's what we learned
   - **Credentials Reset**: Require password reset for users with potentially compromised credentials
   - **Monitoring**: Enhanced monitoring post-recovery (see Anti-Patterns)

6. **Post-Recovery Verification**:
   - **Monitoring Period**: 30-90 days of enhanced monitoring post-recovery
     - Alert on suspicious activity (re-infection attempts, similar attack patterns)
     - Alert on re-use of attacker-associated IPs/domains
   - **Indicators of Compromise (IoCs)**: Hunt for IoCs (file hashes, IPs, domains) across infrastructure
     - May find additional compromised systems
   - **Security Improvements**: Deploy mitigations identified in RCA
     - Patch vulnerability, improve monitoring, strengthen access control
   - **Lessons Learned**: Document what went well, what didn't; improve processes

## Anti-Patterns

- Resuming production before validation (re-infection risk); **verify systems are clean before resuming**
- Restoring from infected backups; **ensure backup pre-dates compromise**
- No enhanced monitoring post-recovery (re-infection undetected); **monitor closely for 30-90 days**
- Resuming all at once (overwhelming support if issues); **staged rollout allows rapid rollback**
- No functional testing (system broken post-remediation); **test critical workflows before general resumption**

## Further Reading

- NIST SP 800-61 (Recovery Procedures): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf
- SANS Incident Recovery: https://www.sans.org/incident-response/
- Disaster Recovery Planning: https://www.nist.gov/publications/contingency-planning-guide-federal-information-systems
- Business Continuity Institute (BCM): https://www.bcibd.org/
