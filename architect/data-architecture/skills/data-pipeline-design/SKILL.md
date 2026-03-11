---
name: data-pipeline-design
description: Design batch and streaming data pipelines. Plan ingestion, transformation, quality checks, and failure recovery. Use when building ETL/ELT systems or data infrastructure.
---

# Data Pipeline Design

Design robust, maintainable data pipelines that reliably move, transform, and validate data at scale.

## Context

You are designing data pipelines (batch or streaming). Plan data flow, transformations, quality gates, failure recovery, and monitoring. Read source systems, target requirements, latency expectations, and volume projections.

## Domain Context

Based on modern data engineering practices (Spark, Airflow, Kafka, Beam):

- **Batch Pipelines**: Scheduled jobs (hourly, daily); high throughput, moderate latency
- **Streaming Pipelines**: Continuous ingestion; low latency, higher operational complexity
- **Micro-batching**: Spark Streaming; lower latency than batch, simpler than true streaming
- **Orchestration**: DAG-based scheduling (Airflow, dbt) for complex multi-stage pipelines
- **Observability**: Monitor latency, throughput, data quality, freshness

## Instructions

1. **Choose Processing Model**: Batch (daily jobs?) or streaming (realtime features?)? Hybrid (Lambda: batch + streaming for both speed and accuracy)? Consider latency SLA and cost.

2. **Design Data Stages**: Raw ingestion (as-is from source) → Bronze. Cleansing and normalization → Silver. Business logic and enrichment → Gold. This layered medallion architecture separates concerns.

3. **Implement Quality Gates**: Validation at each stage. Fail pipeline if data quality drops. Track anomalies: unexpected null rates, value distributions, cardinality changes.

4. **Handle Failures and Recovery**: Idempotent transformations allow safe retries. Checkpoint state for streaming pipelines; resume from last checkpoint on failure. Use dead-letter queues for unparseable records.

5. **Plan Monitoring and Alerting**: Track freshness (when was last successful run?), latency (time from source to sink), volume (record counts by stage), error rates. Alert on anomalies and SLA misses.

## Anti-Patterns

- **No Data Quality Checks**: Assume data from source is clean. Result: garbage in, garbage out. **Guard**: Validate at ingestion; alert on schema changes or anomalies.
- **Tightly Coupled Transformations**: Pipeline is monolithic script. Result: hard to test, reuse, debug. **Guard**: Break into modular stages; each stage is independently testable.
- **No Checkpoint/Recovery**: Assume pipelines always succeed. Result: gaps in data, lost work. **Guard**: Checkpoint state; design for idempotent retries.
- **Ignoring Operational Overhead**: Streaming pipelines look simple at 1MB/s, collapse at 1GB/s. Result: unexpected scaling headaches. **Guard**: Load-test pipelines; plan infrastructure for 10x growth.

## Further Reading

- _Fundamentals of Data Engineering_ by Joe Reis and Matt Housley — modern pipeline design
- _The Data Warehouse Toolkit_ by Ralph Kimball — medallion/dimensional modeling
- _Apache Airflow Guide_ — orchestration patterns
