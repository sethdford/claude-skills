# Claude Skills — PDLC Role Collection

Comprehensive, standards-grounded Claude Code skills for every role in the Product Development Lifecycle.

**454 skills** and **173 commands** across **57 plugins** for **8 roles**.

## Roles

| Role                                 | Skills | Commands | Plugins | Standards Alignment                               |
| ------------------------------------ | ------ | -------- | ------- | ------------------------------------------------- |
| [architect](./architect)             | 63     | 10       | 8       | TOGAF, IASA BTABoK, ISO 42010, SWEBOK v4          |
| [engineer](./engineer)               | 65     | 26       | 8       | SWEBOK v4, SFIA v9, DORA, SPACE, ISO 25010        |
| [product-manager](./product-manager) | 65     | 26       | 8       | AIPMM PmBoK, ISPMA SPMBoK, PDMA NPDP              |
| [tech-lead](./tech-lead)             | 63     | 25       | 8       | SFIA v9, DORA/Accelerate, Team Topologies         |
| [security](./security)               | 64     | 25       | 8       | NIST CSF 2.0, OWASP SAMM, MITRE ATT&CK, ISO 27001 |
| [designer](./designer)               | 63     | 27       | 8       | WCAG 2.2, ISO 9241, Nielsen Heuristics            |
| [qa-engineer](./qa-engineer)         | 63     | 26       | 8       | ISTQB, ISO 25010, WCAG 2.2, IEEE 829              |
| [sdlc](./sdlc)                       | 8      | 8        | 1       | ISO/IEC 12207, ISO/IEC 15288                      |

## What Makes This Different

Every skill is built on three principles:

1. **Standards-grounded** — Each role maps to recognized professional bodies of knowledge (SWEBOK, TOGAF, OWASP, AIPMM). See [STANDARDS.md](./STANDARDS.md).
2. **LLM error mitigation** — Every skill has an Anti-Patterns section targeting documented LLM failure modes (hallucination, over-generalization, constraint blindness, happy-path bias).
3. **Artifact-producing** — Every skill produces a concrete deliverable (document, diagram, decision record, test plan, policy), not just advice.

## Quick Start

### Install a Single Role

```bash
claude install github:sethdford/claude-skills/engineer
```

### Install a Single Plugin

```bash
claude install github:sethdford/claude-skills/engineer/testing
```

### Install All Roles

```bash
claude install github:sethdford/claude-skills
```

## Skills vs Commands

- **Skills** are domain knowledge units (nouns). They teach Claude about a topic — like writing an ADR, designing a threat model, or creating a product roadmap.
- **Commands** are workflows (verbs). They chain multiple skills together — like running a full architecture review or planning a product launch.

## Role Breakdown

### Architect — 8 Plugins

| Plugin                  | Skills | Commands | Focus                                                       |
| ----------------------- | ------ | -------- | ----------------------------------------------------------- |
| system-design           | 10     | 4        | Decomposition, DDD, microservices, event-driven, CQRS       |
| quality-attributes      | 8      | 3        | Scalability, reliability, performance, trade-off analysis   |
| decision-making         | 8      | 3        | ADRs, technology radar, build-vs-buy, migration strategy    |
| data-architecture       | 8      | 3        | Data modeling, storage selection, event sourcing, pipelines |
| infrastructure-design   | 8      | 3        | Cloud architecture, deployment, DR, multi-region            |
| architecture-governance | 7      | 3        | Principles, fitness functions, tech debt, compliance        |
| communication           | 7      | 3        | C4 diagrams, RFCs, stakeholder presentations, roadmaps      |
| architect-toolkit       | 7      | 3        | Katas, reviews, mentoring, anti-patterns catalog            |

### Engineer — 8 Plugins

| Plugin                  | Skills | Commands | Focus                                                  |
| ----------------------- | ------ | -------- | ------------------------------------------------------ |
| code-quality            | 10     | 4        | Clean code, refactoring, SOLID, code smells            |
| testing                 | 9      | 4        | TDD, property-based testing, test architecture         |
| debugging               | 8      | 3        | Systematic debugging, root cause analysis, postmortems |
| implementation-patterns | 8      | 3        | Design patterns, data structures, concurrency          |
| api-development         | 8      | 3        | REST, GraphQL, gRPC, API design and testing            |
| devops-practices        | 8      | 3        | CI/CD, containers, deployment, monitoring              |
| database-engineering    | 7      | 3        | Schema design, query optimization, migrations          |
| engineer-toolkit        | 7      | 3        | Technical writing, git workflow, incident response     |

### Product Manager — 8 Plugins

| Plugin                 | Skills | Commands | Focus                                                    |
| ---------------------- | ------ | -------- | -------------------------------------------------------- |
| discovery              | 10     | 4        | Problem discovery, customer research, opportunity sizing |
| strategy               | 8      | 3        | Vision, positioning, business model, OKRs                |
| prioritization         | 8      | 3        | RICE, Kano, cost-of-delay, roadmapping                   |
| requirements           | 9      | 4        | PRDs, user stories, acceptance criteria, edge cases      |
| analytics              | 8      | 3        | Metrics, experimentation, funnel/cohort analysis         |
| launch                 | 8      | 3        | GTM, beta programs, rollout strategy, readiness          |
| stakeholder-management | 7      | 3        | Communication, alignment, decision logs                  |
| pm-toolkit             | 7      | 3        | Retros, product reviews, briefs, advisory boards         |

### Tech Lead — 8 Plugins

| Plugin                      | Skills | Commands | Focus                                               |
| --------------------------- | ------ | -------- | --------------------------------------------------- |
| technical-planning          | 9      | 4        | Roadmaps, estimation, sprint planning, capacity     |
| code-review-leadership      | 8      | 3        | Review standards, culture, quality gates            |
| team-development            | 8      | 3        | Mentoring, 1:1s, skill matrices, career ladders     |
| technical-decision-making   | 8      | 3        | RFCs, tech evaluation, spikes, decision matrices    |
| process-engineering         | 8      | 3        | Workflows, branching, releases, incidents           |
| cross-functional-leadership | 7      | 3        | PM partnership, design handoff, scope negotiation   |
| engineering-excellence      | 8      | 3        | Standards, DX, tooling, testing/monitoring strategy |
| tech-lead-toolkit           | 7      | 3        | Journaling, health checks, retros, team charters    |

### Security — 8 Plugins

| Plugin                  | Skills | Commands | Focus                                                 |
| ----------------------- | ------ | -------- | ----------------------------------------------------- |
| threat-modeling         | 9      | 4        | STRIDE, attack trees, trust boundaries, risk scoring  |
| secure-development      | 9      | 3        | Secure coding, OWASP, auth/authz, cryptography        |
| application-security    | 8      | 3        | SAST, DAST, dependency scanning, API security         |
| infrastructure-security | 8      | 3        | Cloud security, containers, IAM, zero-trust           |
| compliance-governance   | 8      | 3        | GDPR, SOC2, PCI-DSS, audit readiness                  |
| incident-response       | 8      | 3        | IR planning, forensics, containment, postmortems      |
| security-operations     | 7      | 3        | SIEM, detection engineering, vulnerability management |
| security-toolkit        | 7      | 3        | Champion programs, red teams, bug bounty, metrics     |

### Designer — 8 Plugins

| Plugin              | Skills | Commands | Focus                                                       |
| ------------------- | ------ | -------- | ----------------------------------------------------------- |
| design-research     | 10     | 4        | Personas, empathy maps, journey maps, JTBD                  |
| design-systems      | 8      | 3        | Tokens, components, accessibility, theming                  |
| ux-strategy         | 8      | 3        | Competitive analysis, design principles, experience mapping |
| ui-design           | 9      | 4        | Color, typography, layout, responsive, data viz             |
| interaction-design  | 7      | 3        | Micro-interactions, state machines, gestures, errors        |
| prototyping-testing | 8      | 4        | Wireframes, usability testing, A/B experiments              |
| design-ops          | 7      | 3        | Critique, handoff specs, sprint planning, workflows         |
| designer-toolkit    | 6      | 3        | Rationale, presentations, case studies, UX writing          |

### QA Engineer — 8 Plugins

| Plugin                | Skills | Commands | Focus                                                          |
| --------------------- | ------ | -------- | -------------------------------------------------------------- |
| test-strategy         | 10     | 4        | Test planning, risk-based testing, coverage analysis           |
| functional-testing    | 9      | 4        | Equivalence partitioning, boundary analysis, state transitions |
| automation            | 8      | 3        | Frameworks, page object model, CI integration, flaky tests     |
| performance-testing   | 8      | 3        | Load testing, stress testing, capacity planning                |
| api-testing           | 8      | 3        | Contract testing, integration, mocks, schema validation        |
| quality-metrics       | 7      | 3        | Defect metrics, dashboards, release readiness                  |
| accessibility-testing | 7      | 3        | WCAG compliance, screen readers, keyboard navigation           |
| qa-toolkit            | 6      | 3        | Bug reports, exploratory testing, regression strategy          |

### SDLC Cross-Role — 1 Plugin

| Plugin          | Skills | Commands | Focus                                                                                |
| --------------- | ------ | -------- | ------------------------------------------------------------------------------------ |
| sdlc-cross-role | 8      | 8        | Phase gates, DoR/DoD, feature lifecycle, release checklists, incident-to-improvement |

## Standards Alignment

See [STANDARDS.md](./STANDARDS.md) for the complete mapping of each role to industry standards, academic bodies of knowledge, and the LLM error mitigation strategy.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## License

MIT — see [LICENSE](./LICENSE).
