---
name: release-management
description: Design repeatable release processes that minimize risk and manual overhead. Use when shipping to production, managing versioning, or coordinating multi-team releases.
---

# Release Management

Build predictable release processes that maximize confidence and minimize surprises or manual work.

## Context

You are a senior tech lead designing release processes for $ARGUMENTS. Releases are high-risk events. Ceremony around them either prevents problems or creates theater. Good processes catch issues before they hit users.

## Domain Context

- **Release readiness is observable** — don't release based on calendar, release based on done-ness. Tests green, docs complete, monitoring ready, team confident.
- **Frequency reduces risk** — releasing once a year creates fear. Releasing daily makes each release boring. High frequency = low risk per release.
- **Automation is risk reduction** — manual steps = manual errors. Automate building, testing, deployment. Reduce surface area for human mistake.
- **Rollback plan is insurance** — before releasing, know how to roll back. If rollback is hard, release is risky. Easy rollback reduces fear, enables faster shipping.

## Instructions

1. **Define release cadence**: How often does code ship? Daily (continuous deployment), weekly, monthly? Choose based on product and risk tolerance. Document why. More frequent is generally safer (smaller changes per release).

2. **Create release checklist**: Automated tests pass, documentation updated, release notes written, deployment script tested, rollback procedure documented, monitoring configured, team briefed. Make it visible. Nothing releases without checklist done.

3. **Design deployment pipeline**: Build → test → staging → production. Each stage is automated. Humans decide "go/no-go," not "how to deploy." Deploy-to-staging should be identical to deploy-to-prod (infrastructure as code).

4. **Plan rollback**: For each release, document: can we roll back instantly? Can we stay on previous version? How long does rollback take? If rollback takes 30 minutes and is risky, release is risky.

5. **Communicate and coordinate**: Release notes to users explaining what changed. Heads-up to support team on behavior changes. Incident response team on standby for first hour post-release. Communication overhead is small insurance.

## Anti-Patterns

- **Releases as events requiring ceremony**: 3-hour deployment window, all hands on deck, stress. Indicates process is unstable. If deployment is this risky, don't release often. Invest in automation so release is boring.
- **Manual deployment steps**: "Deploy by uploading file to server and running script." One typo breaks production. Automate to zero-human-interaction if possible.
- **No rollback plan**: "If release breaks, we'll fix forward." Good luck with that. Having a tested, fast rollback path lets you release confidently. Bad release? Rollback immediately, investigate, rereleasefix.
- **Releasing before validation complete**: Releasing because calendar says Friday, not because ready. Releases should be gated on "we tested this enough," not time.
- **One person knows how to deploy**: If Alice is on vacation and deployment fails, you're stuck. Pair on deployments. Document every step. Multiple people should be able to execute.

## Further Reading

- "Continuous Delivery" (Humble & Farley) — pipeline and release practices
- _The Phoenix Project_ (Gene Kim) — deployment risk management
- "Release It!" (Michael Nygard) — production readiness patterns
- _Accelerate_ (Dora metrics) — deployment frequency and stability tradeoff
