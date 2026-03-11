---
name: work-breakdown-structure
description: Decompose complex initiatives into manageable work items with clear ownership and milestones. Use when planning large features or multi-team projects.
---

# Work Breakdown Structure

Create hierarchical decomposition of large initiatives to clarify scope, ownership, and sequencing.

## Context

You are helping break down a complex project or feature into work items for sprint planning and execution. If you have an epic, feature, or initiative description, use it to guide decomposition.

## Domain Context

- Project Management Institute (PMI) defines WBS as the foundation of project planning and risk management
- Larson: effective WBS drives clear ownership and reveals hidden dependencies early
- Agile best practice: WBS at epic/feature level guides refinement; detailed tasks emerge during sprint planning, not upfront

Key principles:

1. **Decompose until ownership is clear**: Each work item should have one obvious owner (engineer or small squad)
2. **Stop before over-specification**: Detailed task lists become stale quickly. Decompose to stories/features, not tasks
3. **Show dependencies visually**: A good WBS reveals which pieces must happen first and which can happen in parallel

## Instructions

1. **Start with the initiative**: Write a one-paragraph description of the business goal and success criteria. Example: "Migrate user authentication from custom JWT to OpenID Connect to reduce security risk and enable SSO"
2. **Identify work streams**: Break into 3-5 major themes. Example: infrastructure (OIDC service setup), client (integrations on web/mobile), backend (credential migration), operations (runbook and support)
3. **For each work stream, list epics**: Break into 1-2 quarter-sized chunks. Example: "Set up OIDC infrastructure and staging environment" then "Migrate production credentials in phases"
4. **For each epic, estimate scope**: Use t-shirt sizing (S/M/L). Is it 1 sprint (S), 2-3 sprints (M), or 4+ sprints (L)?
5. **Identify critical dependencies**: Mark which epics must complete before others start. Use arrows or tables to show sequencing
6. **Assign ownership**: Identify tech lead or senior engineer responsible for each epic. They will drive refinement
7. **Define done criteria**: For each epic, state what "done" means (code review approved, tested in staging, documentation complete, runbook validated)

Example structure:

```
Authentication Migration
├─ OIDC Infrastructure (Owner: Backend Lead)
│  ├─ Set up OIDC provider (identity.example.com)
│  ├─ Deploy in staging, validate with staging users
│  └─ Production infrastructure hardening
├─ Web Client (Owner: Frontend Lead)
│  ├─ Integrate OIDC library, handle token refresh
│  ├─ Migrate local storage to secure storage
│  └─ Test SSO across browsers
├─ Mobile Client (Owner: Mobile Lead)
│  ├─ Native OIDC integration (iOS & Android)
│  └─ Validate on device, handle edge cases
└─ Migration & Operations (Owner: Platform Lead)
   ├─ Data migration (JWT → OIDC credentials)
   ├─ Runbook and support training
   └─ Rollback plan validation
```

## Anti-Patterns

- **Over-decomposition**: LLMs sometimes create 50-task WBS when 10-15 epics would suffice. Stop at epic level; tasks emerge during sprint planning. A 3-month WBS should fit on one page.
- **Unrealistic upfront detail**: WBS that assumes you know every dependency and task upfront is fiction. Always include a "discovery/investigation" phase early to surface unknowns.
- **Missing the "done" definition**: A WBS without done criteria leads to scope creep. Always specify what signals each epic is complete (code shipped, tests passing, docs written, support trained).
- **Ignoring dependency chains**: LLMs often create parallel tasks that actually have hidden dependencies. Review WBS with the team to surface real sequencing.

## Further Reading

- PMI. "A Guide to the Project Management Body of Knowledge." 2021. Chapter on WBS development.
- Larson, Will. "An Elegant Puzzle." Chapter on project scoping and ownership.
- McConnell, Steve. "Software Estimation: Demystifying the Black Art." Microsoft Press, 2006.
