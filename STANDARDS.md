# Standards Alignment & Scientific Grounding

Every skill in this collection is anchored to recognized industry standards, academic bodies of knowledge, and empirically-validated frameworks. This document maps each role to its authoritative foundations and explains the evidence-based approach used throughout.

## Methodology

Skills are designed using a three-layer grounding approach:

1. **Body of Knowledge alignment** — Each role maps to a recognized professional BoK or competency standard
2. **Empirical validation** — Practices reference peer-reviewed research, industry surveys (DORA, State of DevOps), or proven frameworks with measurable outcomes
3. **LLM error mitigation** — Every skill includes an Anti-Patterns section targeting documented failure modes of large language models in that domain (hallucination patterns, over-generalization, cargo-culting, constraint blindness)

## Role-to-Standard Mapping

### Architect

| Standard/Framework                   | Source                | Coverage                                                                                         |
| ------------------------------------ | --------------------- | ------------------------------------------------------------------------------------------------ |
| TOGAF 10th Edition                   | The Open Group        | Architecture Development Method, content metamodel, governance                                   |
| IASA BTABoK                          | IASA Global           | 5-pillar competency model (Business, Design, IT Environment, Quality Attributes, Human Dynamics) |
| ISO/IEC/IEEE 42010:2022              | ISO                   | Architecture description standard                                                                |
| SWEBOK v4 — Software Architecture KA | IEEE Computer Society | New in v4: architecture as first-class knowledge area                                            |
| C4 Model                             | Simon Brown           | Hierarchical architecture diagramming (Context, Container, Component, Code)                      |
| Domain-Driven Design                 | Eric Evans            | Bounded contexts, ubiquitous language, strategic/tactical patterns                               |

### Engineer

| Standard/Framework | Source                                   | Coverage                                                                   |
| ------------------ | ---------------------------------------- | -------------------------------------------------------------------------- |
| SWEBOK v4          | IEEE Computer Society / ISO/IEC TR 19759 | 18 knowledge areas covering full SE lifecycle                              |
| SFIA v9            | SFIA Foundation                          | 120+ professional skills at 7 responsibility levels                        |
| DORA Metrics       | Google/DORA Research                     | Deployment frequency, lead time, MTTR, change failure rate                 |
| SPACE Framework    | Microsoft Research / GitHub              | Satisfaction, Performance, Activity, Communication, Efficiency             |
| DX Core 4          | Abi Noda et al.                          | Developer experience measurement (speed, ease, quality, impact)            |
| IEEE 730-2014      | IEEE                                     | Software quality assurance processes                                       |
| ISO/IEC 25010:2023 | ISO                                      | Software product quality model (8 characteristics, 31 sub-characteristics) |

### Product Manager

| Standard/Framework    | Source                    | Coverage                                                  |
| --------------------- | ------------------------- | --------------------------------------------------------- |
| AIPMM PmBoK           | AIPMM                     | Product management body of knowledge, CPM certification   |
| ISPMA SPMBoK          | ISPMA                     | Software product management body of knowledge             |
| PDMA NPDP             | PDMA                      | New product development professional certification        |
| Lean Product Playbook | Dan Olsen                 | Product-market fit pyramid, hypothesis-driven development |
| Continuous Discovery  | Teresa Torres             | Opportunity solution trees, weekly customer touchpoints   |
| Dual-Track Agile      | Jeff Patton / Marty Cagan | Discovery + delivery running in parallel                  |
| HEART Framework       | Google                    | Happiness, Engagement, Adoption, Retention, Task Success  |

### Tech Lead

| Standard/Framework             | Source                | Coverage                                                        |
| ------------------------------ | --------------------- | --------------------------------------------------------------- |
| SFIA v9 — Levels 5-6           | SFIA Foundation       | Ensure, advise — team leadership and technical authority        |
| DORA / Accelerate              | Forsgren, Humble, Kim | 24 capabilities that drive software delivery performance        |
| Team Topologies                | Skelton & Pais        | Stream-aligned, enabling, complicated-subsystem, platform teams |
| Westrum Organizational Culture | Ron Westrum / DORA    | Pathological → bureaucratic → generative culture model          |
| Staff Engineer Archetypes      | Will Larson           | Tech lead, architect, solver, right hand                        |
| The Manager's Path             | Camille Fournier      | Tech lead → engineering manager progression                     |
| Radical Candor                 | Kim Scott             | Care personally + challenge directly feedback model             |

### Security

| Standard/Framework               | Source                       | Coverage                                            |
| -------------------------------- | ---------------------------- | --------------------------------------------------- |
| NIST Cybersecurity Framework 2.0 | NIST                         | Govern, Identify, Protect, Detect, Respond, Recover |
| OWASP Top 10 (2021)              | OWASP Foundation             | Most critical web application security risks        |
| OWASP SAMM v2                    | OWASP Foundation             | Software assurance maturity model (prescriptive)    |
| BSIMM14                          | Synopsys/Black Duck          | Building security in maturity model (observational) |
| NIST SP 800-218 (SSDF)           | NIST                         | Secure software development framework               |
| MITRE ATT&CK v15                 | MITRE Corporation            | Adversary tactics, techniques, and procedures       |
| ISO/IEC 27001:2022               | ISO                          | Information security management system              |
| CIS Controls v8.1                | Center for Internet Security | Prioritized security safeguards                     |
| SWEBOK v4 — Software Security KA | IEEE Computer Society        | New in v4: security as first-class knowledge area   |

### Designer

| Standard/Framework                           | Source            | Coverage                                          |
| -------------------------------------------- | ----------------- | ------------------------------------------------- |
| Nielsen Norman Group Heuristics              | Jakob Nielsen     | 10 usability heuristics (empirically derived)     |
| WCAG 2.2 / 3.0                               | W3C               | Web content accessibility guidelines              |
| ISO 9241-210:2019                            | ISO               | Human-centred design for interactive systems      |
| Design Council Double Diamond                | UK Design Council | Diverge/converge discovery and delivery model     |
| IDEO Human-Centered Design                   | IDEO.org          | Inspiration, ideation, implementation             |
| Atomic Design                                | Brad Frost        | Atoms → molecules → organisms → templates → pages |
| Material Design / Human Interface Guidelines | Google / Apple    | Platform-specific design systems                  |

### QA Engineer

| Standard/Framework                | Source       | Coverage                                                       |
| --------------------------------- | ------------ | -------------------------------------------------------------- |
| ISTQB Foundation & Advanced       | ISTQB        | Test design techniques, test process, test management          |
| ISO/IEC 25010:2023                | ISO          | Software product quality model (8 characteristics)             |
| ISO/IEC/IEEE 29119                | ISO          | Software testing standard (concepts, processes, documentation) |
| IEEE 829-2008                     | IEEE         | Test documentation standard                                    |
| WCAG 2.2                          | W3C          | Accessibility testing criteria                                 |
| Google HEART Framework            | Google       | Metrics for user experience quality measurement                |
| James Bach's Heuristic Testing    | Satisfice    | Context-driven testing, exploratory testing sessions           |
| Michael Bolton's Testing Sapience | DevelopSense | Critical thinking in testing, testing vs. checking distinction |

### SDLC Cross-Role

| Standard/Framework | Source                | Coverage                                           |
| ------------------ | --------------------- | -------------------------------------------------- |
| ISO/IEC 12207:2017 | ISO                   | Software lifecycle processes                       |
| ISO/IEC 15288:2023 | ISO                   | System lifecycle processes                         |
| CMMI v2.0          | ISACA                 | Capability maturity model for process improvement  |
| SAFe 6.0           | Scaled Agile          | Scaled agile framework for large organizations     |
| DORA / Accelerate  | Forsgren, Humble, Kim | Four key metrics for software delivery performance |

## LLM Error Mitigation Strategy

Every skill includes an **Anti-Patterns** section specifically targeting documented LLM failure modes:

### Common LLM Failure Categories

| Category                   | Example                                                             | Mitigation in Skills                                                            |
| -------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Hallucinated specifics** | Citing nonexistent standards, inventing API endpoints               | Skills require verification against authoritative sources                       |
| **Over-generalization**    | "Use microservices" without analyzing actual constraints            | Skills require constraint gathering before solution proposal                    |
| **Cargo-culting**          | Recommending patterns because they're popular, not because they fit | Anti-patterns explicitly call out "applying X without understanding trade-offs" |
| **Constraint blindness**   | Ignoring team size, budget, timeline, compliance requirements       | Instructions mandate context gathering as step 1                                |
| **Happy-path bias**        | Focusing on success cases, ignoring error states and edge cases     | Skills explicitly require edge case and failure mode analysis                   |
| **Solution bias**          | Jumping to implementation before understanding the problem          | Instructions enforce problem framing before solution design                     |
| **Recency bias**           | Favoring the newest technology regardless of fitness                | Skills reference technology radar methodology for balanced evaluation           |
| **Abstraction addiction**  | Creating unnecessary layers, interfaces, and indirection            | Anti-patterns flag premature abstraction and YAGNI violations                   |

## Empirical References

Key research underpinning the skills:

- **Accelerate** (Forsgren, Humble, Kim, 2018) — Statistical proof that DORA capabilities predict org performance
- **DORA State of DevOps Reports** (2014-2025) — Annual empirical research on software delivery and operational performance
- **KoCo-Bench** (2026) — Domain-specific LLM evaluation benchmark for software development
- **SPACE Framework** (Forsgren et al., 2021) — Microsoft Research paper on developer productivity measurement
- **Measuring Developer Productivity** (DX Core 4, 2024) — Evidence-based developer experience metrics
- **The Mythical Man-Month** (Brooks, 1975/1995) — Foundational work on software project management and complexity
- **A Philosophy of Software Design** (Ousterhout, 2018) — Empirical approach to complexity reduction
- **Thinking, Fast and Slow** (Kahneman, 2011) — Cognitive bias research applicable to all decision-making skills
