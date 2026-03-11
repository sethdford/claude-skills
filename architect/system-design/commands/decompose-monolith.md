---
description: Assess monolith and plan migration to services. Provides step-by-step extraction roadmap.
argument-hint: [monolith description or codebase analysis]
---

# Decompose Monolith

Chain these steps:

1. Use the `monolith-assessment` skill to evaluate pain (deployment frequency, team velocity, scaling bottlenecks). Score pain vs cost of splitting.

2. Use the `system-decomposition` skill to identify business capability seams. Ask: "Could I deploy this feature without touching that code?"

3. Use the `event-driven-architecture` skill to design inter-service communication. Identify events published by each extracting service. Design saga patterns for distributed transactions.

4. Use the `domain-driven-design` skill to ensure each extracted service is a coherent bounded context. Verify ubiquitous language is consistent within each context.

5. Use the `caching-strategy` skill to identify where caching reduces coupling. Example: cache customer data in order-service instead of calling customer-service synchronously.

## Deliverables

Produce:

- **Pain Score Matrix**: Current monolith pain score (deployment, velocity, scaling, team throughput). Target state for each metric.
- **Service Extraction Roadmap**: 3-6 month phased plan. First extract service with lowest risk, highest pain relief.
- **Phase 1 Service Spec**: Name, responsibilities, API, events published/subscribed, database, team ownership
- **Strangler Fig Plan**: How to run old and new code in parallel during transition. Include feature flags, data sync strategy.
- **Fallback Plan**: If extraction fails, how to roll back? What mirrors data to old monolith?

## Critical Thinking Prompts

Before committing:

- What's the actual cost of extraction (dev time, ops, testing)? Does pain relief justify it?
- Which team will own the new service? Are they ready for operational complexity?
- What data must sync between monolith and new service during transition? How long?
- If we extract this service and it performs poorly, how hard is it to move back?
- What's the minimum viable service? Can we extract less and still relieve pain?

## Follow-Up Commands

- `architect-system` — After extraction, design remaining monolith or full system
- `design-infrastructure` — Plan deployment, containers, orchestration
- `disaster-recovery` — Design recovery for new distributed system
