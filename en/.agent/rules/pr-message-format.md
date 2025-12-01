---
trigger: model_decision
description: Applied when creating Pull Requests. Format rules for Prefix + English summary + structured body (overview, changes, test content)
---

# PR Message Format Rules

This rule is a guideline that applies to Pull Request (PR) titles and bodies.

## Position of This Rule

- This rule defines the PR message format in a way that aligns with the commit message convention based on Conventional Commits (`commit-message-format.md`).
- While recommending the same style for title `Prefix` and summary as commit messages, it requires structured descriptions in the PR body such as "Overview," "Changes," and "Test Content."
- When reusing in other projects, adjust `language` and required sections (e.g., "Technical Details") according to each project's policy.

## Language Specification

- In this rule file, `language` is used as a logical name representing the language used in PR messages.
- `language = "en"`
- Title and body should be written in the language specified by `language` as a rule.

## Title (First Line)

### Format (Required)

```
<Prefix>: <Summary (imperative/concise)>
```

- `Prefix` is recommended to use `type` from Conventional Commits, same as commit messages (e.g., `feat`, `fix`, `refactor`, `docs`, `chore`, etc.).
- Write concisely in the language specified by `language`. No period at the end.
- Briefly express what and why (if necessary), aiming for approximately 50 characters or less.

## Body (Structured Format)

### Recommended Template

PR body is recommended to have the following structured sections.

```markdown
## Overview

Summary of what was implemented/fixed in this PR

## Changes

- Description of change 1
- Description of change 2
- Description of change 3

## Technical Details (Optional)

- Implementation details and design intentions as needed

## Test Content

- Types of tests performed (unit tests, E2E tests, manual verification, etc.)
- Results of main behavior verification

## Related Issues

- Closes #123
- Refs #456
```

- "Overview" and "Changes" are required in principle; "Technical Details," "Test Content," and "Related Issues" may be made required according to project operation rules.
- Write bullet points with enough granularity to understand "what," "where," and "why" changes were made.

## Principles for Message Generation

- PR title and body must always be generated from **actual diffs and commit history** (e.g., `git diff`, `git log`) after reviewing their content.
- Do not guess from issue titles or branch names alone; clearly state change content, impact scope, and test content in the body.
- Even for automatic generation by AI or scripts, use diffs, commit history, and related Issue information as input.
- Determine Prefix and summary to align with the commit message convention (`commit-message-format.md`) (avoid semantic inconsistency between commits and PR).

## Prohibited

- Writing title or body only in a language different from that specified by `language`
- Ambiguous titles that don't convey meaning (e.g., abstract expressions like "update", "fix issue", "changes")
- Body with only unstructured long text (without section headings or bullet points, making content hard to grasp)
- Descriptions that differ from actual diffs or intentionally omit important changes, impacts, or test results
