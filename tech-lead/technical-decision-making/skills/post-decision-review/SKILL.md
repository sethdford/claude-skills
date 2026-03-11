---
name: post-decision-review
description: Conduct retrospective reviews of major decisions 3-6 months after implementation to capture learnings and calibrate future decisions. Use to build institutional memory and improve decision quality.
---

# Post-Decision Review

Systematically review decisions after they've played out in reality, capturing what you got right, what surprised you, and how to improve future decisions.

## Context

You are a senior tech lead reviewing a major decision for $ARGUMENTS. Post-mortems are common for incidents; post-decision reviews for normal decisions are rare. Yet they're where organizations learn most about decision-making quality.

## Domain Context

- **Hindsight bias** — decisions look obvious in retrospect. Review 6 months out helps distinguish "obvious in hindsight" from "genuinely good decision-making."
- **Feedback loops accelerate learning** — no feedback loop, same decision mistakes repeat. Regular reviews build institutional memory faster than theory.
- **Implicit assumptions surface only in retrospect** — "we assumed X would happen" often becomes clear when it didn't. Documenting assumptions and reviewing them prevents recurrence.
- **External factors matter** — sometimes good decisions have bad outcomes because unexpected market shifts or technical issues arose. Document those. They inform risk planning next time.

## Instructions

1. **Schedule review 3-6 months after decision goes live**: Timing matters. Too soon (1 month) and full impact isn't clear. Too late (12+ months) and memory fades. 3-6 months is sweet spot.

2. **Compare outcome to prediction**: Pull original decision document. Compare predicted outcomes to actual outcomes. Were predictions accurate? Where did we miss? Document deltas. Example: "We predicted 15% performance improvement; actual was 22%. We were conservative on CPU optimization but underestimated cache benefits."

3. **Assess decision quality, not outcome luck**: Good decision, unlucky outcome (like weather-dependent forecast) is still good decision-making. Bad decision, lucky outcome (market shift bailed us out) is still poor process. Separate decision quality from outcome.

4. **Identify surprises and new learnings**: What surprised you? "We expected adoption to be slow but teams adopted the feature immediately." "We thought ops complexity would be high; turned out to be manageable." Document these. They're calibration data for future estimates.

5. **Extract decision rules for next time**: "When evaluating similar decisions, assume team adoption is faster than we estimate" or "Performance improvements are often higher than benchmarks predict because cache effects compound." Codify learnings into heuristics.

## Anti-Patterns

- **Blame reviews disguised as learning**: Using review to assign fault ("Alice chose wrong technology, she's bad at decisions"). Kills future honesty. Reviews are learning exercises, not performance evaluations.
- **Ignoring sunk cost**: Dwelling on resources spent. "We spent 6 weeks on this" is sunk. Focus on what you learned and whether to continue or change course.
- **Not updating decision criteria**: Learning "we were bad at estimating ops complexity" without changing how you estimate ops complexity in future decisions. Reviews are pointless without behavior change.
- **Only reviewing failures**: Reviewing mistakes is important, but reviewing successful decisions is equally valuable. Why did a decision succeed? What would have broken it?
- **No record keeping**: Running review, discussing learnings, forgetting by next quarter. Document findings in decision record. Update original RFC or decision doc with "6-month review: X, Y, Z."

## Further Reading

- _Thinking, Fast and Slow_ (Kahneman) — decision-making bias and calibration
- _Superforecasting_ (Tetlock) — how to improve prediction accuracy through review
- "Blameless Postmortems" (Etsy/John Allspaw) — conducting reviews without blame
- _The Righteous Mind_ (Haidt) — tribal bias in decision reviews; how to mitigate
