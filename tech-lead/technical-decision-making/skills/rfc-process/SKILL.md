---
name: rfc-process
description: Structure Request for Comments processes to document major technical decisions, surface concerns, and build consensus. Use before implementing significant architectural changes.
---

# RFC Process

Create lightweight but rigorous decision-making processes that surface hidden risks, build buy-in, and create institutional memory.

## Context

You are a senior tech lead designing an RFC process for $ARGUMENTS. Undocumented decisions lead to duplicated work, missed tradeoffs, and tribal knowledge. RFCs create accountability and institutional memory.

## Domain Context

- **RFC culture (Rust community)** — formal but lightweight comment period before major decisions. Prevents surprises and catches edge cases.
- **Decision fatigue** — too many decisions become invisible. Filtering to truly significant ones preserves decision quality.
- **Async-first architecture** — RFCs work best when decisions can happen in writing, with comment periods. Real-time consensus building doesn't scale.
- **Tradeoff documentation** — why we chose X over Y matters more than the choice itself. Future engineers inherit the context.

## Instructions

1. **Define RFC scope**: Major architectural changes, new external dependencies, significant protocol changes, infrastructure decisions. Not: minor refactors, bugfixes, local optimizations. Typical threshold: affects 2+ teams or 2+ quarters of work.

2. **Create template**: Title, Summary (1 paragraph), Motivation (why change?), Proposal (what's the change?), Alternatives considered (with tradeoffs), Implementation plan, Risks & mitigation. Keep to 2-5 pages. Longer RFCs get fewer reads.

3. **Set comment period**: 1-2 weeks for visibility and async feedback. Synchronous decisions create FOMO and exclude people in other timezones. Async allows careful thought.

4. **Facilitate discussion**: Respond to every comment. Resolve concerns or explicitly document "we heard this and chose to accept the risk." Don't dismiss feedback; explain reasoning. Show you're taking concerns seriously.

5. **Document decision**: Once approved, record: decision made, date, key concerns that were raised, how they were addressed. This context is gold when debugging decisions 18 months later.

## Anti-Patterns

- **RFCs as rubber stamps**: Proposing change, ignoring feedback, implementing anyway. Kills credibility. If you're not genuinely open to feedback, don't do an RFC.
- **RFCs for everything**: Every decision becomes a 2-week async discussion. Teams move slowly, decision fatigue drops. Use RFCs for genuinely significant decisions only. Minor decisions should be fast.
- **No implementation follow-up**: RFC approved, then actual implementation diverges. Document delta. Why did implementation differ from proposal? Update decision record.
- **Tribal review groups**: Only senior engineers read and comment on RFCs. Juniors don't see reasoning or participate. Make RFCs visible and explicitly welcome questions.
- **Ignoring edge cases raised**: Someone comments "What about X scenario?" and you brush past it. Document the edge case and decision to handle it later, or change proposal. Don't dismiss.

## Further Reading

- Rust RFC process (github.com/rust-lang/rfcs) — reference implementation
- _Thinking, Fast and Slow_ (Kahneman) — decision quality and documentation
- "Write 5, Read 1000" (Lara Hogan) — asynchronous decision making at scale
- _Decisive_ (Chip Heath) — documenting alternatives prevents reversible/irreversible confusion
