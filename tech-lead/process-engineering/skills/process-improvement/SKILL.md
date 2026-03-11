---
name: process-improvement
description: Systematically identify and implement process improvements that increase team velocity and reduce friction. Use in retrospectives or when noticing repeated friction points.
---

# Process Improvement

Build a culture of continuous small improvements rather than periodic major overhauls.

## Context

You are a senior tech lead identifying process improvements for $ARGUMENTS. Small recurring frictions compound into major velocity loss. Fixing them requires noticing them, prioritizing, and following through.

## Domain Context

- **Small frictions compound** — 10-minute daily standups × 5 days × 50 weeks = 41 hours per engineer per year. If standup could be 5 minutes, you recover 20 hours. Small improvements aggregate massively.
- **Process improvement is bottleneck identification** — fixing fastest step doesn't help. Fix the constraint. Where do engineers spend time waiting?
- **Kaizen philosophy** — continuous small improvements beat periodic major initiatives. Iterate constantly, improve marginally. Small changes stick; large overhauls cause resistance.
- **Data-driven improvement** — hunches about what slows teams down are often wrong. Measure, then improve what matters most.

## Instructions

1. **Capture process friction**: In retros, ask "What slowed us down this week?" Track complaints. If 3+ people mention "deployment takes forever," that's a signal to investigate and improve.

2. **Measure the pain**: How long does deployment actually take? How many times per week? What's the cost in engineering hours? If deployment is 1x per week and takes 4 hours, that's 4 hours lost per week. Worth fixing.

3. **Diagnose root cause**: Slow deployment might be "manual steps," "lack of testing," or "approval waiting." Root cause determines fix. Don't optimize away wrong cause.

4. **Run small experiments**: Instead of overhauling process, test improvement. "This week, ship on Friday instead of Sunday. Did it hurt? Did it improve visibility?" Reversible experiments reduce risk of bad changes.

5. **Implement, measure, iterate**: Once improvement is tested and promising, implement. Measure results. "We cut deployment time from 4 hours to 1.5 hours." Show impact. Document improvement. Move to next bottleneck.

## Anti-Patterns

- **Improving unmeasured problems**: "Standups are too long, let's cut to 5 minutes." How long are they now? Are they actually the bottleneck? Measure before improving.
- **Big process overhaul initiatives**: "We're redesigning the entire workflow." Massive change initiatives fail, create whiplash. Small improvements sustain.
- **Improvements that don't stick**: Changing process, then not reinforcing. Teams drift back. Changes need repetition to stick.
- **Only retrospective improvements**: Retros identify issues, but if "next sprint" nothing changes, retros feel useless. Act on findings quickly (within 1-2 weeks) to show you take them seriously.
- **No celebration of wins**: Fixed a slow process, saved team 5 hours per week. Don't mention it. Team never realizes the improvement. Celebrate wins. Build morale.

## Further Reading

- _Continuous Improvement_ (Imai, Kaizen) — philosophy of small changes
- _The Goal_ (Goldratt) — bottleneck identification
- _Lean Software Development_ (Poppendieck) — waste identification and removal
- "Retrospectives" (Derby & Larsen) — running effective retrospectives for improvement
