---
name: data-flow-diagram
description: Design data movement and transformation pipelines. Show how data flows between systems, transforms, and where it's stored. Use when architecting data integrations or ETL processes.
---

# Data Flow Diagram

Visualize data movement, transformations, and storage across systems to identify bottlenecks and design efficient pipelines.

## Context

You are designing how data flows between systems. Document data sources, transformations, sinks, and timing. Read existing architecture documents and data pipelines.

## Domain Context

Based on enterprise data architecture patterns and streaming frameworks:

- **Batch Processing**: High-latency, high-throughput; good for analytics and reports
- **Stream Processing**: Low-latency, event-driven; good for realtime features and monitoring
- **Lambda Architecture**: Batch + streaming for both completeness and speed
- **Transformation Stages**: Extract, transform (business logic), load; validate at each stage
- **Data at Rest vs In Motion**: Storage systems vs message queues and streams

## Instructions

1. **Identify Data Sources**: List all sources (APIs, databases, event streams, user uploads). For each, note volume, frequency, data format, and reliability.

2. **Map Transformations**: What business logic applies? Normalize, enrich, aggregate, filter? Where does the transformation happen (source, pipeline, destination)? What's the latency requirement?

3. **Define Sinks and Destinations**: Where does processed data land? Data warehouse for analytics? Cache for serving? Message queue for downstream consumers? API for external systems?

4. **Choose Processing Model**: Batch (daily jobs) or streaming (realtime)? Hybrid (Lambda)? Consider latency, cost, operational complexity, and consistency needs.

5. **Diagram the Flow**: Show sources, transformation stages, queues, storage, consumers. Mark synchronous vs asynchronous flows. Identify potential failure points and bottlenecks.

## Anti-Patterns

- **Spaghetti Pipelines**: Too many ad-hoc integrations between systems. Result: impossible to understand data lineage, hard to modify. **Guard**: Create canonical pipeline architecture; consolidate sources.
- **No Staging Environment**: Transform data directly to production analytics. Result: bugs corrupt historical data. **Guard**: Stage transformations; validate data quality before final load.
- **Ignoring Failure Recovery**: Assume pipelines always succeed. Result: gaps in data, silent failures. **Guard**: Implement idempotent transformations, track completion, replay on failure.
- **Tight Coupling Between Stages**: Output of one transformation directly feeds next without buffering. Result: failure cascades. **Guard**: Use message queues; decouple producers and consumers.

## Further Reading

- _Designing Data-Intensive Applications_ by Martin Kleppmann — data pipeline patterns
- _The Art of Statistics_ by David Spiegelhalter — data quality and validation
- _Fundamentals of Data Engineering_ by Joe Reis and Matt Housley — modern data pipelines
