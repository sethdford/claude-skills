---
name: documentation-standards
description: Establish documentation standards that keep docs current, discoverable, and useful. Use when scaling team or improving knowledge retention.
---

# Documentation Standards

Build documentation discipline that prevents doc rot and makes knowledge discoverable.

## Context

You are a senior tech lead establishing documentation standards for $ARGUMENTS. Documentation is like tests: valuable only if maintained. Outdated docs are worse than no docs (they mislead).

## Domain Context

- **Docs are expensive to write but multiply value** — writing doc takes 2 hours upfront, saves 20 minutes × N people who learn from it. At 10+ readers, ROI is positive.
- **Single source of truth prevents divergence** — when docs are scattered (wiki, README, Slack, email), people find conflicting info. Centralize.
- **Docs decay over time** — 6 months old, half of it is stale. Reviews are essential. Every doc needs "last reviewed" date and owner.
- **Examples > specifications** — "Authenticate via OAuth2" is spec. "Here's how OAuth2 works in our system, with code example" is useful. Examples stick in memory.

## Instructions

1. **Establish documentation zones**: README (project setup, quick start), API docs (endpoint reference), Guides (how-to articles), Architecture (design decisions, tradeoffs). Clarity about where information lives prevents duplication.

2. **Create doc template**: System overview (what is it?), Architecture diagram, How to use (quick start), Common patterns (examples), Troubleshooting (FAQ), Links. Template prevents blank-page freeze and ensures consistency.

3. **Assign owners**: Every doc has owner responsible for accuracy. Owner reviews quarterly: "Is this still accurate?" and updates "last reviewed" date. Ownership = accountability.

4. **Link from code**: Add doc links in code comments and README. "See architecture.md for design rationale." Links docs to living code.

5. **Track doc usage**: If available, monitor wiki usage or GitHub docs views. If nobody reads a doc, either it's bad or unnecessary. Investigate.

## Anti-Patterns

- **Doc rot**: Docs written once, never updated. 6 months later, half of it is wrong. Discredits all docs. Establish review cadence.
- **Docs exist but scattered**: Some in README, some in wiki, some in code comments. Discoverable? No. Centralize or at least have master index.
- **No examples**: "Here's what this system does" without "here's code showing how to use it." Useless. Examples are documentation's friend.
- **Over-documentation**: 100-page design doc for simple system. Nobody reads it. Sweet spot: 2-5 page doc per topic. Brevity improves readout.
- **No enforcement**: "We should document this" but no requirement. Docs aren't written. Make documentation part of DoD (Definition of Done): feature isn't done until documented.

## Further Reading

- "Docs as Code" (Anne Gentle) — treating documentation like code
- "Write the Docs" (community) — principles and practices
- _Docs That Work_ (Palimpsest) — documentation systems
- "Organizational Memory" (research) — documentation's role in knowledge retention
