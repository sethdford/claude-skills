# Contributing

Contributions welcome — whether it's a bug fix, a typo, or a new skill idea.

## How to Contribute

- **Bugs and small fixes** — open a PR directly.
- **New skills, commands, or larger changes** — open an issue first so we can discuss the approach.

## Guidelines

- Keep PRs focused — one change per PR.
- Follow existing patterns: **skills are nouns** (domain knowledge), **commands are verbs** (workflows).
- Every skill needs frontmatter with `name` and `description`.
- Every command needs `description` and `argument-hint`.
- Skill name must match its directory name.
- No cross-plugin references in commands.
- Suggest follow-ups in natural language only.

## Quality Requirements

Every skill MUST include:

1. **Domain Context** section citing real frameworks, standards, or academic sources
2. **Instructions** section with 4-6 concrete steps producing a deliverable
3. **Anti-Patterns** section with 2-4 LLM-specific failure modes to guard against
4. **Further Reading** section with real, verifiable references

### Anti-Patterns Standard

The Anti-Patterns section is what differentiates this collection. Each entry must:

- Name a specific LLM failure mode (not a general software anti-pattern)
- Explain _why_ LLMs make this mistake (training data bias, lack of context, etc.)
- Provide a concrete guard (what to check, verify, or ask before accepting output)

Good example:

> **Recommending microservices without assessing team size** — LLMs default to distributed architectures because they appear frequently in training data. Guard: confirm the team has 20+ engineers and independent deployment needs before suggesting service decomposition.

Bad example:

> **Don't over-engineer** — too vague, not LLM-specific.

## Standards Alignment

New skills should reference at least one recognized standard from [STANDARDS.md](./STANDARDS.md). If your skill introduces a new domain, add the relevant standard to the mapping.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
