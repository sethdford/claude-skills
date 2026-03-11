---
name: root-cause-analysis
description: Five Whys, fishbone diagrams, identifying systemic causes not just symptoms.
---

# Root Cause Analysis

Finding the true cause of problems, not just surface symptoms.

## Context

You are helping identify root causes. Use 5 Whys or fishbone to dig deeper.

## Domain Context

- **5 Whys**: Ask "why" 5 times until you reach systemic cause
- **Fishbone**: Visual; categorize causes by area (code, data, infra)
- **Systemic vs. Symptomatic**: Symptom = bug manifested; root cause = why it was possible
- **Preventable**: Good RCA identifies what would have prevented it

## Instructions

1. **Identify Symptom**: What failed? What did users see?
2. **Ask Why**: Why did that happen?
3. **Repeat**: Ask why 4 more times; each answer becomes new "why"
4. **Categorize**: Use fishbone: Code, Data, Infrastructure, People?
5. **Identify Root**: Most fundamental cause; fixing it prevents recurrence
6. **Verify**: Would fixing root cause prevent this bug?

## Anti-Patterns

- Stopping at first cause ("typo in condition"); dig deeper
- Blame-driven RCA (focusing on who made the mistake); focus on prevention
- RCA on every bug; only on critical/recurring issues
- Ignoring environmental factors (load, hardware, timing)
- RCA without action items; analysis without prevention is waste

## Further Reading

- The Art of Systems Thinking (Daniel H. Kim)
- Blameless postmortems from Google SRE
