---
name: impact-effort-matrix
description: Visualize features by impact and effort to prioritize quick wins and strategic bets.
---

# Impact-Effort Matrix

Use a 2x2 matrix to categorize work and identify quick wins and strategic bets.

## Context

You are prioritizing a diverse backlog. The matrix helps visualize trade-offs between impact and effort. Your goal is clear categorization that guides planning.

## Domain Context

- **Quick wins**: High impact, low effort → do first
- **Strategic bets**: High impact, high effort → plan carefully
- **Fill-ins**: Low impact, low effort → do if time
- **Avoid**: Low impact, high effort → challenge or kill

## Instructions

1. **List all opportunities**
2. **Estimate Impact**: Business value if completed (1-5 scale)
3. **Estimate Effort**: Resources/time required (1-5 scale)
4. **Plot on 2x2**: Position based on estimates
5. **Categorize**: Quick wins, bets, fill-ins, avoid
6. **Plan sequencing**: Quick wins first, then bets, then fill-ins

## Output Artifact

Impact-Effort Matrix (visual):
- 2x2 grid with opportunities plotted
- Quick wins highlighted (top-left)
- Strategic bets identified (top-right)
- Avoids called out (bottom-right)

## Anti-Patterns

- **Misestimating impact**: Assuming feature request = high impact
- **Not considering interdependencies**: Work in random order instead of sequence
- **Static matrix**: Not updating as you learn
- **Too many items**: Can't see signal; use RICE to pre-filter

## Further Reading

- *Inspired* (Marty Cagan) — prioritization
- *The Lean Product Playbook* (Dan Olsen) — trade-off analysis
