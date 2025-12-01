---
description: Commit changes to the current branch and push to remote
---

# Commit & Push (Current Branch)

Commits changes and pushes to remote. Direct push to main/master is prohibited.

## Prerequisites

- Changed files exist
- Remote `origin` is configured

## Execution Steps (Non-Interactive)

1. Branch check (prevent direct push to main/master)
2. Run quality checks as needed (lint / test / build, etc.)
3. Stage changes (`git add -A`)
4. Commit (use message from argument or environment variable)
5. Push (`git push -u origin <current-branch>`)

## Usage

### A) Safe Batch Execution (Message Argument Version)

```bash
MSG="<Prefix>: <Summary (imperative/concise)>" \
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ Direct push to main/master is prohibited"; exit 1; \
fi

# Optional quality checks (if needed)
# Example:
# ./scripts/lint.sh && ./scripts/test.sh && ./scripts/build.sh || exit 1

git add -A && \
git commit -m "$MSG" && \
git push -u origin "$BRANCH"
```

Example:

```bash
MSG="fix: Remove unnecessary debug log output" \
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ Direct push to main/master is prohibited"; exit 1; \
fi

# Optional quality checks (if needed)
# ./scripts/quality-check.sh || exit 1

git add -A && git commit -m "$MSG" && git push -u origin "$BRANCH"
```

### B) Step Execution (Readability Focused)

```bash
# 1) Branch check
BRANCH=$(git branch --show-current)
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ Direct push to main/master is prohibited"; exit 1;
fi

# 2) Optional local quality checks (add as needed)
# Example:
# echo "Running quality checks..."
# ./scripts/lint.sh && ./scripts/test.sh && ./scripts/build.sh || exit 1

# 3) Stage changes
git add -A

# 4) Commit (edit message)
git commit -m "<Prefix>: <Summary (imperative/concise)>"

# 5) Push
git push -u origin "$BRANCH"
```

## Notes

- Follow the commit message format and message generation principles in `.agent/rules/commit-message-format.md`.
- Recommended to run `git status` or `git diff` to review diffs before execution.
