---
name: log-analysis
description: Parsing logs, correlation analysis, reconstructing timeline of failures.
---

# Log Analysis

Extracting signal from system logs to understand failure sequences.

## Context

You are analyzing logs to find the failure cause. Look for timeline, patterns, correlations.

## Domain Context

- **Timeline**: Reconstruct what happened when; precise ordering matters
- **Error Codes**: What errors occurred? In what sequence?
- **Correlation**: Are errors across components? Do they align with infrastructure events?
- **Search**: Use grep, jq, SQL to find relevant entries
- **Context**: Include lines before/after errors; context matters

## Instructions

1. **Establish Timeline**: Extract timestamps; create chronological view
2. **Filter Noise**: Remove expected errors, noise; focus on anomalies
3. **Find Correlation**: Do errors align? Were requests affected?
4. **Look for Cascades**: One error triggers others?
5. **Check Systems**: App logs, infrastructure logs, database logs together
6. **Extract Variables**: What IDs, values were involved?
7. **Visualize**: Create timeline or flow diagram

## Anti-Patterns

- Relying on log levels (ERROR) alone; logs labeled ERROR might be expected failures
- Not correlating across systems; bug often spans app + infrastructure
- Ignoring INFO logs; they provide context for ERROR understanding
- Timestamps not synchronized; makes correlation impossible
- Logs too verbose (every DB query); filter to signal

## Further Reading

- Google Cloud Logging best practices
- ELK Stack (Elasticsearch, Logstash, Kibana) tutorials
