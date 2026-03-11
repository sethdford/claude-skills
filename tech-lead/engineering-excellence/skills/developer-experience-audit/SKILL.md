---
name: developer-experience-audit
description: Systematically assess and improve developer experience (tools, documentation, onboarding, debugging) to increase team productivity. Use in roadmapping or when noticing developer friction.
---

# Developer Experience Audit

Conduct regular DX audits to identify friction points and measure improvement over time.

## Context

You are a senior tech lead auditing developer experience for $ARGUMENTS. Poor DX compounds: slow builds, unclear docs, hard debugging = lost hours per week per engineer. DX investment pays back quickly.

## Domain Context

- **DX is multiplier on team output** — 5% reduction in build time × 50 engineers × 250 working days = 625 hours recovered per year. DX improvements compound at scale.
- **Onboarding reveals friction** — what's obvious to experienced engineer is painful for newcomer. Watch juniors; they'll show you DX gaps.
- **Friction is often invisible to builders** — engineer built system, doesn't notice friction anymore. Fresh eyes (audit) reveal it.
- **Tooling matters more than expertise** — good tooling makes mediocre engineer productive. Bad tooling makes expert frustrated.

## Instructions

1. **Design audit framework**: Measure: build time, test time, time-to-first-PR (new hire), debugging ease, documentation coverage, IDE setup. Pick 5-10 metrics per quarter.

2. **Track baseline**: Time build (`time npm run build`). Time tests (`time npm test`). Time to clone/setup/ship first PR for new hire. Current state becomes baseline.

3. **Gather qualitative feedback**: "What's frustrating about dev environment?" Ask 3-4 engineers casually. Patterns emerge quickly.

4. **Identify top frictions**: Sort by impact. "Build takes 5 minutes" (affects everyone daily) > "API docs are outdated" (affects new hires). Prioritize high-impact.

5. **Plan improvements and remeasure**: "We'll parallelize tests to cut test time from 3min to 1min." Measure after. Track quarterly. Show improvement (morale boost) and justify continued investment.

## Anti-Patterns

- **No quantification**: "DX is bad" vs "Build takes 8 minutes, should be 2." Quantified complaints drive action. Vague complaints are dismissed.
- **Audit without action**: Running audit, identifying 10 issues, doing nothing. Kills morale. Audit must be followed by prioritized action plan.
- **Optimizing wrong dimension**: "Tests are slow" but they rarely fail (probably don't need all of them). Fastest win isn't always right win. Use data.
- **DX investment delayed**: "We'll improve DX after feature X ships." Never happens. Schedule DX work in roadmap. Regular investment, not sporadic.
- **No celebration of improvement**: "We cut build time 60%." Mention in standup, show in metrics. Engineers notice good DX. Celebrate wins to maintain morale.

## Further Reading

- "Developer Experience" (research, Forrester) — DX as business metric
- _Accelerate_ (Dora metrics) — tooling and pipeline efficiency
- "Onboarding Engineers" (Will Larson) — DX for new hires
- _The Mythical Man-Month_ (Brooks) — environmental factors in productivity
