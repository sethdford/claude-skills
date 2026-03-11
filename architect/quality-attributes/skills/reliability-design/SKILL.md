---
name: reliability-design
description: Design systems that fail gracefully and recover automatically. Use when defining SLAs, designing for fault tolerance, or improving uptime.
---

# Reliability Design

Build systems that anticipate failures, degrade gracefully, and recover automatically. Design for MTBF and MTTR trade-offs.

## Context

You are designing for reliability. The user faces uptime requirements, wants to reduce MTTR, or needs to design disaster recovery. Read their current SLAs and failure modes.

## Domain Context

Based on Nygard's Release It! and Google's SRE practices:

- **MTBF (Mean Time Between Failures)**: How long before next failure? Increase by building fault-tolerant systems
- **MTTR (Mean Time To Recovery)**: How long to recover? Decrease by automating recovery and alerting
- **Graceful Degradation**: When components fail, reduce functionality rather than crashing entirely
- **Fault Isolation**: Failures contained to one component; don't cascade
- **Observability**: Can you see problems before users do? Metrics, logs, traces for every critical path

## Instructions

1. **Define SLA/SLO/SLI**:
   - **SLA**: Service level agreement (e.g., 99.99% uptime) with penalties
   - **SLO**: Service level objective (internal target, e.g., 99.95%)
   - **SLI**: Service level indicator (measured metric, e.g., "request success rate")

2. **Map Failure Modes**: For each critical component, ask: "What happens if this fails?" Example: database down → query service fails → frontend shows error.

3. **Design Fault Isolation**: Use bulkheads (thread pools per dependency), timeouts, and circuit breakers. Ensure one service failure doesn't bring down others.

4. **Plan Recovery**: For each failure, specify recovery mechanism. Database replica failover (automated)? Service restart? Manual intervention?

5. **Establish Monitoring**: Instrument critical paths with metrics (request latency, success rate, queue depth). Alert when approaching SLI threshold.

## Anti-Patterns

- **SLA Without Measurement**: Promise 99.9% uptime but don't measure it. **Guard**: Define SLI, measure continuously, publish results.
- **Overengineering Reliability**: Build 99.999% uptime when 99.9% is sufficient. Cost of 9's grows exponentially. **Guard**: Right-size SLA to business impact; don't over-engineer.
- **Assuming Graceful Degradation Works**: Design degrades but don't test it. Result: degraded mode is broken. **Guard**: Test failure scenarios regularly (chaos engineering).
- **No Alerting on Recovery**: Failure happens, gets fixed automatically, nobody knows. Result: pattern not addressed. **Guard**: Alert on failures even if auto-recovered.

## Further Reading

- _Release It!_ by Michael Nygard — failure modes and defensive programming
- _Site Reliability Engineering_ by Google — SRE principles and practices
- _The Phoenix Project_ by Gene Kim et al. — understanding system dependencies
