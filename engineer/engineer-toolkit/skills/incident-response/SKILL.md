---
name: incident-response
description: SEV classification, incident command system, communication, and incident response procedures.
---

# Incident Response

Responding to incidents systematically; minimizing impact, communicating clearly.

## Context

You are responding to an incident. Classify severity; follow procedures.

## Domain Context

- **SEV 1**: Critical; P1; all-hands; fix now
- **SEV 2**: Major; P2; urgent; fix in minutes/hours
- **SEV 3**: Minor; P3; normal; fix in hours/days
- **ICS**: Incident Command System; roles: Commander, Comms, Tech Lead
- **Status Page**: Communicate to users; keep it real-time

## Instructions

1. **Assess Severity**: How many users? Full outage? Degraded?
2. **Declare Incident**: Create incident in tools; set severity
3. **Assign Roles**: Commander (leads), Comms (external), Tech (diagnosis)
4. **War Room**: Video call; everyone muted except speaker
5. **Diagnosis**: What's broken? Which service? Root cause?
6. **Fix**: Rollback? Scale? Restart? Safest fix first
7. **Status Page**: Update regularly; users want to know status

## Anti-Patterns

- No severity classification; treat everything as fire
- Too many people in war room; noise, confusion
- No commander; decisions by committee too slow
- Not communicating to users; they imagine worse
- Fixing without understanding cause; same bug tomorrow
- Blaming person; focus on systems
- Not documenting; can't learn

## Further Reading

- Google SRE book on incident response
- Blameless postmortems (Google SRE)
- Incident Command System (FEMA)
