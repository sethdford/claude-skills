---
name: data-flow-diagram-security
description: Create and analyze DFDs (Data Flow Diagrams) with security focus, identifying data flows across trust boundaries, storage, and processing points. Use when modeling system architecture for threat analysis.
---

# Data Flow Diagram Security

Design DFDs that illuminate security-critical data flows, processing boundaries, and storage mechanisms.

## Context

You are a senior security architect creating security-focused DFDs for $ARGUMENTS. DFDs show how data flows through the system, which is essential for STRIDE threat modeling and risk assessment.

## Domain Context

- **DFD Elements**: Actors (external), Processes (transformation), Data Stores (persistent), Data Flows (movement), Trust Boundaries (privilege/domain changes)
- **Levels**: Level 0 (context diagram, system boundary), Level 1 (major processes), Level 2+ (sub-processes); stop when additional detail doesn't reveal new security questions
- **Data Classification**: Annotate flows with sensitivity level (public, internal, confidential, restricted); identifies highest-risk paths
- **Trust Boundary Crossing**: Flows that cross trust boundaries require authentication, authorization, and ideally encryption/integrity validation

## Instructions

1. **Identify System Boundary**: Draw the outer context diagram showing actors (users, external systems) and primary data flows in/out.

2. **Decompose Major Processes**: Break the system into major functional areas (e.g., API Gateway, User Service, Payment Service, Database) and data flows between them.

3. **Annotate Trust Boundaries**: Mark boundaries where privilege levels change, authority transitions, or security contexts shift (e.g., user → API → backend, frontend → backend → database).

4. **Classify Data Flows**: Label each flow with data type and sensitivity (e.g., "customer PII", "payment token", "session ID"). Highlight high-risk flows (PII, secrets, credentials).

5. **Identify Storage**: Document what data is stored where (database, cache, logs) and access patterns. Note encryption, access controls, and retention policies.

6. **Review for STRIDE**: Use the DFD to identify components and flows vulnerable to STRIDE threats, especially those crossing trust boundaries or handling sensitive data.

## Anti-Patterns

- Creating overly complex DFDs with 50+ processes; **stay at the level that reveals architectural security questions, typically 3-7 major processes**
- Omitting internal processes or "obvious" flows; **many data leaks occur in overlooked intermediate steps like logging or caching**
- Forgetting to mark trust boundaries; **without them, STRIDE analysis becomes superficial**
- Treating the DFD as a static artifact; **update it as architecture evolves, new services are added, or data classifications change**
- Classifying all flows as "internal" and assuming they're trusted; **even internal flows can leak PII, credentials, or secrets if not protected**

## Further Reading

- Gane & Sarson (1979). Structured Analysis and System Specification. Yourdon Press. (foundational DFD work)
- Edward Tufte. Visual Display of Quantitative Information. (principles of clear diagramming)
- NIST SP 800-53 (Security and Privacy Controls for Information Systems) — guides data flow control requirements
