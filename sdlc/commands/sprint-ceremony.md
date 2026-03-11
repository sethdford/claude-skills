---
description: Conduct a complete sprint cycle with planning, DoR validation, retrospective, and action items.
argument-hint: "[sprint number or date range]"
---

Facilitate a comprehensive sprint cycle: planning, DoR validation, retrospective, action items.

## Steps

1. **Tech Lead Sprint Planning** (`tech-lead:sprint-planning-guide`)
   - Input: Backlog, team capacity, dependencies
   - Output: Sprint goal, sprint backlog, team commitments

2. **Definition of Ready Validation** (`sdlc:definition-of-ready`)
   - Input: Sprint backlog items
   - Output: DoR checklist for each item; identify items not ready

3. **Retrospective to Action** (`sdlc:retrospective-to-action`)
   - Input: Previous sprint observations, metrics
   - Output: Improvements and action items

4. **PM Backlog Prioritization** (`product-manager:prioritize-backlog`)
   - Input: Backlog, improvements from retro
   - Output: Next sprint priorities

## Output

**Sprint Ceremony Summary** containing:

- Sprint goal and planned items
- DoR validation (items ready / not ready)
- Retrospective observations (what went well, what didn't)
- Action items with owners and timelines
- Priorities for next sprint
- Team commitments and capacity

## Example
```

/sdlc:sprint-ceremony "Sprint 42 (Mar 11 - Mar 22)"

→ Planning: 8 items planned, 75 story points, 3 team members
→ DoR Validation: 7/8 items ready; 1 item needs design review (defer to Sprint 43)
→ Retrospective: Positive: "Code reviews fast", Negative: "Design phase bottleneck"
→ Actions: "Add designer to code review" (tech lead, low effort)
→ Priorities: "Design is now critical path; add designer capacity"

Output: Sprint Ceremony Summary
Sprint Goal: "Complete authentication redesign"
Sprint Backlog: [7 items, 71 story points]
DoR Status: 7/8 items ready
Retrospective Actions: [list with owners]
Next Sprint Priorities: [list]
Team Confidence: HIGH

```

## Next Steps

- "Sprint starts tomorrow at 9:00am."
- "Defer 1 not-ready item; prioritize for Sprint 43."
- "Implement retrospective action: add designer to code review."