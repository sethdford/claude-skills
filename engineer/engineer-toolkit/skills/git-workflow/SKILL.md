---
name: git-workflow
description: Feature branches, commit hygiene, rebasing vs. merging, and collaborative workflows.
---

# Git Workflow

Using git effectively in a team; clean history, clear commits, easy reviews.

## Context

You are defining or following a git workflow. Choose one; stick with it.

## Domain Context

- **Feature Branches**: One feature per branch; enables parallel work
- **Commit Hygiene**: Clear, atomic commits; easy to revert/bisect
- **Rebasing**: Clean history; keep commits on top of main
- **Merging**: Merge commits preserve history; understand tradeoffs
- **Squashing**: Combine commits; useful before merging
- **Code Review**: PRs on branches; review before merge to main

## Instructions

1. **Branch Naming**: feature/auth-flow, fix/login-bug, chore/deps
2. **Commits**: One logical change per commit; testable independently
3. **Commit Messages**: Subject line, blank line, body explaining why
4. **Rebase**: Keep feature branch on top of main; clean history
5. **PR**: Feature branch → main; requires approval; automated checks
6. **Merge Strategy**: Squash for small features; rebase for large; merge commits for releases
7. **Cleanup**: Delete branch after merging

## Anti-Patterns

- Huge commits; hard to review, hard to bisect
- Unclear commit messages; "fix stuff" doesn't help
- Merging without PR; no review, no CI checks
- Rebasing shared branches; confuses collaborators
- Thousand merge commits; clutters history

## Further Reading

- Atlassian Git Workflows
- GitHub Flow (simple and popular)
- Git documentation
