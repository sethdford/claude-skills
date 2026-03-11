---
layout: default
title: Claude Skills — PDLC Role Collection
---

# Claude Skills

Comprehensive, standards-grounded Claude Code skills for every role in the Product Development Lifecycle.

**454 skills** | **173 commands** | **57 plugins** | **8 roles**

---

## Quick Start

Install everything:

```bash
claude install github:sethdford/claude-skills
```

Or install by role:

```bash
claude install github:sethdford/claude-skills/engineer
claude install github:sethdford/claude-skills/architect
claude install github:sethdford/claude-skills/security
```

---

## Roles

| Role                                  | Skills | Commands | Standards                                  |
| ------------------------------------- | ------ | -------- | ------------------------------------------ |
| [Architect](./architect/)             | 63     | 10       | TOGAF, IASA BTABoK, ISO 42010, SWEBOK v4   |
| [Engineer](./engineer/)               | 65     | 26       | SWEBOK v4, SFIA v9, DORA, SPACE, ISO 25010 |
| [Product Manager](./product-manager/) | 65     | 26       | AIPMM PmBoK, ISPMA SPMBoK, PDMA NPDP       |
| [Tech Lead](./tech-lead/)             | 63     | 25       | SFIA v9, DORA/Accelerate, Team Topologies  |
| [Security](./security/)               | 64     | 25       | NIST CSF 2.0, OWASP SAMM, MITRE ATT&CK     |
| [Designer](./designer/)               | 63     | 27       | WCAG 2.2, ISO 9241, Nielsen Heuristics     |
| [QA Engineer](./qa-engineer/)         | 63     | 26       | ISTQB, ISO 25010, WCAG 2.2, IEEE 829       |
| [SDLC Cross-Role](./sdlc/)            | 8      | 8        | ISO/IEC 12207, ISO/IEC 15288               |

---

## What Makes This Different

### Standards-Grounded

Every role maps to recognized professional bodies of knowledge — not opinions, not blog posts, not LLM-generated advice. SWEBOK v4 for engineers, TOGAF for architects, NIST CSF for security, ISTQB for QA.

See the full [Standards Alignment](./STANDARDS/).

### LLM Error Mitigation

Every skill includes an **Anti-Patterns** section targeting documented LLM failure modes:

| Failure Mode           | Example                               | How Skills Mitigate                                |
| ---------------------- | ------------------------------------- | -------------------------------------------------- |
| Hallucinated specifics | Citing nonexistent standards          | Require verification against authoritative sources |
| Over-generalization    | "Use microservices" without context   | Mandate constraint gathering before proposals      |
| Happy-path bias        | Ignoring error states                 | Require edge case and failure mode analysis        |
| Cargo-culting          | Popular patterns without fit analysis | Call out "applying X without trade-off analysis"   |
| Constraint blindness   | Ignoring team size, budget            | Context gathering as step 1                        |

### Artifact-Producing

Every skill produces a concrete deliverable — a document, diagram, decision record, test plan, or policy. Not just advice.

---

## Skills vs Commands

**Skills** are domain knowledge units (nouns). They teach Claude about a topic — writing an ADR, designing a threat model, creating a product roadmap.

**Commands** are workflows (verbs). They chain multiple skills together — running a full architecture review, planning a product launch, executing a security assessment.

---

## Contributing

See [CONTRIBUTING](./CONTRIBUTING/) for guidelines. Every skill must include:

1. Domain Context citing real frameworks and standards
2. Instructions with 4-6 concrete steps producing a deliverable
3. Anti-Patterns with 2-4 LLM-specific failure modes
4. Further Reading with real, verifiable references

---

MIT License | [GitHub](https://github.com/sethdford/claude-skills)
