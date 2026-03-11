---
name: architecture-roadmap
description: Create multi-quarter architecture vision and roadmap. Prioritize initiatives, estimate effort, communicate strategy. Use when planning architecture evolution or communicating long-term vision.
---

# Architecture Roadmap

Create strategic architecture roadmap aligned with business goals and organizational capacity.

## Context

You are planning architecture evolution over next 2-4 quarters. Prioritize initiatives, estimate effort, communicate strategy to stakeholders. Read business strategy, current technical gaps, team capacity.

## Domain Context

Based on strategic planning and architecture roadmapping:

- **Architecture Initiatives**: Major changes (migrate to microservices, refactor database, implement observability)
- **Dependencies**: Some initiatives block others. Database migration must complete before service redesign.
- **Timeline**: When should each initiative start? Capacity constraints (limited team, shared resources).
- **Communication**: Regular updates to stakeholders. Adapt roadmap as priorities shift.

## Instructions

1. **Identify Themes**:
   - Year 1: Foundation (infrastructure, observability, deployment automation)
   - Year 2: Scale (microservices, database sharding, multi-region)
   - Year 3: Maturity (compliance, security, advanced optimizations)

2. **Define Initiatives** (per quarter):
   - Q1: "Implement centralized logging and monitoring" (2 engineers, 4 weeks)
   - Q2: "Migrate from EC2 to Kubernetes" (3 engineers, 8 weeks)
   - Q3: "Split monolith into microservices (Payment)" (4 engineers, 10 weeks)

3. **Map Dependencies**: Q1 enables Q2 (monitoring needed before K8s migration). Q2 enables Q3 (K8s for service deployment).

4. **Estimate Effort**: Be honest. "Migrate monolith" is 6+ months, not 2. Pad estimates; add contingency.

5. **Communicate Regularly**: Monthly updates to leadership. Celebrate completions. Adjust for new priorities. Show progress.

## Anti-Patterns

- **Roadmap Set in Stone**: Never changes. Reality doesn't match plan. Result: roadmap ignored, decisions made ad-hoc. **Guard**: Review quarterly; adjust based on new information.
- **Too Ambitious**: Promise 10 initiatives in 3 months. Result: miss all deadlines, team burned out. **Guard**: Realistic scope; 2-3 major initiatives per quarter max.
- **No Dependency Tracking**: Start initiatives in wrong order, blocked by other work. Result: slow progress. **Guard**: Explicit dependency map; critical path analysis.
- **No Communication**: Roadmap exists but teams don't know. Result: surprises, resistance. **Guard**: Publish and discuss; gather feedback; explain trade-offs.

## Further Reading

- _Roadmapping in Product Management_ by Todd Olson — strategic planning
- _The Goal_ by Eliyahu Goldratt — dependency and bottleneck management
- _Scaling Up_ by Verne Harnish — organizational alignment and execution
