# Incident to Improvement

Transforms an incident into systemic improvements: postmortem (engineer) → root cause (QA) → security review (security) → process improvement (tech lead) → backlog items (PM).

## Domain Context

An incident is a temporary failure. An improvement is a permanent change that makes that failure less likely or less severe in the future. The difference between teams that learn from incidents and teams that repeat them is whether they systematically convert incidents into improvements.

The incident-to-improvement cycle:

1. **Postmortem** (engineer) — What happened? Why? When did we first detect it?
2. **Root Cause** (QA + engineer) — What conditions allowed this to happen? What test would have caught it?
3. **Security Review** (security) — Were customer data, credentials, or systems compromised? How do we verify it's secure again?
4. **Process Improvement** (tech lead) — How do we prevent this class of bug in the future? (testing, monitoring, code organization)
5. **Backlog Items** (PM) — What work items should we add to the backlog to implement improvements?

**ISO/IEC 12207 Reference:**

- 5.3.10 Operation and Maintenance (problem resolution)
- 5.3.11 Disposal (lessons learned)

## Instructions

### Step 1: Postmortem (Engineer Perspective)

- **Input**: Incident description, timeline, customer impact
- **Ask**: What was the root cause? (obvious cause, not root cause yet)
- **Ask**: When did we first detect this? How long was the customer affected?
- **Ask**: What were the detection methods? (alert, customer report, automated monitoring)
- **Ask**: How was it resolved? (emergency code change, config change, feature flag, rollback)

Output: Postmortem narrative (what happened, when, how resolved)

### Step 2: Root Cause Analysis (QA + Engineer)

- **Ask**: What conditions had to be true for this bug to exist?
- **Ask**: What testing would have caught this? (unit test, integration test, load test, edge case test)
- **Ask**: Is this a class of bugs we've seen before? (similar patterns in incident history)
- **Ask**: What monitoring would have detected this faster?

Output: Root cause analysis (the actual causes, not just the symptom)

### Step 3: Security Review (Security Perspective)

- **Ask**: Were customer data, credentials, or systems compromised?
- **Ask**: Was the incident exploitable (could an attacker cause this intentionally)?
- **Ask**: What verification is needed to confirm data integrity? (audit logs, forensics)
- **Ask**: Should we notify customers or regulators? (based on data breach laws)

Output: Security impact assessment and remediation steps

### Step 4: Process Improvement (Tech Lead)

- **Ask**: How do we prevent this class of bug? (options: better testing, monitoring, code review, tooling, architecture)
- **Ask**: What's the most effective prevention? (based on cost, team skills, timeline)
- **Ask**: Should we add this to Definition of Done? (to prevent recurrence)
- **Ask**: Do we need monitoring or alerting changes?

Output: Process improvement recommendations with priority and effort

### Step 5: Backlog Items (PM)

- **Ask**: What work items need to be created to implement improvements?
- **Ask**: What's the priority? (critical: prevent recurrence, high: reduce risk, medium: improve visibility)
- **Ask**: When should we do this? (immediate, next sprint, planned)
- **Ask**: Who should own it? (engineer for code change, QA for test addition, tech lead for monitoring)

Output: Backlog items with owners, priority, effort estimates

### Step 6: Consolidate the Incident Report
```

Incident Report: [Incident ID / Name]
Date: [When it occurred]
Duration: [How long it lasted]
Customer Impact: [Who was affected, how, for how long]

Timeline:
[Time 1] - What happened / What was deployed / What config changed
[Time 2] - Alert fired / Customer reported / System degraded
[Time 3] - Investigation started
[Time 4] - Root cause identified
[Time 5] - Fix deployed / Rollback executed
[Time 6] - System stable

Postmortem (Engineer):
Detection method: [alert / customer report / monitoring]
Resolution: [code change / config change / rollback]
Steps taken to resolve: [list]

Root Cause Analysis (QA + Engineer):
Root causes: [list]
Testing gap: [What test would have caught this?]
Similar patterns: [Related incidents / bugs]
Monitoring gap: [What alert would have detected this faster?]

Security Review:
Data compromise: [Yes / No / Unknown] - Details if applicable
Exploitability: [Yes / No] - If an attacker could cause this
Verification needed: [Audit logs, forensics, customer notification]
Regulatory notification: [Required / Not required]

Process Improvements:
Improvements: [list]
Priority: [Critical / High / Medium]
Effort: [estimate in hours]
Owner: [engineer / QA / tech lead]

Backlog Items:
[ ] [Item 1] - [Description] - [Owner] - [Effort] - [Priority]
[ ] [Item 2] - [Description] - [Owner] - [Effort] - [Priority]
[ ] [Item 3] - [Description] - [Owner] - [Effort] - [Priority]

Sign-Off:
Engineer: ********\_******** Date: **\_\_\_**
QA: **********\_\_********** Date: **\_\_\_**
Security: ******\_\_\_\_****** Date: **\_\_\_**
Tech Lead: ******\_\_\_****** Date: **\_\_\_**
PM: **********\_********** Date: **\_\_\_**

```

## Anti-Patterns

1. **Postmortem without root cause**
   - Mistake: "There was a null pointer exception, we added a null check, done"
   - Correct: Why was a null allowed? Why didn't tests catch this? Why didn't monitoring alert?
   - Fix: Ask "why" at least 5 times; find the root cause, not the symptom

2. **Improvements that don't match the root cause**
   - Mistake: Root cause is "engineer didn't understand the API contract", improvement is "add more unit tests"
   - Correct: If the issue is understanding, the improvement is better documentation or pair programming
   - Fix: Match improvement to root cause; ensure the improvement actually prevents recurrence

3. **Not closing the loop**
   - Mistake: "We identified improvements, but never added them to the backlog or implemented them"
   - Correct: Improvements must be backlog items with owners and timelines
   - Fix: PM must prioritize improvements into the backlog; track implementation

4. **Skipping the security review**
   - Mistake: "This was a minor bug, not a security incident"
   - Correct: Even minor bugs can have security implications; always review
   - Fix: Security reviews every incident; signs off on security impact

5. **Treating incidents as individual events**
   - Mistake: "This incident is unique; it doesn't suggest broader problems"
   - Correct: Incidents are signals of systemic weaknesses; look for patterns
   - Fix: Retro question: "Is this a new class of bug? Have we seen similar patterns?"

6. **Not including QA in root cause analysis**
   - Mistake: "Engineer posts-mortem, then we move on"
   - Correct: QA should be part of root cause (testing gaps) and improvements
   - Fix: QA required for incident review; QA owns improvements to test strategy

## Further Reading

- **Postmortem Culture** — Edmondson, A. M., "The Fearless Organization: Creating Psychological Safety in the Workplace for Learning, Innovation, and Growth" (Wiley)
- **Root Cause Analysis** — Niklas, C. D., "Root Cause Analysis Handbook" (Reliability Center, Inc.)
- **Incident Response** — PagerDuty, "Incident Response for Everyone" (https://response.pagerduty.com/)