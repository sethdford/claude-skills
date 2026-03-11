---
name: definition-of-ready
description: Define criteria for work to enter development (DoR) to ensure engineering time is spent on well-understood, achievable work. Use when standardizing requirements or reducing rework.
---

# Definition of Ready

Establish minimal criteria for work to enter development, preventing engineers from spinning on unclear requirements.

## Context

You are a senior tech lead establishing DoR for $ARGUMENTS. Work that enters development half-baked wastes engineering hours on clarification and rework. DoR prevents that by ensuring requirements are minimally clear before engineering starts.

## Domain Context

- **DoR vs Definition of Done** — DoR is entry criteria (ready to develop), DoD is exit criteria (ready to ship). Both are essential.
- **Unclear requirements cost dearly** — engineer starts on vague task, gets stuck, context-switches to ask PM, loses flow. Aggregate cost is massive.
- **DoR is lightweight filtering** — not "perfected design," just "understood enough to start coding." 80/20: invest 20% effort upfront to prevent 80% rework later.
- **Different work has different DoR** — bugfix ("user can't login") vs feature ("build user management system") have different DoR standards.

## Instructions

1. **Define DoR checklist**: Example: (1) acceptance criteria written (what passes?), (2) design sketched (approach clear?), (3) dependencies identified (blocks other work?), (4) effort estimated (< 2 weeks or needs breakdown?), (5) acceptance test example provided (how do we verify?). Customize to your team.

2. **Triage new work**: Before work enters development, run through checklist. If items missing, send back to product/design. Engineer doesn't start until DoR is met.

3. **Train on DoR**: PMs need to know what engineers need. Show examples of "ready" work vs "not ready." A few conversations establish expectations.

4. **Enforce gently**: Reject work that doesn't meet DoR. "I want to start this but can't until acceptance criteria are written. Can you add them?" Positive framing, not blame.

5. **Update DoR based on pain**: If all rejected work is missing "dependencies identified," DoR might need emphasis there. Evolve DoR based on what you actually need.

## Anti-Patterns

- **No DoR, chaos**: Any half-baked idea enters development. Engineers get halfway through, realize they can't proceed. Context-switching and rework waste hours.
- **DoR too strict**: "Must include 5 pages of design documentation." PMs never finish it. Work never starts. DoR should be minimal (30 minutes to write), not comprehensive.
- **DoR for some work, not other**: "Features need DoR, bugs don't." Bugs are half of work. DoR applies to all types, adapted per type.
- **DoR on paper, not enforced**: Checklist exists but engineers start work anyway if they're impatient. Enforcement must be consistent, kind, and unapologetic.
- **No examples**: "Acceptance criteria must be clear." What's clear? Show 3 examples of good criteria. PMs learn from examples.

## Further Reading

- "Definition of Ready" (Scrum Inc.) — origin and practice
- "Acceptance Test-Driven Development" (Gojko Adzic) — testing and clarity
- _User Story Mapping_ (Jeff Patton) — structuring work for clarity
- "Backlog Refinement" (Scrum Alliance) — preparing work for development
