---
name: cross-team-coordination
description: Coordinate work across multiple teams to prevent conflicts, reduce duplication, and align on shared systems. Use when scaling beyond single team or managing dependencies.
---

# Cross-Team Coordination

Build coordination mechanisms that prevent teams from working at cross-purposes or duplicating effort.

## Context

You are a senior tech lead coordinating across teams for $ARGUMENTS. Without coordination, teams step on each other (two teams refactoring same system), duplicate work, or create integration nightmares.

## Domain Context

- **Communication cost grows with team count** — 3 teams communicating = 3 channels. 4 teams = 6 channels. Coordination overhead explodes. Need structured communication, not ad-hoc.
- **Duplication is expensive** — two teams building similar features, both suboptimal. Sharing work is faster but requires coordination.
- **Dependency awareness prevents surprises** — team A needs team B's API by Q2. Without visibility, Q3 discovers API wasn't built. Early dependency mapping prevents this.
- **Async coordination scales** — sync meetings with N teams don't work. Document decisions, use async feedback, coordinate via artifacts (shared documentation, roadmaps).

## Instructions

1. **Create shared roadmap**: High-level 6-month roadmap visible to all teams. Shows what each team is doing and where dependencies exist. Updated quarterly.

2. **Dependency mapping meetings** (quarterly): Each team describes work planned. Others flag dependencies or conflicts. "Team A needs Team B's API" gets documented. Explicit, not surprised.

3. **Shared architecture documents**: If multiple teams touch same system, document it. One source of truth. Each team can see what's already built, avoid duplication.

4. **Weekly async status**: Each team posts progress (3-5 bullets) in shared doc. No meeting. Other teams read and comment. Visibility without meeting overhead.

5. **Escalation path**: When teams conflict ("Team A wants to refactor DB, Team B shipping feature needing old schema"), escalate to shared lead for decision. Document decision so both teams understand.

## Anti-Patterns

- **No cross-team visibility**: Teams working in silos, discover conflicts when integrating. Wasteful rework.
- **Coordination by meeting**: Quarterly meetings don't work. Needs 2-week cadence minimum to catch emerging issues. But too frequent wastes time. Weekly async + escalation meetings on-demand works well.
- **No shared roadmaps**: Each team has roadmap, nobody sees the aggregate. Reveals duplication only in hindsight.
- **Async-only communication**: Some decisions need sync discussion (major conflicts, complex tradeoffs). Pure async = prolonged negotiation. Have sync meetings for high-stakes decisions, async for status.
- **No clear escalation path**: Conflict between teams, they argue and escalate upward in chaos. Clear escalation path (both report to X, X decides) prevents escalation spirals.

## Further Reading

- _The Phoenix Project_ (Gene Kim) — cross-team dependencies and delivery
- "Spotify Model" (Henrik Kniberg) — scaling engineering teams with tribes/chapters
- _Accelerate_ (Dora metrics) — organizational structure and delivery
- "Conway's Law" — system design reflects organization structure; design org accordingly
