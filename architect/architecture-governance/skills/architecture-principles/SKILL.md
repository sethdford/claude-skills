---
name: architecture-principles
description: Define foundational architecture principles and decision-making rules. Communicate guidelines across organization. Use when establishing architectural standards or updating strategy.
---

# Architecture Principles

Establish foundational principles that guide architectural decisions and align organization.

## Context

You are defining architecture principles for the organization. Create clear, memorable guidelines that inform decisions. Involve stakeholders from product, engineering, and operations.

## Domain Context

Based on architecture governance frameworks (TOGAF, Gartner):

- **Guiding Principles**: High-level philosophy (e.g., "Cloud-first", "Stateless services", "API-driven")
- **Decision Rules**: Specific rules derived from principles (e.g., "Use managed databases not self-hosted" from "Minimize operational burden")
- **Trade-off Hierarchy**: When principles conflict, which takes priority? Performance vs Cost? Consistency vs Availability?
- **Exemptions**: Clear process to override principles; document why and remediation plan
- **Communication**: Memorability matters; short, actionable, memorable

## Instructions

1. **Identify Core Values**: What matters to the organization? Speed of innovation? Cost efficiency? Security? Reliability? List top 3-5.

2. **Derive Principles**: Turn values into principles. "Speed of innovation" → "Ship independently without central coordination". "Cost efficiency" → "Use managed services to reduce operational overhead".

3. **Make Principles Memorable**: Use simple language. "Move fast with confidence" better than "Implement robust CI/CD pipelines". Acronyms help: KISS (Keep It Simple, Stupid).

4. **Create Decision Rules**: For each principle, what are concrete decisions? "Cloud-first" → "Use EC2 not on-prem", "Use Lambda for new services", "Data in S3 not shared NFS".

5. **Communicate and Enforce**: Share with teams. Use in architecture reviews. Celebrate adherence; discuss exceptions constructively. Update as organization evolves.

## Anti-Patterns

- **Too Many Principles**: 20 principles, teams ignore most. Result: becomes noise. **Guard**: 5-7 principles max. Memorable, not exhaustive.
- **Principles Without Teeth**: Define but don't enforce. Result: ignored, no effect. **Guard**: Use in reviews; track compliance; discuss exceptions.
- **Conflicting Principles**: "Always use consistency" vs "Optimize for latency" without hierarchy. Result: confusion. **Guard**: Explicit trade-off hierarchy; example: consistency > cost > speed.
- **No Updates**: Principles defined 5 years ago; organization evolved. Result: misalignment. **Guard**: Review annually; update with changes in strategy.

## Further Reading

- _TOGAF Standard_ — enterprise architecture framework with principle-setting
- _The Art of the Metaobject Protocol_ — principle-driven design
- _Good Architecture is Good Design_ by Simon Brown — clear architectural communication
