---
trigger: model_decision
description: Applied when creating Git commit messages. Format rules for Conventional Commits-based Prefix + English summary + bulleted body
---

# Git Commit Message Format Rules

This rule is a guideline for commit messages that applies to all commits.

## Position of This Rule

- This rule is a commit message convention based on Conventional Commits.
- While adhering to basic formats like `Prefix` and `BREAKING CHANGE` from Conventional Commits, it adds guidelines specific to this repository such as `language` specification and bulleted body.
- When reusing in other projects, adjust `language` and the list of Prefixes according to each project's policy.

## Language Specification

- In this rule file, `language` is used as a logical name representing the language used in commit messages.
- `language = "en"`
- Summary and body should be written in the language specified by `language` as a rule.

## Basic Format (Required)

```
<Prefix>: <Summary (imperative/concise)>

- Change 1 (bullet point)
- Change 2 (bullet point)
- ...

Refs: #<Issue number> (optional)
BREAKING CHANGE: <content> (optional)
```

## Prefix (Leading Prefix)

Prefix corresponds to `type` in Conventional Commits and uses lowercase English words.

- feat: Add new feature
- fix: Bug fix
- refactor: Refactoring (no behavior change)
- perf: Performance improvement
- test: Add/modify tests
- docs: Documentation update
- build: Build/dependency changes
- ci: CI-related changes
- chore: Miscellaneous tasks (tool settings/scripts, etc.)
- style: Style-only changes (unrelated to code logic)
- revert: Revert

As with Conventional Commits, the format `<Prefix>(scope):` is also allowed as needed (e.g., `fix(translation): ...`).
- For detailed specifications, also refer to the official [Conventional Commits](https://www.conventionalcommits.org/) documentation.

## Summary (First Line)

- Write concisely in the language specified by `language`. No period at the end.
- Briefly express what and why (if necessary).
- Aim for approximately 50 characters or less.

## Principles for Message Generation

- Commit messages must always be generated from uncommitted diffs (e.g., `git diff` / `git diff --cached`) after reviewing their content.
- Do not guess from issue titles or branch names alone; summarize and enumerate the actual changes contained in the diff.
- Even for automatic generation by AI or scripts, use uncommitted diffs as input.
- When bots or automation tools commit, follow this rule and always generate messages based on diffs.

## Body (Bullet Points)

- List changes as bullet points starting with "- ".
- Write in the same language as the summary (the `language` defined in this rule file) as a rule. Technical terms in English are acceptable as needed.
- If possible, also add bullet points for "impact scope," "migration steps," "risks," "rollback method," etc.

## Footer (Optional)

- Refs/Closes: Specify related Issues or PRs with `Refs: #123` / `Closes: #123`.
- BREAKING CHANGE: If there are backward-incompatible changes, clearly state the content (or use the `!` notation with Prefix like `fix!: ...`).

## Examples

```
fix: Remove unnecessary debug log output

- Remove verbose log lines from user info retrieval process
- Reduce log volume while keeping necessary information

Refs: #123
```

```
refactor: Consolidate duplicate validation logic into common function

- Extract duplicate form input check code to utility function
- Remove duplicate logic from callers to improve readability
- No behavior changes
```

## Prohibited

- Writing summary only in a language different from that specified by `language`
- Ambiguous summaries that don't convey meaning (e.g., abstract expressions like "update", "fix bug")
- Body with only long text without bullet points that makes content hard to grasp
- Commits that only disable or bypass static analysis or checks without substantial improvement (e.g., configuration changes that only relax check rules)
