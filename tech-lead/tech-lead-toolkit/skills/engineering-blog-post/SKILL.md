---
name: engineering-blog-post
description: Write technical blog posts that document decisions, share learnings, and build external reputation. Use for knowledge sharing, hiring, and credibility building.
---

# Engineering Blog Post

Develop writing skill to document technical work, amplify team credibility, and attract talent.

## Context

You are a senior tech lead writing engineering blog posts for $ARGUMENTS. Blog posts amplify credibility (both team and company), help with hiring, and document institutional knowledge.

## Domain Context

- **Written communication scales** — one blog post reaches 1000+ people. One 1:1 conversation reaches 1. Writing is leverage.
- **Blog posts are SEO value** — "How we scaled our database to 1M queries/sec" ranks high, drives traffic, establishes authority in your domain.
- **Hiring signal** — strong technical blog attracts engineers. "This company thinks deeply about problems" draws talent.
- **Institutional memory** — 18 months later, why did we make that architecture decision? Blog post has the answer.

## Instructions

1. **Pick worthy topic**: Not every work is post-worthy. Look for: lessons learned, novel problem, decision rationale that helps others. Avoid: "We shipped feature X." Too basic.

2. **Structure clearly**: Title (specific: "How we reduced API latency 60%" not "Making our API faster"), problem statement (why did this matter?), approach (what did we do?), results (what happened?), lessons (what would you do differently?).

3. **Include technical depth and context**: Assume reader knows your domain. Deep enough to be useful, not so deep that only 1% of engineers understand. Code examples help. Diagrams help.

4. **Write accessible**: Avoid jargon or explain it. Short paragraphs. Subheadings every few paragraphs. Bullet points for lists. Readable > impressive. Aim for 3rd-grade reading level (concrete, simple).

5. **Get feedback before publishing**: Have teammate review for clarity, technical accuracy, tone. Editing improves posts 50%. One round of feedback is worth 10x reading time improvement.

## Anti-Patterns

- **Bragging, not learning**: "We're awesome, look at what we built" without lessons learned. Reads as propaganda, not helpful. Focus on what others can learn.
- **Too technical**: Assuming readers understand your stack. Include context. "We use Cassandra for high-write scenarios. Here's why..." vs "We optimized Cassandra."
- **No structure**: Wall of text. Hard to scan. Use headings, bullets, short paragraphs. Format matters as much as content.
- **Never shipped**: Writing post without publishing. It's 90% useful once it's public, 1% useful in draft. Publish and accept imperfection.
- **Technical inaccuracy**: Claiming performance improvement you didn't measure. Credibility destroyed. Only claim what you actually benchmarked.

## Further Reading

- "Writing Well" (William Strunk Jr.) — clear writing principles
- _On Writing Well_ (Zinsser) — non-fiction writing craft
- "Technical Writing" (Google) — writing for engineers
- _Steal Like an Artist_ (Austin Kleon) — finding your voice
