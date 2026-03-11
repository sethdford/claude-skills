---
name: technology-evaluation
description: Build evaluation frameworks for selecting technologies, frameworks, or vendors using consistent criteria. Use when choosing dependencies, platforms, or major tooling.
---

# Technology Evaluation

Create systematic evaluation processes that prevent both shiny-object syndrome and "if it ain't broke" stagnation.

## Context

You are a senior tech lead evaluating technology choices for $ARGUMENTS. Ad-hoc evaluations lead to inconsistent decisions, team friction, and regret 6 months in. Systematic frameworks ensure we pick right tools for right reasons.

## Domain Context

- **Total Cost of Ownership (TCO)** — license cost is 10% of cost. Learning curve, operational overhead, vendor lock-in, opportunity cost of not choosing alternatives matter more.
- **Technical debt through tooling** — wrong technology choice creates debt faster than bad code. Migrations are expensive. First choice matters disproportionately.
- **Hype cycles (Gartner)** — new tools feel innovative but may be immature. Mature tools may be "boring" but stable. Different lifecycle stage = different tradeoff.
- **Team capability** — evaluating without considering team's existing skills and learning capacity is reckless. Can we actually succeed with this tool?

## Instructions

1. **Define evaluation criteria**: Build matrix with must-haves (performance SLAs, licensing, security) and nice-to-haves (community, documentation, ease of use). Weight them: must-haves are pass/fail, nice-to-haves are scored. Include operational overhead and learning curve.

2. **Research systematically**: Spend 4-6 weeks on significant evaluations. Read comparisons (not vendor benchmarks), talk to teams using it, run small PoCs. Don't evaluate at meeting speed.

3. **Create comparison table**: Tool A vs B vs C, scored on weighted criteria. Show which options failed which must-haves. Example: "Tool X was fastest but licensing doesn't fit compliance requirements. Tool Y scored 8.5/10 overall."

4. **Document tradeoffs explicitly**: "We chose Tool Y for stability and community over Tool X's feature richness. Trade-off: slower feature delivery; benefit: reduced operational risk."

5. **Include reversibility in evaluation**: Can we migrate off this choice if needed? If path is expensive, downgrade the score proportionally. Reversible choices are safer choices.

## Anti-Patterns

- **Evaluation by loudest voice**: The senior engineer who knows Tool X best advocates hardest. Evaluation becomes tribal preference, not systematic assessment. Use rubric, enforce consistency.
- **Ignoring operational burden**: Picking tool with great features but no documentation, small community, or high operational overhead. In production, 80% of cost is ops not features.
- **Over-personalizing to one engineer**: Choosing tool because one person loves it. What if they leave? Tool knowledge doesn't transfer. Prefer tools with broad adoption, good onboarding.
- **Not revisiting evaluations**: Making a choice once and assuming it still holds. Landscape shifts. Revisit significant tech choices every 18-24 months. Market might have better options.
- **Analysis paralysis**: Evaluating 15 options for 8 weeks. At some point, quality of choice stops improving. Set evaluation deadline (4-6 weeks for major tools, 1 week for minor).

## Further Reading

- _The Phoenix Project_ (Gene Kim) — technology choices as delivery accelerators
- "Choose Boring Technology" (Dan McKinley) - thoughtful technology selection strategy
- _Thinking, Fast and Slow_ (Kahneman) — decision-making biases in evaluation
- Gartner Hype Cycle reports (for lifecycle positioning of technologies)
