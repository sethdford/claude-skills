---
name: red-team-exercise
description: Plan and execute red team exercises to test security controls and incident response capabilities.
---

# Red Team Exercise

Plan and execute red team exercises to test security controls.

## Context

You are a senior security leader planning red team exercises for $ARGUMENTS. Red teams simulate real attacks; they test controls, find gaps, and validate incident response. Unlike pen tests (checking for specific vulnerabilities), red teams emulate how real attackers operate: persistence, lateral movement, stealth. Red team exercises are the ultimate security test.

## Domain Context

- **Red vs. Pen Test**: Pen test finds vulnerabilities; red team simulates APT behavior (multiple attack chains, persistence, evasion)
- **Blue Team**: Your team defending; red team attacks
- **Scope**: Entire infrastructure, or specific systems/scenarios
- **Duration**: Days to weeks (emulates real intrusion duration)
- **Objectives**: Find control gaps, test incident response, identify architectural flaws

## Instructions

1. **Plan Red Team Exercise**:
   - **Scope**: What systems in scope? Production (risky) or staging (safer)?
     - Start with staging/development for first exercises
     - Advance to limited production (non-critical systems) after proving safety
   - **Objectives**:
     - "Can red team reach customer database undetected?"
     - "How long before we detect lateral movement?"
     - "Can we eject red team within 4 hours?"
   - **Rules of Engagement**:
     - What's allowed? Denial of service? Data exfiltration? Social engineering?
     - Who is in the loop? (Executive sponsor must approve; too many people = exercise discovered)
     - Escalation: If red team finds critical vulnerability, escalate immediately
   - **Timeline**: When will exercise run? Minimize business impact
   - **Inject Points**: Key decision points (when do defenders need to escalate, make difficult calls?)

2. **Red Team Preparation**:
   - **Intelligence Gathering**: Red team researches organization
     - Public information (website, LinkedIn, DNS records)
     - Vulnerability research (CVEs relevant to your tech stack)
     - Industry-standard attacks (supply chain, phishing, misconfigurations)
   - **Attack Planning**: Develop attack plan
     - Initial access (phishing, vulnerable web app, supply chain)
     - Persistence (backdoor, scheduled task, new account)
     - Lateral movement (credential theft, hop from web server to database server)
     - Objectives (exfiltrate data, disrupt service, etc.)
   - **Tools Preparation**: Set up tools (Cobalt Strike, Mimikatz, post-exploitation tools)
     - All in staging; nothing against production until exercise starts

3. **Execute Exercise**:
   - **Start**: Red team begins attack (initial access)
   - **Monitoring**: Blue team monitors SIEM, alerts, incidents
     - Don't tell blue team exercise is running (tests detection)
     - Or tell them (tests response speed)—depends on exercise objective
   - **Escalation**: As red team progresses, escalate to management
     - When detected, incident commander activates response
   - **Objectives Achievement**: Red team attempts to achieve objectives
     - If objective is "exfiltrate data", red team tries to move data off network
     - If objective is "gain persistence", red team establishes backdoor
   - **Evaluation Points**:
     - MTTD: How long to detect red team?
     - MTTR: How long to respond?
     - Control effectiveness: Which controls worked? Which failed?
     - Incident response: Did team follow procedures? Communicate effectively?

4. **Monitoring & Observation**:
   - **Feedback Loop**: Observers (security team, not involved in response) watch and document
     - What happened? Timeline of events
     - How did team respond? Decisions made
     - What worked? What didn't?
   - **Deconflict**: If real incident occurs during exercise, exercise pauses (security first)
   - **Documentation**: Record everything for post-exercise review

5. **Post-Exercise Review (Hot-Wash)**:
   - **Timeline Review**: Walk through what happened chronologically
   - **What Went Well**: Recognize effective responses, good decisions
   - **What Didn't Work**: Identify gaps, process failures, control deficiencies
   - **Gaps Identified**:
     - Detection gap: Attack undetected for X hours
     - Response gap: Team didn't know what to do when incident detected
     - Technical gap: Control failed (firewall rule misconfigured)
   - **Action Items**: Prioritize improvements; assign owners; set deadlines

6. **Implementation & Metrics**:
   - **Action Items Tracking**: Ensure recommendations are implemented
     - Timeline: Critical within 30 days, High within 90 days
   - **Validation**: Post-implementation exercise validates improvements
     - Re-run same attack scenario; verify it's now detected/prevented
   - **Metrics**:
     - MTTD improvement (exercise 1: detected in 6 hours → exercise 2: detected in 1 hour?)
     - Incident response speed (exercise 1: 2 hours to contain → exercise 2: 30 minutes?)
     - Control effectiveness (exercise 1: red team accessed database → exercise 2: stopped by network policy?)

## Anti-Patterns

- No scope/rules (red team tests production; causes outage); **clear scope and approval required**
- No communication to leadership (exercise discovered by surprised executives); **executive sponsor informed**
- Too many people know (exercise is "leaked"; team prepares instead of responding naturally); **"need-to-know only"**
- No post-exercise review (lessons not captured); **comprehensive debrief is most valuable part**
- No follow-up on action items (exercise findings ignored); **track improvements; validate in next exercise**

## Further Reading

- NIST SP 800-115 (Red Team Testing): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf
- Cobalt Strike (Red Team Tool): https://www.cobaltstrike.com/
- MITRE ATT&CK (Red Team Framework): https://attack.mitre.org/
- Red Team Best Practices: SANS, Mandiant, Verizon reports
