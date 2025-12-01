---
description: Batch flow to commit, push changes, and create a Pull Request
---

# Commit, Push & Create PR

Commits changes, pushes to remote, and then creates a Pull Request.

## Prerequisites

- Changed files exist
- Remote `origin` is configured
- GitHub CLI (`gh`) is installed (for fallback)
- On a working branch (feature/*, fix/*, etc.)

## Execution Steps (Non-Interactive)

1. Branch check (prevent direct push to main/master)
2. Run quality checks as needed (lint / test / build, etc.)
3. Stage changes (`git add -A`)
4. Commit (use message from argument or environment variable)
5. Push (`git push -u origin <current-branch>`)
6. Create PR (using MCP, CLI, or other method appropriate for the environment)

## Usage

### A) Execute with Minimal Information (Recommended)

Pattern where you specify only the commit message and let AI (via MCP, etc.) handle PR title and body.

```bash
# Specify commit message only (example)
MSG="fix: Remove unnecessary debug log output"

# Batch execution
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

# AI creates PR here (example)
# - Infer purpose from branch name
# - Check changed files with git diff --name-status
# - Auto-generate PR title and message
# - Create PR with mcp_github_create_pull_request / gh pr create, etc.
```

> Note: MCP (Model Context Protocol) is a standard protocol for agents to safely operate external services like GitHub. This procedure uses MCP's GitHub integration for PR creation. MCP-compatible environment setup is required. Reference: <https://modelcontextprotocol.io/>

### B) Manually Specify PR Title and Message

```bash
# Variable setup
MSG="fix: Remove unnecessary debug log output"
PR_TITLE="fix: Remove unnecessary debug log output"
PR_BODY=$(cat <<'PRBODY'
## Overview
This PR removes unnecessary debug logs and reduces log output volume.

## Changes
- Remove verbose debug log output
- Keep only necessary log levels and messages

## Technical Details
- Impact scope is limited to log output only; no changes to business logic

## Test Content
- Manually verified presence/absence of log output and behavior

## Related Issues
Refs #123
PRBODY
)
# Note: <<'PRBODY' (with quotes) disables variable expansion inside heredoc.
# Use <<PRBODY (without quotes) if you want to include variables in PR body.

# Batch execution
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ Direct push to main/master is prohibited"; exit 1; \
fi

# Optional quality checks (if needed)
# ./scripts/quality-check.sh || exit 1

git add -A && \
git commit -m "$MSG" && \
git push -u origin "$BRANCH" && \
gh pr create --title "$PR_TITLE" --body "$PR_BODY" --base main
```

### C) Step Execution (For Debugging)

```bash
# 1) Branch check
BRANCH=$(git branch --show-current)
echo "Current branch: $BRANCH"
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ Direct push to main/master is prohibited"; exit 1;
fi

# 2) Check changed files
echo "Changed files:"
git status --short

# 3) Optional local quality checks (add as needed)
# Example:
# echo "Running quality checks..."
# ./scripts/lint.sh && ./scripts/test.sh && ./scripts/build.sh || exit 1

# 4) Stage changes
git add -A
echo "Staging complete"

# 5) Commit
MSG="fix: Remove unnecessary debug log output"
git commit -m "$MSG"
echo "Commit complete"

# 6) Push
git push -u origin "$BRANCH"
echo "Push complete"

# 7) Create PR (request from AI or CLI)
# After this, use AI or gh command to create PR:
# - Branch name: $BRANCH
# - Diff: git diff main...HEAD --name-status
# - Commit history: git log main..HEAD --oneline
```

## Information Sources for PR Auto-Generation

Information used when AI creates PR:

```bash
# Get branch name (used to infer purpose)
git branch --show-current

# Get diff with base
git merge-base origin/main HEAD

# List of changed files
git diff --name-status $(git merge-base origin/main HEAD)...HEAD

# Change statistics (as needed)
git diff --stat $(git merge-base origin/main HEAD)...HEAD

# Commit history
git log origin/main..HEAD --oneline
```

> **Note on branch references:** The above commands use `origin/main` (remote branch) to compare with the latest remote state. The `main` argument in `gh pr create --base main` refers to the target branch name on the remote repository. Both approaches are correct usage in their respective contexts.

## PR Title and Message Rules

- Follow the detailed format for PR titles and bodies in `.agent/rules/pr-message-format.md`.
- This command assumes PR messages are written in the structured format defined in that rule (Overview / Changes / Test Content, etc.).

## Notes

- Follow the commit message format and message generation principles in `.agent/rules/commit-message-format.md`.
- Recommended to run `git status` or `git diff` to review diffs before execution.

## Troubleshooting

### If Push Succeeds but PR Creation Fails

```bash
# Manually create PR only
gh pr create --title "Title" --body "Message" --base main

# Or create via web browser
# Open the Pull Requests page of the target repository on GitHub and create PR from the UI.
```

### Inferring Prefix from Branch Name

| Branch Prefix | Prefix   |
| ------------- | -------- |
| feature/      | feat     |
| fix/          | fix      |
| refactor/     | refactor |
| perf/         | perf     |
| test/         | test     |
| docs/         | docs     |
| build/        | build    |
| ci/           | ci       |
| chore/        | chore    |

## Execution Example

```bash
# Example 1: Minimal specification (AI auto-generates)
MSG="fix: Remove unnecessary debug log output"
BRANCH=$(git branch --show-current)
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ Direct push to main/master is prohibited"; exit 1;
fi

# Optional quality checks (if needed)
# ./scripts/quality-check.sh || exit 1

git add -A && git commit -m "$MSG" && git push -u origin "$BRANCH"

# After this, request AI:
# "Please create a PR for branch $BRANCH.
#  Generate appropriate title and message from branch name and diff."
```

## Related Documentation

- Commit message rules: `.agent/rules/commit-message-format.md`
- PR message rules (optional): `.agent/rules/pr-message-format.md`
- Development flow: Project-specific README / CONTRIBUTING / development guides, etc.
