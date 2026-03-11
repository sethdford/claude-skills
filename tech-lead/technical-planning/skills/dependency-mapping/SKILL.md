---
name: dependency-mapping
description: Identify and visualize dependencies between teams, systems, and work items to prevent blocked work. Use when planning cross-team initiatives.
---

# Dependency Mapping

Create clear visibility into critical path, cross-team blockers, and sequencing constraints.

## Context

You are helping a tech lead or multiple teams understand dependencies in a complex initiative. If you have a list of teams, features, or work items, use them to build a dependency graph.

## Domain Context

- Theory of Constraints (Goldratt, "The Goal"): identifying and managing the critical path is how to unblock complex work
- Larson: mismanaged cross-team dependencies are the #1 source of timeline slippage
- Systems thinking: dependencies often cascade; removing one blocker reveals the next

Key principles:

1. **Explicit beats implicit**: Dependencies that are unspoken get discovered painfully. Write them down
2. **Differentiate types**: Blocking (task B cannot start until A finishes), informational (good to know), and resource (same person needed on both tasks)
3. **Shorten critical path**: Focus optimization on the longest dependency chain, not everything

## Instructions

1. **List all work items**: From your WBS or roadmap, create a flat list of epics, features, or projects with owners
2. **For each item, ask**: "What must be done before we can start this?" Create pairs (A depends on B)
3. **Classify dependencies**:
   - **Blocking**: Task cannot start until dependency finishes (e.g., backend API must exist before mobile integrates)
   - **Resource**: Same engineer needed on both (cross-team pair programming or handoff)
   - **Informational**: Useful to know but not blocking (e.g., design feedback for next phase)
4. **Build the graph**: Use a simple table or ASCII diagram. Example:
   ```
   Item                    | Depends On            | Type      | Owner
   ─────────────────────────────────────────────────────────────────
   Mobile OIDC integration | OIDC API staging      | Blocking  | Mobile Lead
   OIDC API staging        | Identity svc deployed | Blocking  | Backend Lead
   Identity svc deployed   | Infrastructure ready  | Blocking  | Infra Lead
   Support training        | Runbook completed     | Blocking  | Platform Lead
   ```
5. **Find the critical path**: Trace the longest chain of blocking dependencies. Optimizing this path moves the overall delivery date
6. **Identify parallelization**: Look for non-blocking items that can run in parallel (e.g., web client development and mobile can run simultaneously after API is ready)
7. **Plan handoff points**: For each dependency, schedule a handoff meeting. Ensure receiver knows acceptance criteria and ETA
8. **Build contingency plans**: For each critical path item, ask "what if this slips by 1 week?" Plan alternate routes or parallel work

## Anti-Patterns

- **Assuming hidden dependencies will emerge naturally**: LLMs often assume teams will "figure it out" during execution. Explicit dependency mapping prevents surprises. Always document assumptions upfront.
- **Ignoring resource conflicts**: Two critical path items might need the same specialist. LLMs often miss these shared resource constraints. Ask "who is doing this?" for each item.
- **Treating all dependencies equally**: Blocking dependencies matter; informational ones are noise. LLMs sometimes create dependency graphs that are too detailed and lose signal. Focus on blocking dependencies only.
- **No contingency for critical path slippage**: Plans assume everything on the critical path finishes on time. Have a plan B if any critical item slips.

## Further Reading

- Goldratt, Eliyahu. "The Goal: A Process of Ongoing Improvement." North River Press, 1984. Theory of Constraints.
- Larson, Will. "An Elegant Puzzle." Chapter on managing complex projects and dependencies.
- Reilly, Tanya. "The Staff Engineer's Path." Chapter on managing large organizational changes.
