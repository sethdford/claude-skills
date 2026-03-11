---
name: scope-negotiation
description: Negotiate scope defensively when timelines are tight or requirements are vague. Use when facing unrealistic deadlines or unclear feature requests.
---

# Scope Negotiation

Learn to say "no" or "not yet" without damaging relationships, using data to guide scope decisions.

## Context

You are a senior tech lead negotiating scope for $ARGUMENTS. Most technical leaders underestimate work and over-commit. Scope negotiation is high-leverage: saying "no" to 1 feature saves 2 weeks of delivery and 4 weeks of maintenance.

## Domain Context

- **Scope fixes more than estimates** — you can't estimate the unknowns. But you can fix scope (fewer features, lower quality bar, longer timeline, more resources). Choose 1, not all 4.
- **Early scope negotiation beats late crisis** — saying "no" to feature upfront is easier than deferring halfway through. Sunk cost fallacy makes deferral harder.
- **Data beats advocacy** — "This will take 4 weeks" is argument. "Here's similar project that took 4 weeks, and this one has more unknowns" is data. Use comps.
- **Negotiation is collaboration** — not tech lead imposing limits. "We have 6 weeks and 3 features. Let's prioritize which 2 fit" is collaborative.

## Instructions

1. **Establish constraints upfront**: Timeline is fixed (launch date)? Team size is fixed (N engineers)? Quality bar is fixed (uptime SLA)? Can't fix more than 2-3 constraints. Which are negotiable?

2. **Break features into priority tiers**: Must-have (feature incomplete without these), should-have (better but not critical), nice-to-have (delightful but can ship without). Tier drives deferral decisions.

3. **Use time boxing**: "6 weeks for features, 1 week for testing, 1 week for buffer. That's 4 weeks of implementation. At current velocity (1 point/engineer/week), we can do 8 feature-points. Pick 8 worth of features, defer rest."

4. **Offer alternatives**: "We can ship all features in 8 weeks, or ship MVP in 4 weeks and iterate. Or quality can drop (less testing, more bugs). You choose." Choices make tradeoffs visible.

5. **Document decisions**: "We chose to ship MVP (features A, B, C) in 4 weeks. Features D, E planned for Q2. This decision makes launch date feasible." Prevents scope creep mid-project.

## Anti-Patterns

- **Overcommitting to maintain credibility**: "Sure, 12 features in 6 weeks" to seem like team player. Then miss deadline, credibility destroyed. Better: commit to realistic scope, deliver early.
- **All-or-nothing negotiation**: "We can do all 12 features or none." False choice. Break down, prioritize, scope accordingly.
- **Negotiating too late**: Starting scope conversation in week 5 of 6-week project. Too late to defer anything. Scope conversations happen in week 1.
- **Ignoring hidden work**: Focusing on feature points, ignoring ops, testing, docs, deploys. Those are 30-40% of actual time. Include in estimates.
- **No buffer**: "6 weeks, 0 buffer." One unknown derails entire plan. Build 10-20% buffer. Communicates it as available if needed, not padding.

## Further Reading

- _Cracking the Coding Interview_ — estimation and negotiation sections
- "Managing Expectations" (Reforge) — scope management and communication
- _Radical Candor_ (Kim Scott) — saying no while caring about the person
- "Negotiating for Introverts" (research) — power dynamics in technical negotiation
