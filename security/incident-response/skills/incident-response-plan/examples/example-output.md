# Example: Incident Response - Ransomware Attack Scenario

## Incident Overview

**Scenario**: Ransomware detected on production database servers.

**Timeline**: 2026-03-10 (Friday) 9:47 AM - 5:00 PM + Monday morning post-mortem

**Final Impact**: No customer data lost; 4-hour recovery; full incident response executed

---

## Incident Timeline

### Detection Phase (9:47 AM)

**09:47** — Automated alert fires:

- Monitoring system detects 500+ files renamed with `.locked` extension in database directory
- Alert severity: **CRITICAL** (infection pattern matches known ransomware)
- Alert sent to: SOC dashboard, Slack #incidents, paged on-call security engineer

**09:52** — Initial triage:

- SOC analyst confirms alert is real (not false positive)
- Escalates to incident commander: Robert Kim (VP Security)
- Initiates war room: Slack channel #ransomware-incident, Zoom bridge established
- Participants: Robert (IC), Sarah (DB team), James (Infrastructure), Lisa (Security engineer), Carol (Comms officer)

### Initial Response (10:00 - 10:30)

**10:00** — Incident commander briefing:

- Robert: "We have ransomware on the database server. Timeline so far?"
- James: "File encryption started ~9:15 AM (logs show first `.locked` files at 9:15). Only database directory affected so far. No other systems showing signs of infection."
- Sarah: "Database is still responding. I can see ~10K files encrypted. Last clean backup is from 4 AM this morning (5 hours of potential data loss)."
- Robert: "Is backup integrity verified?" Sarah: "Yes, tested quarterly. Clean."

**10:15** — Decision: Shut down database server

- Goal: Stop encryption from spreading; preserve evidence; prevent attacker communication
- Risk: Some in-flight transactions lost (acceptable)
- Action: Isolate server from network; take snapshot for forensics

**10:30** — Isolation complete:

- Database server disconnected from network
- Database process killed (locks data, prevents further corruption)
- Forensic image created (will take 30 min, runs in background)
- Team: Document all actions with timestamps

### Investigation Phase (10:30 - 12:00)

**10:45** — Security investigation begins:

- Lisa: Checking server logs for unauthorized access
- "Found it. SSH login at 8:47 AM from IP 203.45.67.89. User: contractor_dev"
- Access method: Contractor's laptop logged into company VPN; credentials were 6 months old (still valid)
- Lisa: "No evidence of lateral movement yet. Attacker stayed on database server only."

**11:00** — Contractor laptop analysis:

- Contacted contractor; asking for their laptop for forensics
- Confirmed: Laptop was left unattended Friday morning at coffee shop
- Attacker likely got VPN credentials from laptop

**11:30** — Forensic timeline:

- 8:47 AM: Attacker SSH login with contractor credentials
- 9:00 AM: Downloaded ransomware binary (wget from malware-as-a-service site)
- 9:15 AM: Ransomware executed; encryption started
- 9:30 AM: Ransom note created; attacker demanded $50K in Bitcoin

**12:00** — Recovery decision:

- Confirmation: Attacker NOT still on server (no persistence mechanisms found)
- Data exfiltration: No evidence of data leaving server (would take hours)
- Recovery plan: Full rebuild from 4 AM backup

### Recovery Phase (12:00 - 5:00 PM)

**12:15** — Restore begins:

- Sarah: Starting full database restore from 4 AM backup
- Estimated time: 3 hours (large database)
- Validation: Running integrity checks post-restore

**1:00 PM** — Customer communication drafted:

- Carol (Comms): "We identified and contained a security incident affecting our infrastructure. Our database was encrypted by ransomware. We have NO evidence that customer data was accessed or exfiltrated. Our systems are being restored from clean backups."
- Draft shared with legal/privacy team for approval

**2:30 PM** — Exec briefing:

- Robert to CEO: "Ransomware attack contained. No customer data compromised. Restoring from backup now. Expected full recovery by 5 PM. Root cause: contractor laptop lost at coffee shop. We're implementing new security controls."

**3:45 PM** — Database restore complete:

- Sarah: "Restore finished. Running validation tests."
- Validation: ✅ All data integrity checks passed
- No data loss (4 hours of potential transactions lost, but no permanent damage)

**4:30 PM** — Database brought back online:

- Monitoring confirms: Database responding normally
- Customer systems can reconnect

**5:00 PM** — Customer notification sent:

- Email to all customers: "We experienced a brief security incident this morning. All data is safe. Services restored. Here's what happened and what we're doing."
- Support team alerted for incoming questions

### Post-Incident Phase (Monday)

**Monday 10:00 AM** — Post-mortem meeting:

- Participants: Robert, Sarah, James, Lisa, Carol, legal, product lead
- Timeline review: Confirmed facts from logs
- Root cause: Contractor laptop compromised (left unattended)
- Contributing factors:
  - VPN credentials not rotated in 6 months
  - No MFA on VPN access
  - Database server not isolated in network segment
  - No backup testing automation (lucky that backup worked)

**Action items from post-mortem**:

| Item                                                 | Owner  | Deadline  | Priority |
| ---------------------------------------------------- | ------ | --------- | -------- |
| Implement MFA for VPN access                         | James  | 2 weeks   | Critical |
| Rotate all contractor credentials immediately        | Robert | Today     | Critical |
| Audit all external access (VPN, SSH keys)            | Lisa   | This week | Critical |
| Implement network segmentation (database isolated)   | James  | 30 days   | High     |
| Automate backup testing (weekly integrity checks)    | Sarah  | 30 days   | High     |
| Upgrade monitoring to detect encryption patterns     | Lisa   | 2 weeks   | High     |
| Contractor device policy (must use company hardware) | HR     | This week | Medium   |
| Customer communication about security improvements   | Carol  | 1 week    | Medium   |

---

## Incident Severity Assessment

**Classification**: CRITICAL

**Justification**:

- Production database was encrypted
- All customers could have been affected
- Recovery was time-sensitive

**Downtime**: ~5 hours (from detection to full recovery)

**Customer impact**: None (no data loss, services restored)

**Revenue impact**: Minimal (no SLA breach; customers understand; good communication)

---

## What Went Well

1. **Fast detection** (within 2 minutes of ransomware executing): Automated monitoring worked
2. **Quick escalation**: On-call team responded immediately
3. **Clear incident commander**: Robert made decisive choices (shut down, restore)
4. **Backup strategy paid off**: 4 AM backup was clean and working
5. **Good communication**: Customers notified quickly with facts
6. **Forensics-aware**: Isolated before recovery, preserved evidence
7. **Team coordination**: Cross-functional team (DB, Infra, Security, Comms) all worked smoothly

---

## What Didn't Go Well

1. **Contractor credential reuse**: Same credentials for 6 months
2. **No MFA on VPN**: Only password required; lost laptop = full access
3. **No network segmentation**: Attacker could have spread; got lucky they didn't
4. **Manual backup testing**: Didn't find out if restore worked until incident
5. **No encryption detection tuning**: False positives didn't alert earlier
6. **Contractor device policy**: No requirement to use company hardware (contractor brought personal laptop)

---

## Lessons Learned

| Lesson                            | Action                                               |
| --------------------------------- | ---------------------------------------------------- |
| Credential rotation is critical   | Implement 90-day rotation for all external access    |
| MFA is not optional               | Enforce on VPN, not just applications                |
| Network segmentation saves lives  | Implement zero-trust networking                      |
| Backups are only good if tested   | Automate backup verification                         |
| Encryption monitoring is valuable | Tune detection to flag unusual file operations       |
| Incident response playbooks work  | This scenario matched our plan; execution was smooth |
| Communication matters             | Customers appreciated transparency; no trust damage  |

---

## Financial Impact

| Category                      | Amount      | Notes                                       |
| ----------------------------- | ----------- | ------------------------------------------- |
| Incident response costs       | $5,000      | Team time (5 people × 4 hours)              |
| Forensic imaging              | $2,000      | External firm analysis                      |
| Backup restore costs          | $1,000      | Infrastructure resources                    |
| Contractor laptop replacement | $1,500      | Device was compromised                      |
| Customer support overhead     | $3,000      | Extra support calls, comms                  |
| **Total**                     | **$12,500** | Relatively low because we contained quickly |

---

## Customer Communication (Sent 5 PM)

```
Subject: Important Security Update — Infrastructure Incident

Dear [Customer],

This morning, we detected and quickly contained a security incident affecting our
production infrastructure. Here's what happened:

WHAT HAPPENED:
At 9:47 AM PT, automated monitoring detected unauthorized encryption on one of our
database servers. Upon investigation, we determined that a contractor's computer was
compromised, giving attackers access to our VPN.

WHAT WE DID:
1. Immediately isolated the affected server to prevent spread
2. Confirmed no attacker access to other systems
3. Verified that customer data was not accessed or copied
4. Restored all services from clean backups by 5 PM

YOUR DATA IS SAFE:
- No customer data was accessed or compromised
- All services are fully operational
- Your data integrity is verified

WHAT WE'RE DOING:
1. Implementing multi-factor authentication (MFA) on VPN access (2 weeks)
2. Network isolation for databases (30 days)
3. Automatic backup integrity testing (30 days)
4. Enhanced encryption detection (2 weeks)
5. Updated contractor security policies

QUESTIONS?
Our team is available 24/7 at support@company.com. We've included a detailed
FAQ below.

We take security seriously and appreciate your trust during this incident.

— The Security Team
```

---

## Metrics & KPIs

| Metric                         | Target   | Actual    | Status                  |
| ------------------------------ | -------- | --------- | ----------------------- |
| MTTD (Mean Time to Detect)     | <1 hour  | 2 minutes | ✅ Excellent            |
| MTTR (Mean Time to Recover)    | <4 hours | 5 hours   | ⚠️ Good (slightly over) |
| Data Loss                      | 0        | 0         | ✅ Zero data loss       |
| Customer Impact                | Minimal  | None      | ✅ No impact            |
| Root Cause Found               | Yes      | Yes       | ✅ Clear                |
| Preventive Controls Identified | Yes      | Yes       | ✅ 4 major controls     |

---

## Sign-Off

**Incident Status**: ✅ **CLOSED** (Monday 2 PM)

**Approval**:

- Robert Kim (VP Security): ********\_******** Date: 2026-03-11
- Sarah Chen (DB Lead): ********\_******** Date: 2026-03-11
- CEO: ********\_******** Date: 2026-03-11

**Next Review**: Action items tracked in Jira; next check-in: 2026-04-10 (30 days)
