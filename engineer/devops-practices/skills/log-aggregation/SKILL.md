---
name: log-aggregation
description: ELK Stack, structured logging, log query patterns, and centralized log management.
---

# Log Aggregation

Collecting, indexing, and querying logs for debugging and monitoring.

## Context

You are setting up log aggregation. Use structured logs; make them queryable.

## Domain Context

- **Structured**: JSON logs with fields; queryable not text
- **Trace ID**: Correlate logs across services
- **Centralized**: Logs from all services in one place
- **Retention**: How long to keep logs? Cost/value tradeoff
- **Searchability**: Fast queries for debugging

## Instructions

1. **Structured Logging**: JSON with fields not free text
2. **Trace ID**: Include on every log; correlate across services
3. **Log Levels**: DEBUG, INFO, WARN, ERROR; use appropriately
4. **Centralization**: ELK, Datadog, Splunk; pick one
5. **Filtering**: Useful queries to narrow down issues
6. **Retention**: Keep recent logs accessible; archive old
7. **Performance**: Don't log too much; expensive and slow

## Anti-Patterns

- Text logs without structure; can't query programmatically
- No trace IDs; can't correlate across services
- Logging everything; too much data, hard to find signal
- Keeping logs forever; expensive storage
- No log pipeline; raw logs, no transformation/enrichment

## Further Reading

- ELK Stack documentation
- Structured logging guide
- Log aggregation best practices (Google Cloud)
