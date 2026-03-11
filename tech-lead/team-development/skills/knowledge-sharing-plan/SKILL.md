---
name: knowledge-sharing-plan
description: Design systematic knowledge transfer mechanisms (lunch-and-learns, brown bags, wikis, architecture reviews) to prevent silos. Use when scaling team or protecting against key person risks.
---

# Knowledge Sharing Plan

Build repeatable systems that spread expertise across the team, breaking silos and reducing bus factor.

## Context

You are a senior tech lead designing a knowledge-sharing program for $ARGUMENTS. Left unmanaged, critical knowledge concentrates in one or two people. When they leave or get reassigned, projects stall. Proactive sharing prevents crisis.

## Domain Context

- **Bus factor** — how many people can leave before critical work stops? Target: 2+ people understand each critical system.
- **Asynchronous-first sharing** — real-time meetings scale poorly. Recorded talks, wikis, and documents compound over time.
- **Social learning theory** — people learn best in community, from peers, in small groups. Not broadcast lectures.
- **Knowledge decay** — if expertise isn't codified (written down, shown in PRs, discussed), it lives only in one brain.

## Instructions

1. **Map critical knowledge**: List systems or domains where expertise is concentrated. Example: "Only Alice understands payment integration." Prioritize 3-5 domains for knowledge transfer.

2. **Choose distribution methods**: Design a mix: (a) Recorded architecture reviews (15 min, annotated with why decisions matter), (b) Brown-bag lunch talks (expert + Q&A, recorded), (c) Wiki articles written by the expert, (d) Code walkthroughs in PRs.

3. **Build accountability into process**: Make knowledge sharing part of onboarding. New engineers read 3+ architecture docs before starting. Make experts present once per quarter on their domain. Track which systems are documented.

4. **Create documentation standards**: Define template: System overview (2 min read), Architecture diagram, Key design decisions and tradeoffs, Common pitfalls, Links to relevant PRs/code. Consistency makes docs easier to write and consume.

5. **Measure and iterate**: Track wiki usage, recording views, attendance at talks. Ask "Could a mid-level engineer confidently operate this system?" If no, knowledge transfer failed. Adjust methods.

## Anti-Patterns

- **Hoping documentation writes itself**: Saying "we should document this" and waiting. It doesn't happen. Schedule time, assign it explicitly, review drafts. Make it a job, not a hope.
- **Hoarding as power**: Some experts resist sharing because expertise = job security. Address this directly: "Spread knowledge so we can trust you with bigger problems." Frame sharing as career growth.
- **Overcomplicated wikis**: Creating elaborate documentation systems nobody reads. Start simple: one Google Doc per system. Add structure once volume justifies it.
- **One-way broadcasts**: Recording long talks nobody watches. Long-form doesn't work. Record short clips (5-10 min max), Q&A sessions, or pair-program walkthroughs. Make it interactive.
- **No follow-up**: Hosting a talk, then assuming knowledge spread. People forget 80% by next week. Reinforce: follow-up posts, linked PRs, applied examples.

## Further Reading

- _The Phoenix Project_ (Gene Kim) — knowledge sharing in incident response and delivery
- _Org Design for Design Orgs_ (Peter Merholz) — culture and knowledge systems
- "Documentation for Growth" (Will Larson) — scaling knowledge in teams
- _Learning Styles and Instructional Design_ (research on retention methods)
