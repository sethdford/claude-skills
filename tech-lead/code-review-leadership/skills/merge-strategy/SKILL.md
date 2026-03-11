---
name: merge-strategy
description: Define merge strategies (squash, rebase, merge commits) that balance history clarity with practical workflow. Use when setting CI/CD merge policies.
---

# Merge Strategy

Choose and document merge strategies that work for your team's workflow and history preferences.

## Context

You are helping a tech lead decide on merge strategy for a repository. If you have insights into the team's workflow (frequent hotfixes, long-lived feature branches, monorepo), use them.

## Domain Context

- Git workflow philosophies vary (GitHub Flow, Git Flow, trunk-based development) each with different merge strategies
- Research (Forsgren et al.): high-performing teams use strategies that enable fast feedback loops
- History readability matters: blame, bisect, and log mining all depend on clean history

Key principles:

1. **Match strategy to workflow**: GitHub Flow (fast, short-lived branches) uses squash; Git Flow (long-lived releases) uses merge commits
2. **Commits are both history and workflow**: Commit messages serve future readers (blame, changelog); granular commits help with bisect and cherry-pick
3. **Automate the policy**: Enforce strategy in CI/CD, don't rely on developer discipline

## Instructions

1. **Assess team workflow**: Are branches short-lived (< 1 day) or long-lived (weeks)? Do you cherry-pick or do full releases?
2. **Choose strategy**:
   - **Squash**: Simplifies history, good for short-lived feature branches, makes blame harder
   - **Rebase**: Linear history, good for learning flow, harder to track original branch context
   - **Merge commit**: Preserves branch history, good for long-lived releases, adds merge commit noise
3. **Document in CONTRIBUTING.md**: Explain why you chose this strategy
4. **Enforce in CI/CD**: Disable manual merges. Only allow via automated CI job that applies strategy
5. **Set commit message standards**: Define what goes in messages (linked issues, breaking changes, etc.)
6. **Consider exceptions**: Hotfixes might use different strategy than feature branches. Document criteria

Example strategies by workflow:

- GitHub Flow (main + short feature branches): Squash merges, auto-generate release notes from PR titles
- Git Flow (main, develop, release branches): Merge commits, preserve branch context for releases
- Trunk-based (frequent commits to main): Rebase or squash, fast CI feedback, rapid releases

## Anti-Patterns

- **Strategy mismatched to workflow**: LLMs sometimes recommend squash merges for long-lived branches, which loses important context. Match strategy to team reality
- **Enforced history without team buy-in**: Teams that don't understand merge strategy will bypass it or complain constantly. Explain the why and solicit feedback
- **No exceptions documented**: Edge cases (hotfixes, emergency patches) often need different strategies. Document when exceptions apply
- **Merge strategy as a learning opportunity lost**: Each merge is a chance to clean up history. LLMs sometimes treat it as an automated step. Have humans review merge commits

## Further Reading

- Driessen, Vincent. "A Successful Git Branching Model." (Git Flow) 2010.
- GitHub's "GitHub Flow" guide: practical guide to short-lived branches.
- Fowler, Martin. "Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation." Addison-Wesley, 2010.
