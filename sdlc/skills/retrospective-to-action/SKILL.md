# Retrospective to Action

Runs a structured retro that produces actionable items assigned to specific roles.

## Domain Context

Retrospectives are where teams reflect on how they work and commit to changes. But many retros become venting sessions with no follow-up. The difference is structure: **retrospective-to-action** ensures that:

1. Observations are categorized (what went well, what didn't, what confused us)
2. Root causes are identified
3. Improvements are concrete and assigned
4. Improvements are prioritized and tracked

**ISO/IEC 12207 Reference:**

- 5.3.11 Disposal (lessons learned, process improvements)

## Instructions

### Step 1: Frame the Retro

- **Input**: Sprint context (dates, team size, key events)
- **Ask**: What were the sprint goals?
- **Ask**: Did we hit them? (yes/partial/no)
- **Ask**: What external events impacted the sprint? (incidents, stakeholder changes, dependency delays)

Output: Retro framing

### Step 2: Observations (What Happened)

Ask the team to capture observations in three categories:

**What Went Well?**

- Examples: "Code review process was smooth", "Feature shipped on time", "Team collaboration was great"
- Ask the team: What should we keep doing?

**What Didn't Go Well?**

- Examples: "Testing took longer than expected", "Communication with PM was unclear", "We shipped a bug to production"
- Ask the team: What should we change?

**What Confused Us?**

- Examples: "Requirements changed mid-sprint", "We weren't sure about the design until mid-development", "Monitoring didn't catch the issue"
- Ask the team: What would make this clearer next time?

Output: Observation lists from all team members

### Step 3: Root Cause Analysis

For each "didn't go well" observation:

- **Ask**: Why did this happen? (ask at least once)
- **Ask**: What could we have done differently?
- **Ask**: Is this a systemic issue or a one-time event?

Output: Root causes and potential improvements

### Step 4: Improvement Ideas

For each root cause:

- **Ask**: What's an improvement that would prevent this next sprint?
- **Ask**: Who would own this? (engineer, QA, PM, tech lead, designer)
- **Ask**: How much effort? (quick win, sprint work, epic work)

Output: Improvement ideas with owners and effort estimates

### Step 5: Prioritize Improvements

- **Quick wins** (< 1 hour) — Do this immediately
- **Sprint work** (1-5 days) — Add to next sprint backlog
- **Epic work** (> 5 days) — Plan for future sprint

- **High impact** — Affects multiple people, prevents recurrence of major issue
- **Medium impact** — Affects some people, improves efficiency
- **Low impact** — Nice to have, low urgency

Output: Prioritized improvement list

### Step 6: Assign Owners

For each improvement:

- **Ask**: Who should own this?
- **Ask**: Can they commit to doing it?

Output: Assignments

### Step 7: Consolidate Retro Notes
```

Retrospective: Sprint [N]
Date: [Date]
Team: [Members]

Sprint Goals: [Goals]
Goal Achievement: [Yes / Partial / No]
Key Events: [Incidents, blockers, changes]

What Went Well:
• [Observation] - Team sentiment: [positive]
• [Observation] - Team sentiment: [positive]
• [Observation] - Team sentiment: [positive]

What Didn't Go Well:
• [Observation] - Root cause: [cause] - Improvement: [idea]
• [Observation] - Root cause: [cause] - Improvement: [idea]
• [Observation] - Root cause: [cause] - Improvement: [idea]

What Confused Us:
• [Observation] - Clarity improvement: [idea]
• [Observation] - Clarity improvement: [idea]

Improvements (Prioritized):
Quick Wins (< 1 hour):
[ ] [Improvement] - Owner: [name] - Effort: [estimate]
[ ] [Improvement] - Owner: [name] - Effort: [estimate]

Sprint Work (1-5 days):
[ ] [Improvement] - Owner: [name] - Effort: [estimate]
[ ] [Improvement] - Owner: [name] - Effort: [estimate]

Epic Work (> 5 days):
[ ] [Improvement] - Owner: [name] - Effort: [estimate]

Backlog Items Created:
[ ] [Issue ID] - [Title] - [Owner] - [Sprint]
[ ] [Issue ID] - [Title] - [Owner] - [Sprint]
[ ] [Issue ID] - [Title] - [Owner] - [Sprint]

Follow-Up:
Next retro date: [Date]
Review improvement status: [Yes / No]

```

### Step 8: Close the Loop

- **Immediately** — Assign quick wins; expect completion in next 1-2 days
- **Next Sprint** — Prioritize sprint work improvements into backlog
- **Future** — Track epic work improvements; plan for dedicated sprint

## Anti-Patterns

1. **Retros without follow-up**
   - Mistake: "We did retro, identified improvements, but never tracked them"
   - Correct: Every improvement becomes a backlog item with an owner
   - Fix: PM is responsible for creating and tracking improvement backlog items

2. **Retros that blame individuals**
   - Mistake: "Engineer shipped a bug, so they should write better code"
   - Correct: Bugs are systemic failures (inadequate testing, unclear requirements, design issues)
   - Fix: Focus on systemic improvements, not individual blame

3. **Treating all observations as equally important**
   - Mistake: "All 15 observations get equal discussion time"
   - Correct: Prioritize by impact and effort
   - Fix: Time-box the retro (60 min for week sprint); prioritize top 5 improvements

4. **Improvements with no owners**
   - Mistake: "We should improve testing" (but no one owns it)
   - Correct: Every improvement has a specific owner who commits to it
   - Fix: In retro, ask: "Who owns this? Can you commit to next sprint?"

5. **Not reviewing improvement status in the next retro**
   - Mistake: "We created improvement items, but never checked if they happened"
   - Correct: Start next retro by reviewing previous sprint's improvements
   - Fix: Retro agenda always includes: "Review last sprint's improvement items"

6. **Retros that don't inform process changes**
   - Mistake: "We retro, but DoR/DoD never change based on learnings"
   - Correct: Retros should evolve team practices
   - Fix: Question: "Should this observation change our DoR or DoD?"

## Further Reading

- **Agile Retrospectives** — Derby, E. & Larsen, D., "Agile Retrospectives: Making Good Teams Great" (Pragmatic Bookshelf)
- **Blameless Postmortems** — Edmonson, A., "The Fearless Organization" (Wiley)
- **Continuous Improvement** — Liker, J., "The Toyota Way" (McGraw-Hill)