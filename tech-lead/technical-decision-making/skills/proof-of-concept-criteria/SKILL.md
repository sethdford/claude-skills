---
name: proof-of-concept-criteria
description: Define when and how to validate ideas through PoCs before full implementation. Use to decide between spikes, PoCs, and production rollouts.
---

# Proof of Concept Criteria

Distinguish when you need a spike (research), PoC (validation), or pilot (real-world test) versus going straight to production.

## Context

You are a senior tech lead deciding proof-of-concept scope for $ARGUMENTS. Poor PoC criteria lead to either wasted months on unnecessary validation or shipping risky code straight to production.

## Domain Context

- **PoC answers "does it work in our environment?"** not "can it theoretically work?" Spikes answer "can we do it?", PoCs answer "will it work for us?"
- **Production complexity compounds** — assumptions that worked in PoC may fail under scale, real-world data, or fault conditions. PoCs reduce but don't eliminate risk.
- **Business PoCs vs technical PoCs** — business PoC proves user value (build minimal feature, test with customers). Technical PoC proves implementation feasibility (simplified version in real system).
- **PoC != MVP** — PoC has minimal rigor, MVP ships to users. Don't confuse them.

## Instructions

1. **Define PoC trigger criteria**: Spike found approach viable but major unknowns remain. Examples: "Will this perform under 100K users?" "Does real data cause issues spike didn't surface?" "Can operations staff handle new tooling?" If spike answered the question sufficiently, skip PoC, start implementation.

2. **Scope PoC narrowly**: Test specific uncertainty in most realistic environment possible. Example: "Deploy new database with real data, run actual queries, measure latency + ops burden" not "build entire new system." PoC is minimal production slice.

3. **Define success criteria upfront**: "Response time under 100ms, 99%ile latency under 500ms. Operations team can monitor and respond to alerts within SLA." Specific, measurable. If PoC doesn't hit criteria, don't ship.

4. **Timeline and effort**: PoCs typically 2-6 weeks with 2-3 people. If PoC is month-long, you've started implementation, not validation. Keep PoC tight.

5. **Go/no-go decision process**: At PoC end, explicitly decide: ship to production, iterate PoC, go back to spike, or kill the idea. Document decision and rationale. "PoC succeeded technically but cost is higher than estimated. Revisit in 18 months when scale justifies it."

## Anti-Patterns

- **PoCs that turn into products**: Building PoC without rigor, then shipping it to production. PoC quality expectations are wrong. Rewrite after PoC concludes if you ship.
- **Over-validating**: Running PoCs for obvious choices. If spike answered the question, ship. Validation-by-committee kills velocity. Know when "good enough" is good enough.
- **Business PoCs with no technical validation**: Building feature for users without knowing if tech foundation works. Customer feedback doesn't matter if system crashes. Do technical validation first.
- **Misleading PoCs**: Testing with synthetic data, ideal conditions. Real data exposes edge cases. Test with production-like data even in PoC.
- **No clear endpoint**: PoC runs indefinitely. Team keeps adding "just one more test." Set calendar date. When date arrives, decide, don't extend.

## Further Reading

- "Proof of Concepts" (Gartner) — PoC maturity models and frameworks
- _Validated Learning_ (Ries, Lean Startup) — validation before shipping
- "Death by a Thousand PoCs" (Martin Fowler) — when PoCs become wasteful
- _Rapid Development_ (McConnell) — proof-of-concept planning and decision gates
