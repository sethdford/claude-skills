---
name: observability-design
description: Design observability (metrics, logs, traces) for understanding system behavior in production. Use when debugging distributed systems or building monitoring.
---

# Observability Design

Design comprehensive observability across metrics, logs, and traces to understand system behavior and debug issues.

## Context

You are building observability for a system. The user struggles to debug production issues or wants better visibility. Read their current monitoring setup.

## Domain Context

Based on Google's SRE practices and observability research:

- **Metrics**: Quantitative measurements (latency, error rate, QPS). Fast queries, low cardinality.
- **Logs**: Event records with context (error messages, user actions). High volume, searchable.
- **Traces**: Request flow across services. Shows dependencies and latency breakdown.
- **Correlation IDs**: Link logs and traces across services. Essential for debugging.
- **Cardinality**: Unique values for metric labels. High cardinality (millions of unique values) breaks storage.

## Instructions

1. **Define Key Metrics**: For each critical path, specify SLI metrics (success rate, latency, saturation). Example: order checkout: success rate >99.9%, p99 latency <500ms.

2. **Design Metrics Collection**: Instrument code with metrics (request count, latency histogram, error count). Use metrics library (Prometheus, StatsD). Keep cardinality low.

3. **Configure Logging**: Log key events (authentication, errors, deployments). Include correlation ID in every log. Aggregate logs centrally (ELK, Datadog).

4. **Implement Distributed Tracing**: Every request gets trace ID at entry point. Pass to every downstream service. Record span (service name, operation, latency, result).

5. **Build Dashboards & Alerts**: Dashboard shows health overview (SLI status). Alerts on SLI violation. Alert requires runbook (action to resolve).

## Anti-Patterns

- **High Cardinality Metrics**: Emit metric with user ID as label. Result: millions of unique metrics, breaks storage. **Guard**: Use low-cardinality labels (service, endpoint); never user ID or request ID.
- **Logging Everything**: Log every request, every database call. Result: petabytes of data, can't find signal. **Guard**: Log sparingly; focus on errors and critical paths.
- **No Correlation IDs**: Cannot trace request across services. **Guard**: Correlation ID generated at entry point, passed to all downstream services.
- **Alerts Without Runbooks**: Alert fires but nobody knows what to do. Result: ignored alerts. **Guard**: Every alert must have clear runbook explaining cause and fix.

## Further Reading

- _Google's Site Reliability Engineering_ — observability practices at scale
- _The Art of Monitoring_ by James Turnbull — comprehensive monitoring and alerting strategy
- _Observability Engineering_ by Gundeck and Ligus — modern observability with traces and logs
