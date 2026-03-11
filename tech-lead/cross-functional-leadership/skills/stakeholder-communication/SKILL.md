---
name: stakeholder-communication
description: Communicate technical progress, tradeoffs, and risks to non-engineers in language they understand. Use in status updates, executive presentations, or crisis communication.
---

# Stakeholder Communication

Translate technical concepts for non-engineers without losing accuracy or oversimplifying into uselessness.

## Context

You are a senior tech lead communicating with stakeholders for $ARGUMENTS. Poor technical communication leads to misalignment (stakeholder thinks X is ready when engineer knows it's not) or lost credibility (stakeholder feels patronized).

## Domain Context

- **Audience translation** — VP cares about: on-time delivery, risk, user impact. Not syntax details. Manager cares about: team morale, bottlenecks, progress. Not architecture minutiae.
- **Specificity vs clarity tradeoff** — "We refactored the ORM" is vague. "We switched database systems, improving query latency 60% but requiring 3 weeks to migrate" is specific and meaningful.
- **Jargon is a barrier** — using technical terms assumes audience understands. Either define terms or avoid them. Test comprehension.
- **Confidence calibration** — stakeholders need to know "we're 80% confident of timeline" vs "we hope to make timeline." Confidence affects their planning.

## Instructions

1. **Know your audience**: What do they care about? Revenue impact? Timeline? Risk? Team satisfaction? Tailor message accordingly. VP gets risk/timeline, engineer gets detail.

2. **Translate, don't dumb down**: "We optimized database queries" vs "We're speeding up the checkout flow." Same idea, different emphasis. Technical accurate, stakeholder-relevant.

3. **Use comparisons**: "Current system handles 1000 users/day. Proposed system handles 100,000 users/day" is concrete. "We're scaling the system" is vague.

4. **Quantify tradeoffs**: "Shipping now: launch on time, but 30% of features deferred. Shipping with all features: 2-month delay." Stakeholder chooses from clear options.

5. **Calibrate confidence**: "We're 95% confident we ship on time" or "There's 50/50 risk of 2-week delay due to unknowns. Here's the risk mitigation." Confidence allows planning.

## Anti-Patterns

- **Jargon without explanation**: "We have a P1 in the CI/CD pipeline. Needs refactoring of the ORM." Stakeholder doesn't know what P1 is or why it matters. Explain briefly.
- **False specificity**: "We'll ship in 3.7 weeks." Implies precision you don't have. Better: "Estimated 3-4 weeks, could be 2-3 if we cut scope, or 5-6 if unknowns surface."
- **Oversimplification**: "Everything is fine" when actually there are risks. Stakeholder makes bad decisions based on false confidence. Be honest about uncertainty.
- **No translation of bad news**: "We hit a blocker" is passive. "The data migration will take 2 weeks longer than expected, pushing launch to March 15. Here's how we're mitigating risk." Provides context and agency.
- **One-size-fits-all updates**: Same status to CEO and to engineering team doesn't work. Tailor depth and emphasis per audience.

## Further Reading

- "Executive Communication" (HBR) — communicating with C-level
- _Made to Stick_ (Chip Heath) — making ideas memorable and clear
- "Storytelling with Data" (Cole Nussbaumer) — visual communication of data
- "Crucial Conversations" (Patterson et al.) — difficult conversations with stakeholders
