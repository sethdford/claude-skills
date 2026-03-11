---
name: monitoring-instrumentation
description: Metrics, logs, traces (observability); choosing what to measure, dashboards, and incident response.
---

# Monitoring Instrumentation

Observing systems to understand behavior and detect problems.

## Context

You are planning observability. Measure what matters; enable debugging.

## Domain Context

- **Metrics**: Numbers (latency, errors, CPU); aggregated, queryable
- **Logs**: Text events; detailed, high volume
- **Traces**: Request paths; understand where time is spent
- **Dashboards**: Visualize metrics for on-call engineers
- **Alerts**: Notify when metrics exceed thresholds

## Instructions

1. **Define SLOs**: Service level objectives; what matters?
2. **Metrics**: Latency, error rate, throughput; per service/endpoint
3. **Logs**: Structured logs with trace ID for correlation
4. **Traces**: End-to-end request tracking for debugging
5. **Dashboards**: Visualize SLOs; use during incident response
6. **Alerts**: Alert on SLO violations, not absolute thresholds
7. **Runbooks**: Document how to respond to alerts

## Anti-Patterns

- Too many metrics; noisy, hard to find signal
- Alerts with no runbook; on-call engineer guesses
- Logging everything; expensive and hard to search
- No trace IDs; can't correlate across services
- Alerting on absolute thresholds; SLO-based is better

## Further Reading

- Google SRE book on monitoring
- Prometheus documentation
- Distributed tracing (Jaeger, DataDog)
