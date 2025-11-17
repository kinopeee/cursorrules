# Commit & push (current branch)

## Overview

This is a generic command template for committing changes on the current branch and pushing them to the remote.  
Branch policies (such as disallowing direct pushes to main/master) and pre-commit quality checks (lint / test / build, etc.) should be adjusted per project.

## Preconditions

- There are modified files.
- The remote `origin` is configured.

## Steps (non-interactive)

1. Check the current branch and prevent direct pushes to main/master.
2. Optionally run quality checks (lint / test / build, etc.).
3. Stage changes (`git add -A`).
4. Commit (using an environment variable or argument for the message).
5. Push (`git push -u origin <current-branch>`).

## Usage

### A) Safe one-liner execution (with message argument)

```bash
MSG="<Prefix>: <summary (imperative / concise)>" \
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ Direct pushes to main/master are not allowed"; exit 1; \
fi

# Optional quality checks (only if needed)
# Example:
# ./scripts/lint.sh && ./scripts/test.sh && ./scripts/build.sh || exit 1

git add -A && \
git commit -m "$MSG" && \
git push -u origin "$BRANCH"
```

Example:

```bash
MSG="fix: remove unnecessary debug log output" \
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ Direct pushes to main/master are not allowed"; exit 1; \
fi

# Optional quality checks (only if needed)
# ./scripts/quality-check.sh || exit 1

git add -A && git commit -m "$MSG" && git push -u origin "$BRANCH"
```

### B) Step-by-step execution (readability first)

```bash
# 1) Check branch
BRANCH=$(git branch --show-current)
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ Direct pushes to main/master are not allowed"; exit 1;
fi

# 2) Optional local quality checks (add as needed)
# Example:
# echo "Running quality checks..."
# ./scripts/lint.sh && ./scripts/test.sh && ./scripts/build.sh || exit 1

# 3) Stage changes
git add -A

# 4) Commit (edit the message)
git commit -m "<Prefix>: <summary (imperative / concise)>"

# 5) Push
git push -u origin "$BRANCH"
```

## Notes

- Commit message formatting and generation principles should follow `.cursor/rules/commit-message-format.en.mdc` (or another language-specific rule file).
- Always review diffs with `git status` or `git diff` before executing this command.


