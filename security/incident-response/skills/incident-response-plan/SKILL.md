---
name: incident-response-plan
description: Develop comprehensive incident response plans with clear roles, procedures, communication protocols, and recovery workflows. Use when establishing IR processes, conducting tabletops, or updating response procedures after incidents.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# Incident Response Planning

Build a comprehensive incident response program with clear roles, procedures, severity classifications, and communication protocols to minimize mean time to detection (MTTD) and mean time to resolution (MTTR).

## Context

You are building or improving an incident response (IR) program. A strong IR program doesn't prevent all incidents, but it dramatically reduces their impact. Organizations without plans suffer: longer detection time, chaotic response, poor communication, and higher customer impact. An effective plan is practiced, documented, and clear on roles.

IR is not a one-time document; it's a living program that improves after each incident through post-mortems and tabletop exercises.

## Domain Context

- **Incident Categories**: Malware, phishing, data breach, ransomware, DDoS, account compromise, insider threat, supply chain attack, compliance violation
- **Response Phases**: Detection → Triage → Containment → Investigation → Recovery → Post-Incident Review
- **Incident Classification**: Severity (Critical, High, Medium, Low) drives response speed and escalation
- **MTTD (Mean Time to Detect)**: How quickly is an incident discovered? Goal: <1 hour for critical
- **MTTR (Mean Time to Resolve)**: How quickly is an incident resolved? Goal: <4 hours for critical
- **Communication**: Incident commander coordinates response; clear escalation ensures executive/customer awareness
- **Evidence preservation**: Don't destroy evidence in haste to recover; forensics may be needed

## When to Use This Skill

- You're building a security operations center (SOC) or IR program
- Your team has experienced incidents and needs a structured process
- Customers or auditors require an incident response plan
- You're conducting tabletop exercises to test readiness
- You're updating IR procedures after an incident

## Prerequisites

Before building the plan, identify:

1. **Incident types relevant to your business**: What threats matter most? (Data breach for SaaS; ransomware for healthcare; DDoS for financial)
2. **Stakeholders**: Who needs to be involved? (Security, engineering, ops, legal, communications, finance, executive sponsor)
3. **Current detection capabilities**: What alerts do you have? (SIEM, intrusion detection, log monitoring, user reports)
4. **Infrastructure/data**: What systems are critical? Where is sensitive data stored? What's the business impact if compromised?
5. **Regulatory requirements**: What notification timelines are required? (GDPR 72 hours, state laws vary, contracts may require notification)

## Instructions

### 1. Define Incident Classification & Escalation

Create clear criteria for each severity level:

| Severity     | Definition                                                                                         | MTTD Target | Response Team                   | Escalation                                                           |
| ------------ | -------------------------------------------------------------------------------------------------- | ----------- | ------------------------------- | -------------------------------------------------------------------- |
| **CRITICAL** | Affects customer data, production systems down, widespread compromise, active exploitation         | <1 hour     | All-hands                       | Immediate notification to CEO, board, legal, customers               |
| **HIGH**     | Affects internal systems, customer disruption, unauthorized access attempt, 1-5 customers impacted | <4 hours    | Core IR team + engineering lead | VP Security notified within 1 hour; customer notification within 24h |
| **MEDIUM**   | Minor issue, contained impact, suspicious but unconfirmed, <10 employees affected                  | <24 hours   | On-call engineer + security     | Team lead notified; document for analysis                            |
| **LOW**      | Suspicious activity, low likelihood, security research, no impact                                  | <1 week     | Security team                   | Track for patterns; quarterly review                                 |

### 2. Establish the Incident Response Team

Define roles and responsibilities:

- **Incident Commander**: Leads response; makes decisions on containment/recovery; coordinates teams; updates executives
- **Security Engineer**: Investigates; collects evidence; determines scope and duration of compromise
- **Infrastructure Engineer**: Executes containment (isolate systems, kill processes, disable accounts); restores from backup
- **Communications Officer**: Notifies executives, customers, authorities; manages public narrative
- **Privacy Officer**: Determines if breach occurred; determines notification obligations; coordinates legal
- **Executive Sponsor**: Authorized to approve actions (take systems offline, spend emergency funds, authorize paid cleanup)
- **Database Administrator**: Restores databases; validates data integrity post-recovery
- **Network Engineer**: Isolates network segments; analyzes packet captures; implements controls

**Document**: On-call rotation; primary/backup for each role; contact list (phone + email); escalation path

### 3. Design Detection & Alerting

Establish alert standards:

- **Detection sources**: SIEM alerts, IDS/IPS, unusual access patterns, user reports, threat intelligence, application logs
- **Alert standards**: Clear criteria for what triggers escalation (10 failed logins in 5 min → lock account; unusual data access → investigate)
- **Initial triage**: Incident commander assesses severity; assigns response team; initiates IR process
- **Validation**: Not all alerts are real incidents; process to quickly validate before full escalation
- **Notification**: Alert SOC/on-call; page incident commander; initiate IR war room (Slack channel or bridge line)

**Example alert thresholds**:

- 10 failed login attempts within 5 minutes → potential brute-force attack
- Data exfiltration >1 GB from single user → potential breach
- Privilege escalation (user gains admin rights) → immediate investigation
- Database dump command executed → potential data theft

### 4. Containment & Investigation Procedures

Step-by-step actions:

**1. Preserve Evidence (CRITICAL)**:

- Don't shut down compromised systems immediately; preserve logs/memory
- Collect volatile data (open connections, running processes, memory state)
- Forensic imaging of affected systems

**2. Isolate Compromised Systems**:

- Disconnect from network (physically or virtually)
- Disable affected accounts
- Revoke API keys and access tokens
- If worm detected, isolate entire subnet

**3. Investigation**:

- Review logs (application, system, network) for:
  - When did attacker first gain access?
  - What systems did they touch?
  - What data was accessed or exfiltrated?
  - How did they get in? (phishing, vuln, weak credentials, supply chain?)
- Determine scope (how many systems, how much data, how many customers?)
- Timeline: When was first unusual activity? When was it detected? Why the gap?

**4. Threat Analysis**:

- Is attacker still active? Check for persistence mechanisms (backdoors, changed passwords, new accounts)
- Is this ransomware? Check for file extensions, ransom notes, encryption behavior
- Is this data exfiltration? Estimate data volume and sensitivity

**5. Decision on Recovery**:

- Full system rebuild (safest): Wipe and restore from clean backup
- Surgical removal (if possible): Remove malware without rebuilding; only if high confidence
- Patch-and-harden: If threat was a vulnerability, patch and restart

### 5. Recovery & Communication

**Recovery**:

- Restore systems from clean backups (not infected backups)
- Patch vulnerability that was exploited
- Test systems post-recovery; validate backups actually work
- Hardening: Re-enable MFA, rotate credentials, tighten firewall rules

**Communication** (parallel with recovery):

- **Internal**: Status updates every 4 hours; all-hands standup daily during incident
- **Customer notification**:
  - If data breach: Notify per regulatory timeline (GDPR 72h, some states 48h)
  - Message: What happened? What data was affected? What we're doing. What customers should do.
- **Law enforcement**: If ransomware or sophisticated attack, consider FBI/CISA notification
- **Auditors/Compliance**: Notify if required by contracts or regulations

**Example customer notification**:

> "We identified unauthorized access to our systems on [date]. Our investigation shows [X records] were accessed. We have no evidence of misuse. We have contained the access and restored systems. You should [monitor credit/change passwords]. We provide [X months free monitoring]. Contact [support email] for questions."

### 6. Post-Incident Review (Blameless)

Within 2 weeks of resolution:

- **Timeline**: Recreate incident timeline (when discovered, when escalated, when contained)
- **Root cause**: Why did this happen? Was it a missing control, process failure, or technical flaw?
- **Impact**: How many customers? How much data? Revenue impact? Reputation impact?
- **What went well**: What response activities worked? What team coordination was effective?
- **What didn't go well**: Where were delays? Confusion? Missing information?
- **Action items**: What will we change to prevent recurrence or reduce impact next time?
  - Technical fixes (patch vulnerability, add monitoring, implement control)
  - Process fixes (update runbook, add alert, improve documentation)
  - Training (brief team on new detection method)

**Important**: Blameless postmortem—focus on systems and processes, not individual failures. Goal is learning, not punishment.

### 7. Training & Tabletop Exercises

**Annual training**: All staff receives IR training (30-60 min)

- What triggers an incident
- Who to contact
- What not to do (don't delete logs, don't rush to shut down)

**Semi-annual tabletop**: Simulate incident scenario

- Scenario (e.g., "Ransomware detected on 5 servers at 10am Friday")
- Teams respond as if real (who escalates, what's the timeline, how do we communicate?)
- Debrief: What went well? What's our bottleneck?

## Output Format

An incident response plan (living document):

```
# Incident Response Plan

## Incident Classification & Escalation
[Table with severity levels, MTTD targets, escalation procedures]

## Incident Response Team
[Roles, responsibilities, on-call schedule, contact list]

## Detection & Alerting
[Alert standards, triage procedure, initial response]

## Containment Runbook
[Step-by-step procedures for: preserve evidence, isolate, investigate, decide recovery]

## Recovery Procedures
[System restore, patching, validation, hardening]

## Communication Template
[Internal status update, customer notification, law enforcement contact]

## Post-Incident Review Process
[Timeline recreation, root cause analysis, action items, blameless culture]

## Training Schedule
[Annual training, tabletop scenarios, refresher cadence]

## Appendix
- Escalation Contact List
- System criticality (which systems are critical?)
- Data classification (what's PII, what's financial?)
- Vendor/third-party incident contacts
```

## Worked Example

**Incident Response Plan: SaaS Analytics Platform**

### Critical Incident Scenario Response

**Scenario**: Ransomware detected on database server at 9:47am Friday. Attacker demands payment; some customer data encrypted.

**Response Timeline**:

- **9:47am**: Alert fires (file extension .locked detected on 500+ files in database directory)
- **9:52am**: SOC escalates to incident commander (Page Robert, VP Security)
- **10:00am**: War room established (Slack: #incident, Zoom bridge)
  - Robert (IC): Decide whether to shut down
  - Database team: Assess which databases encrypted; check backup integrity
  - Security team: Investigate how attacker got in; check for persistence
- **10:15am**: Decision: No evidence of data exfiltration yet; shutdown database to preserve evidence
- **10:30am**: Backup integrity confirmed; we can restore from 4 hours ago (12am backup)
- **10:45am**: Isolation: Database server disconnected from network; attacker can't move laterally
- **11:00am**: Executive briefing: Ransomware contained; no customer data lost (4-hour recovery point); database recovery in progress
- **11:30am**: Root cause analysis starts: SSH logs show attacker used compromised credentials (employee laptop with old password)
- **1:00pm**: Database restore begins; estimated 3-4 hours to completion
- **2:00pm**: Customer communication prepared (draft): "We detected and contained ransomware affecting our infrastructure. Our investigation shows no customer data was accessed or exfiltrated..."
- **5:00pm**: Database restore complete; testing shows no data corruption
- **6:00pm**: Customer notification sent; support team ready for calls
- **Monday**: Post-incident review; action items (mandatory password reset, MFA enforcement, improve database backup testing)

---

## Decision Framework

When responding to an incident:

- **If unsure about severity**: Err on the side of higher severity. It's easier to downgrade than deal with an undetected critical incident.
- **If deciding between containment speed and evidence preservation**: In general, preserve evidence if incident is contained. Forensics may be needed for legal/insurance.
- **If customer notification timing is unclear**: Consult your legal/compliance team immediately. Notification windows are strict (GDPR 72h).
- **If a system is compromised and you don't know why**: Don't assume it's patched; assume there's a persistence mechanism. Full rebuild is safer.
- **If incident commander is overwhelmed**: Assign a second commander or rotate; don't leave one person making all decisions under stress.

## Anti-Patterns & Guards

### Anti-Pattern 1: Untested Plan

**Description**: IR plan written once; never tested. When real incident happens, it fails.

**Guard**: Tabletop exercises at least semi-annually. Test the critical path (who escalates, how fast).

### Anti-Pattern 2: No Clear Incident Commander

**Description**: During incident, everyone has opinions; no one is making decisions.

**Guard**: Declare incident commander explicitly. They have final say (not consensus).

### Anti-Pattern 3: Destroying Evidence Too Fast

**Description**: Shutting down systems before forensics; losing ability to determine attack vector.

**Guard**: Preserve before recovery. Forensic imaging takes <1 hour; it's worth it.

### Anti-Pattern 4: Poor Communication

**Description**: Customers learn about breach from news; internal teams don't coordinate.

**Guard**: Prepare communication templates in advance. Designate communications officer.

### Anti-Pattern 5: Not Learning from Incidents

**Description**: Post-mortems written; recommendations ignored. Same incident repeats.

**Guard**: Assign action items; track through completion. Revisit in next tabletop.

## Quality Checklist

Before declaring IR program ready:

- [ ] **Incident classification is clear**: Team can quickly assess severity
- [ ] **Roles are defined**: Every IR function has an owner and backup
- [ ] **Detection is comprehensive**: Multiple alert sources; not just SIEM
- [ ] **Containment procedures are specific**: Step-by-step, not vague
- [ ] **Communication templates exist**: Prepared language for customers/executives
- [ ] **Team is trained**: Everyone knows their role; annual training scheduled
- [ ] **Plan is tested**: Tabletop exercises at least semi-annually
- [ ] **Post-mortems are blameless**: Focus on systems, not individuals
- [ ] **Regulations understood**: Know notification timelines and requirements

## Further Reading

- NIST SP 800-61 (Incident Handling Guide): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf
- SANS Incident Handler's Handbook: https://www.sans.org/incident-response/
- CISA Incident Response: https://www.cisa.gov/incident-response
- PagerDuty Incident Response: https://www.pagerduty.com/incident-response/
- Google Site Reliability Engineering (SRE): Chapter on incident response and blameless postmortems
