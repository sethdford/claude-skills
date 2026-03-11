# Code Review Leadership Plugin

Establish comprehensive code review practices that balance quality, speed, and team health.

## Skills

This plugin includes 8 skills for building effective code review culture and infrastructure:

### Standards & Culture

- **code-review-standards** — Define acceptance criteria, approval roles, and escalation paths
- **review-culture-guide** — Build a culture where feedback improves code and team relationships
- **constructive-feedback** — Teach reviewers to give feedback that improves code without harming trust

### Practical Tools

- **review-checklist-design** — Create domain-specific review checklists that surface defects without creating busywork
- **merge-strategy** — Choose merge strategies (squash, rebase, commit) that match your workflow
- **quality-gate-definition** — Define automated gates (coverage, linting, security) that block before manual review

### Infrastructure & Measurement

- **automated-review-setup** — Configure CI/CD tooling, linters, and security scanners
- **review-metrics** — Track cycle time, participation diversity, and defect escape to measure and improve review health

## Commands

Chain skills to build complete review infrastructure:

- **define-standards** — Create comprehensive code review standards document with checklists and merge strategy
- **setup-quality-gates** — Configure automated tooling and gates with clear thresholds
- **review-metrics** — Establish metrics dashboard and health measurement process

## Key Principles

1. **Automate what's obvious**: Linting, formatting, security scans should be automated. Humans review design and logic
2. **Lead time matters most**: Optimize for fast reviews (< 24h) before optimizing for depth
3. **Culture beats process**: Clear standards help, but a culture of trust and learning drives better outcomes
4. **Measurement without action is waste**: If you measure metrics, act on them when they trend wrong
5. **Feedback is a gift, not a burden**: Frame code review as mutual improvement, not gatekeeping

## How to Use

Each skill includes:

- Domain context grounded in research (Forsgren, Edmondson, McKinsey studies)
- Step-by-step instructions for creating artifacts (checklists, gates, culture norms)
- **Anti-Patterns section**: common mistakes (tool overload, culture without systems, metrics without action)
- Further reading from authoritative sources

Commands chain skills and suggest follow-up actions.

## Author

Seth Ford

## License

MIT
