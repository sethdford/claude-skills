---
name: monitoring-strategy
description: Design monitoring and alerting that catches production issues fast without creating alert fatigue. Use when establishing observability or improving incident response.
---

# Monitoring Strategy

Build monitoring that surface real problems without drowning on-call in noise.

## Context

You are a senior tech lead designing monitoring for $ARGUMENTS. Poor monitoring means bugs reach customers before engineers know. Alert fatigue means on-call ignores pages. Good monitoring is invisible until needed.

## Domain Context

- **Alert fatigue kills on-call** — 100 alerts per week, 95% are noise. On-call ignores all of them. One real alert gets missed. Better 5 high-signal alerts.
- **Metrics vs logs vs traces** — metrics (aggregates: error rate, latency) catch systemic issues. Logs (raw events) show what happened. Traces (request path) show why. Combine all three.
- **Threshold choice is hard** — alert if error rate > 1%? Too sensitive (flaky). > 5%? Too late (customers angry). Data-driven thresholds (measure typical variation, alert on 3-sigma) work better.
- **Observability compounds** — monitoring in place, you optimize. "Error rate spiked at 3am, went back to normal. Why? Debug tools enabled fast diagnosis." Without monitoring, issues are mysterious.

## Instructions

1. **Define SLOs (Service Level Objectives)**: "99.9% uptime," "p95 latency < 100ms." SLOs drive monitoring. Alert when at risk of missing SLO.

2. **Choose metrics**: Request latency (p50, p95, p99), error rate (by type), throughput (requests/second), queue depth (if applicable). 5-10 key metrics per service.

3. **Set alert thresholds carefully**: Use historical data. "Error rate usually 0.1%, spike to 0.3% is normal variance. Alert if > 1%." Threshold = normal_level + 3×stddev.

4. **Alert on trends, not absolutes**: "Error rate jumped from 0.1% to 2% in 5 minutes" is actionable. "Error rate is 0.5%" is not (normal). Alert on change, not absolute.

5. **Invest in runbooks**: When alert fires, on-call has 1-pager: what does this alert mean, what do you do about it, how do you escalate? Runbooks enable fast resolution.

## Anti-Patterns

- **Alert fatigue**: Hundred alerts per week, on-call ignores them. Real incident gets missed. Better to under-alert and miss some issues than over-alert and miss all.
- **No context in alerts**: Alert says "Error rate high" without context (which service? which endpoint?). On-call can't debug. Alerts should include enough context for diagnosis.
- **Monitoring but no dashboards**: Data collected but hard to visualize. On-call can't explore. Invest in dashboards (key metrics visible at a glance).
- **Monitoring production only**: Debugging issues means looking at logs. If logs only exist in production, hard to debug locally. Log in all environments.
- **Alert without action**: Alert fires, on-call doesn't know what to do. Runbook is missing or unclear. Every alert should have runbook.

## Further Reading

- "Google SRE Book" (Chapters on monitoring) — monitoring at scale
- _The Art of Monitoring_ (Arturo) — philosophy and practice
- "Observability Engineering" (O'Reilly) — modern observability
- "Alerting on SLOs" (Google Cloud) — threshold selection
