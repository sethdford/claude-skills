# Incident Response Plan Template

## Executive Summary

[Overview of IR program, scope, and key objectives]

---

## Incident Classification & Escalation

| Severity     | Definition | MTTD Target | Response Team | Escalation         | Notification                               |
| ------------ | ---------- | ----------- | ------------- | ------------------ | ------------------------------------------ |
| **CRITICAL** | [Criteria] | [Time]      | [Teams]       | [To whom and when] | [Customer/Executive notification timeline] |
| **HIGH**     | [Criteria] | [Time]      | [Teams]       | [To whom and when] | [Customer/Executive notification timeline] |
| **MEDIUM**   | [Criteria] | [Time]      | [Teams]       | [To whom and when] | [Customer/Executive notification timeline] |
| **LOW**      | [Criteria] | [Time]      | [Teams]       | [To whom and when] | [Customer/Executive notification timeline] |

---

## Incident Response Team

### Roles & Responsibilities

| Role                        | Responsibility                                                  | Primary | Backup | Contact       |
| --------------------------- | --------------------------------------------------------------- | ------- | ------ | ------------- |
| **Incident Commander**      | Leads response; makes containment/recovery decisions; escalates | [Name]  | [Name] | [Phone/Email] |
| **Security Engineer**       | Investigates; collects evidence; determines scope               | [Name]  | [Name] | [Phone/Email] |
| **Infrastructure Engineer** | Executes containment; isolates systems; restores backups        | [Name]  | [Name] | [Phone/Email] |
| **Communications Officer**  | Notifies executives, customers, authorities                     | [Name]  | [Name] | [Phone/Email] |
| **Privacy Officer**         | Determines breach status; notification obligations              | [Name]  | [Name] | [Phone/Email] |
| **Database Administrator**  | Restores databases; validates integrity                         | [Name]  | [Name] | [Phone/Email] |

### On-Call Rotation

- **Weekly rotation**: [Rotation schedule]
- **Escalation path**: [If on-call unavailable, contact X]
- **Testing cadence**: [How often is on-call tested?]

---

## Detection & Alerting

### Alert Sources

| Source         | Alert Type   | Severity Assigned          | Action             |
| -------------- | ------------ | -------------------------- | ------------------ |
| [SIEM/IDS/etc] | [Alert type] | [How severity is assigned] | [Initial response] |

### Alert Thresholds

- [Example: 10 failed logins in 5 minutes → potential brute-force]
- [Example: Data exfiltration >1 GB → potential breach]
- [Example: Privilege escalation to admin → immediate investigation]

### Initial Triage Procedure

1. Alert received → [Process]
2. Validate alert (is it real?) → [Decision criteria]
3. Assign severity → [Use classification table above]
4. Escalate to incident commander → [Timeline]
5. Initiate incident war room → [Communication channel/tools]

---

## Containment & Investigation Runbook

### Phase 1: Preserve Evidence (CRITICAL)

- [ ] Collect volatile data (open connections, memory state, running processes)
- [ ] Create forensic image of affected systems (do not shut down without imaging)
- [ ] Preserve logs: application logs, system logs, network logs
- [ ] Document timeline: when was attack first detected? When did it occur?

**Tools/Commands**:

```
[List commands for memory dump, log collection, forensic imaging]
```

### Phase 2: Isolate Compromised Systems

- [ ] Disconnect from network (physically if needed)
- [ ] Disable affected user accounts
- [ ] Revoke API keys and access tokens
- [ ] If worm suspected: isolate entire subnet
- [ ] Document actions taken and timestamps

**Tools/Commands**:

```
[List commands for network isolation, account disabling, token revocation]
```

### Phase 3: Investigation

**Key Questions to Answer**:

- When did the attacker first gain access? (look for first suspicious activity)
- What systems did they touch? (trace lateral movement)
- What data was accessed/exfiltrated? (scope of impact)
- How did they get in? (entry point analysis)
- Is attacker still active? (check for persistence mechanisms)

**Investigation Procedure**:

1. Review logs for: [Specific log sources and what to look for]
2. Check for persistence: [Backdoors, changed passwords, new accounts, scheduled tasks]
3. Analyze network traffic: [Look for command & control, data exfiltration]
4. Interview affected users: [Phishing, unusual access, account compromise]

### Phase 4: Threat Analysis

- [ ] Is attacker still active? [Evidence: yes/no]
- [ ] Type of attack: [Ransomware / Data theft / DDoS / Account compromise / etc]
- [ ] Estimated data volume: [If exfiltration]
- [ ] Number of affected systems: [Count]
- [ ] Number of affected customers: [Count]

### Phase 5: Recovery Decision

**Option 1: Full System Rebuild** (Safest)

- Wipe and restore from clean backup
- Timeline: [Estimated hours]
- Data loss risk: [Acceptable/Unacceptable]

**Option 2: Surgical Removal** (If possible)

- Remove malware without rebuilding
- Confidence level: [High/Medium/Low]
- Timeline: [Estimated hours]

**Option 3: Patch & Harden**

- Patch exploited vulnerability
- Timeline: [Estimated hours]

**Decision**: [Which option chosen and why]

---

## Recovery Procedures

- [ ] Restore systems from [backup location]
- [ ] Patch vulnerability that was exploited
- [ ] Test systems post-recovery
- [ ] Validate backup integrity
- [ ] Re-enable MFA/rotate credentials
- [ ] Tighten firewall rules
- [ ] Timeline: [Expected completion time]

---

## Communication Template

### Internal Status Update (Every 4 hours during incident)

```
Subject: [INCIDENT SEVERITY] - [Brief description] - Status Update #[N]

Current Status: [Timeline since detection]
Severity: [Critical/High/Medium/Low]

What we know:
- [Key facts discovered]
- [Scope of impact]
- [Current status: investigating/contained/recovering/resolved]

What we're doing:
- [Current actions]
- [Next steps]

Timeline of actions:
- [HH:MM] [Action taken]
- [HH:MM] [Action taken]

Expected next update: [Time]

Questions: [Contact]
```

### Customer Notification (if data breach)

```
Subject: Important Security Update Regarding Your Account

Dear [Customer],

We identified unauthorized access to our systems on [date]. Our investigation shows [describe what happened].

What data was affected:
- [List of data types accessed]

What we're doing:
- [Containment steps]
- [Recovery steps]
- [Preventive measures]

What you should do:
- [Recommended actions for customer: change password, monitor credit, etc]

We provide [X months free monitoring/credit protection service].

Contact us at [support email] for questions.
```

---

## Post-Incident Review (Blameless)

**Timeline**: Review to be conducted within 2 weeks of resolution.

**Participants**: [Incident commander, security team, engineering leads]

### Incident Timeline

- [HH:MM] [What happened]
- [HH:MM] [What happened]
- [Timeline to be filled in during PIR]

### Root Cause Analysis

**Primary cause**: [Why did this happen?]

**Contributing factors**: [What made it possible?]

**Failure points**: [Where did we miss this?]

### Impact Assessment

- Customers affected: [Number]
- Data types compromised: [List]
- Revenue impact: [Estimated]
- Reputation impact: [Assessment]

### What Went Well

- [Response element that worked]
- [Coordination that was smooth]
- [Team member who excelled]

### What Didn't Go Well

- [Delay or confusion]
- [Missing information]
- [Process failure]

### Action Items

| Item                                    | Owner      | Deadline | Status |
| --------------------------------------- | ---------- | -------- | ------ |
| [Technical fix: patch vulnerability]    | [Engineer] | [Date]   | [ ]    |
| [Process fix: improve detection]        | [Security] | [Date]   | [ ]    |
| [Training: incident response refresher] | [Lead]     | [Date]   | [ ]    |

---

## Training & Exercises

### Annual Training

- **Audience**: All staff
- **Content**: [IR basics, how to report incidents, what not to do]
- **Frequency**: Annually (recommend September)
- **Duration**: [30-60 minutes]

### Semi-Annual Tabletop Exercises

**Exercise 1** (Q2): [Scenario - e.g., ransomware on database]

**Exercise 2** (Q4): [Scenario - e.g., data breach discovery]

Each exercise includes:

- Scenario description
- Start time and timeline of events
- Debrief discussion
- Lessons learned

---

## Critical Assets & Backups

| Asset             | Type              | Location   | Backup Frequency | Restore Time |
| ----------------- | ----------------- | ---------- | ---------------- | ------------ |
| [System/Database] | [Production/Data] | [Location] | [Daily/Weekly]   | [Est. hours] |

---

## Vendor & Third-Party Contacts

| Service                  | Primary Contact | Phone   | Email   | Notes        |
| ------------------------ | --------------- | ------- | ------- | ------------ |
| [Hosting provider]       | [Name]          | [Phone] | [Email] | [Account ID] |
| [Incident response firm] | [Name]          | [Phone] | [Email] | [Contract #] |
| [Forensics provider]     | [Name]          | [Phone] | [Email] | [Contract #] |

---

## Document Metadata

| Property         | Value                |
| ---------------- | -------------------- |
| Owner            | [Security Lead]      |
| Created          | [Date]               |
| Last Updated     | [Date]               |
| Review Frequency | [Quarterly/Annually] |
| Next Review      | [Date]               |
