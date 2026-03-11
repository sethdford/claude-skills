---
name: skill-matrix
description: Map team capabilities against current and future role requirements. Use when planning capacity, identifying training needs, or succession planning.
---

# Skill Matrix

Build a capability map showing who has which skills, proficiency levels, and development areas.

## Context

You are a senior tech lead creating a skill matrix for $ARGUMENTS. A skill matrix reveals team strengths, spots critical knowledge silos, and guides targeted development investments.

## Domain Context

- **Cross-training principle**: Teams with redundant skills survive key person dependencies. Single points of failure create risk and burnout.
- **Proficiency levels (Dan Pink)**: Progression from awareness (knows exists) → competence (can do independently) → mastery (teaches others, optimizes).
- **Knowledge silos** are often invisible until someone leaves or gets pulled to other projects. Proactive mapping prevents disaster.
- **Role-based skill requirements** vary by level. Staff engineers need different skills than mid-level contributors.

## Instructions

1. **Define skill domains**: List critical domains (e.g., systems design, API development, DevOps, database optimization, security). Include soft skills: mentoring, code review, incident response. Target 12-20 total skills.

2. **Establish proficiency scale**: Create 4-level system: 1=Aware (understands concept), 2=Competent (solves problems independently), 3=Expert (leads work, mentors others), 4=Authority (sets team standard, solves novel problems). Avoid false precision beyond 4 levels.

3. **Map current team**: One row per person, one column per skill. Use color coding or numbers. Identify who is strongest in each skill. Flag expertise gaps for critical domains.

4. **Compare against role levels**: For each role level (junior, mid, senior, staff), document required proficiency per skill. Show visually: where is the team exceeding requirements? Where are we under-resourced?

5. **Create development roadmap**: Identify high-priority skill gaps and assign growth paths. Example: "Alice is 2-level in systems design, needs 3-level for promotion; assign her 2 architecture reviews quarterly."

## Anti-Patterns

- **Static documents**: Creating a skill matrix once, then ignoring it for 18 months. Skills decay. Update quarterly or when team composition changes. Dead documents mislead succession planning.
- **Inflated self-assessments**: Engineers rating themselves 4 on skills they've barely touched. Use 360 feedback and project-based validation. Calibrate in team discussions.
- **Focusing only on technical skills**: Ignoring mentoring, communication, or incident response. Soft skills determine whether technical experts can lead. Include both dimensions.
- **No follow-up action**: Identifying gaps but not funding development. Engineers notice if you say "we need DevOps skills" but never send anyone to conferences or pair them with the expert.

## Further Reading

- _The Pragmatic Programmer_ (Hunt & Thomas) - cross-training for team resilience
- _Accelerate_ (Dora metrics) - technical practices and team capability assessment
- "Building High-Performing Teams" (Will Larson, Manager Playbook) - visibility into capability planning
- _Adler's Organisational Development_ - role clarity and skill alignment
