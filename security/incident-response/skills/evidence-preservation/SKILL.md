---
name: evidence-preservation
description: Preserve evidence during incident response to enable forensic analysis and maintain legal admissibility.
---

# Evidence Preservation

Preserve evidence during incident response for forensics and legal proceedings.

## Context

You are a senior forensic investigator managing evidence preservation for $ARGUMENTS. Evidence preservation is critical for determining "what happened" and may be needed for legal proceedings (criminal prosecution, civil litigation). Evidence mishandled or lost undermines investigation and may be inadmissible in court. Chain of custody is essential.

## Domain Context

- **Volatile Data**: RAM, cache, network buffers; lost when system shuts down
- **Persistent Data**: Disk, logs, backups; survives system shutdown
- **Chain of Custody**: Documentation of who handled evidence, when, why; proves integrity
- **Forensic Imaging**: Bit-level copy of storage; preserves all data including deleted files
- **Legal Standard**: Evidence may be needed in civil litigation or criminal prosecution; must be legally sound

## Instructions

1. **Identify Evidence to Preserve**:
   - **Volatile First**: Capture RAM before system shutdown (RAM data lost when power off)
     - Memory dump to isolated USB/network location
     - Use dd, FTK Imager, EnCase, or similar tool
   - **Disk Image**: Full forensic image of storage (bit-level copy)
     - Use dd, ddrescue, FTK Imager; preserve all data including deleted files
   - **Logs**: System logs, application logs, network logs, database logs
     - Export to immutable storage (write-once, time-stamped)
   - **Network Traffic**: PCAP files (packet capture) if available
   - **Configuration**: Running configuration, settings, installed software
   - **Artifacts**: Browser history, recent files, temporary files, cache

2. **Preserve Volatile Data (Before Shutdown)**:
   - **Memory Dump**:
     - Live acquisition from running system
     - Use dd: `dd if=/dev/mem of=/external_drive/memory.img bs=1M`
     - Or FTK Imager: Capture RAM to file on isolated storage
     - Hash (MD5/SHA256) for integrity verification
   - **Network Connections**: Use netstat/ss to capture active connections; may reveal attacker C2
   - **Process List**: Process snapshot; attacker may hide process but it's in memory
   - **Bash History**: Commands executed; attacker may delete .bash_history but it's in memory
   - **Open Files**: lsof output; shows what processes have open

3. **Preserve Persistent Data (Disk & Logs)**:
   - **Forensic Imaging**:
     - Full disk image before any remediation/analysis
     - Use dd: `dd if=/dev/sda of=/external_drive/disk.img bs=4K`
     - Or FTK Imager/EnCase: Creates .img/.E01 file
     - Hash entire image for integrity
   - **Log Preservation**:
     - System logs: /var/log (Linux), Event Viewer (Windows)
     - Application logs: database, web server, custom applications
     - Network logs: firewall, IDS/IPS, proxy
     - Export logs to immutable storage before rotation/deletion
   - **Backup Images**: If organization has backups, preserve relevant backup images
     - May reveal data at different points in time

4. **Chain of Custody Documentation**:
   - **Evidence Log**:
     - Unique identifier for each piece of evidence
     - Description (what, where, when)
     - Who collected it, when, how
     - Hash/checksum for verification
   - **Handling Log**:
     - Who handled evidence, when, why
     - Any analysis performed, by whom
     - Results/findings
   - **Storage**:
     - Where evidence is stored (location, access restrictions)
     - Who has access (limited to authorized personnel)
     - Audit log of access (who viewed evidence when)
   - **Integrity Verification**:
     - Re-hash evidence periodically to verify no tampering
     - Document any changes (new findings, re-analysis)

5. **Legal & Admissibility Considerations**:
   - **Authentication**: Evidence must be authenticated (is it what you claim it is?)
     - Chain of custody proves it hasn't been altered
     - Metadata (timestamps, hashes) prove integrity
   - **Relevance**: Evidence relevant to incident (shows what happened, how)
   - **Reliability**: Evidence collected using reliable methods (forensically sound imaging, not ad-hoc copying)
   - **Expert Witness**: Analyst must be able to testify about collection/analysis
   - **Legal Hold**: Once incident is detected, preserve all related data (may be needed in litigation)
     - Don't delete emails, logs, backups related to incident

6. **Long-term Storage & Retention**:
   - **Secure Storage**: Encrypt evidence at rest; access-controlled storage
   - **Retention Period**: How long to keep? (At least as long as statute of limitations; 3-7 years typical)
   - **Redundancy**: Store copies in multiple locations (prevent loss)
   - **Accessibility**: Ensure you can access evidence years later (format, media longevity)
   - **Metadata**: Document analysis findings; preserve analyst notes

## Anti-Patterns

- Destroying evidence before forensics (immediate shutdown); **preserve RAM first**
- No chain of custody documentation (evidence inadmissible); **meticulously document handling**
- Analyzing evidence on non-isolated system (analyst gets compromised); **use isolated forensic workstation**
- Overwriting evidence (deleting raw data after analysis); **keep original images indefinitely**
- No hash verification (evidence tampering undetectable); **hash at collection and access points**

## Further Reading

- NIST SP 800-86 (Evidence Preservation): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-86.pdf
- SANS Digital Forensics: https://www.sans.org/cyber-security-courses/digital-forensics-incident-handling/
- RFC 3227 (Guidelines for Evidence Handling): https://tools.ietf.org/html/rfc3227
- FBI Evidence Handling Guide: https://www.fbi.gov/services/information-management/foipa/privacy-impact-assessments
