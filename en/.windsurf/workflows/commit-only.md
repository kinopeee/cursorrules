---
description: Commit local changes to the current branch only (no push)
executionMode: safe
---

# Commit Only (Current Branch)

Commits local changes only. Does not push or create PR.

## Prerequisites

- Changed files exist
- Follow the commit message conventions defined in `.windsurf/rules/commit-message-format.md`

## Execution Steps (Non-Interactive)

1. Review uncommitted diffs and consider commit message content (e.g., `git diff` or `git diff --cached`)
2. Stage changes (`git add -A`)
3. Commit (pass message via environment variable or argument)

### A) Safe Batch Execution (Message Argument Version)

```bash
MSG="<Prefix>: <Summary (imperative/concise)>" \
git add -A && \
git commit -m "$MSG"
```

Example:

```bash
MSG="fix: Remove unnecessary debug log output" \
git add -A && \
git commit -m "$MSG"
```

### B) Step Execution (Readability Focused)

```bash
# 1) Review diffs
git status
git diff

# 2) Stage changes
git add -A

# 3) Commit (edit message)
git commit -m "<Prefix>: <Summary (imperative/concise)>"
```

## Notes

- Follow the commit message format and message generation principles in `.windsurf/rules/commit-message-format.md`.
- Branch strategy (e.g., no direct commits to main, working branch workflow) and pushing to remote (`git push`) are outside the scope of this command. Define them in project-specific README / CONTRIBUTING / separate commands as needed.

