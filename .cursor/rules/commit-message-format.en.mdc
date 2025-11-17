---
alwaysApply: true
description: Git commit message format rules (Prefix + summary + bullet list)
---

# Git Commit Message Format Rules

This rule defines the commit message guidelines that apply to all commits.

## Role of this rule

- This rule is a commit message convention based on Conventional Commits.
- While `Prefix` and `BREAKING CHANGE` follow the Conventional Commits specification, it adds repository-specific guidelines such as `language`-based language selection and bullet-list bodies.
- When reusing this rule in other projects, adjust `language` and the list of prefixes according to each project's policy.

## Language

- In this file, `language` is a logical name that represents the language used in commit messages.
- `language = "en"`
- The summary and body should, in principle, be written in the language specified by `language`.

## Basic format (required)

```
<Prefix>: <summary (imperative / concise)>

- Change item 1 (bullet)
- Change item 2 (bullet)
- ...

Refs: #<issue-number> (optional)
BREAKING CHANGE: <description> (optional)
```

## Prefix

`Prefix` corresponds to the `type` in Conventional Commits and should be a lowercase English word.

- feat: new feature
- fix: bug fix
- refactor: refactoring (no behavior change)
- perf: performance improvement
- test: tests added/updated
- docs: documentation updates
- build: build/dependency changes
- ci: CI-related changes
- chore: chores (tools, scripts, etc.)
- style: style-only changes (no logic impact)
- revert: revert a previous change

As in Conventional Commits, you may optionally use the `<Prefix>(scope):` form when needed (e.g. `fix(translation): ...`).
For details, see the [Conventional Commits](https://www.conventionalcommits.org/) specification.

## Summary (first line)

- Write a concise summary in the language specified by `language`; do not add a trailing period.
- Briefly express what was changed and, if needed, why.
- Aim for about 50 characters in the summary line.

## Message generation principles

- Always inspect the uncommitted diff (`git diff` / `git diff --cached` etc.) and generate the summary and body based on those changes.
- Do not rely only on issue titles or branch names; summarize the actual changes present in the diff.
- When AI or scripts generate commit messages, they should also use the uncommitted diff as input.
- Bots and automation tools must follow this rule and generate messages based on the diff as well.

## Body (bullet list)

- List changes as bullet points starting with `- `.
- The body should be written in the same language as the summary (`language`), but technical terms can be in English as needed.
- When possible, also include items such as impact scope, migration steps, risks, and rollback procedures.

## Footer (optional)

- Refs/Closes: Explicitly reference related Issues or PRs using `Refs: #123` / `Closes: #123`.
- BREAKING CHANGE: When making backward-incompatible changes, describe them here (you may also use `fix!: ...` with `!` on the prefix).

## Examples

```
fix: remove unnecessary debug log output

- Remove redundant log lines from user information fetch processing
- Reduce log volume while keeping necessary information

Refs: #123
```

```
refactor: extract duplicated validation logic into common function

- Extract duplicate form input validation code into a utility function
- Remove duplicated logic at call sites to improve readability
- No behavioral changes
```

## Prohibited patterns

- Writing the summary only in a different language than specified by `language` (for example, a non-English summary while `language = "en"`).
- Vague summaries that do not convey meaning (e.g. "update", "fix bug").
- Long bodies without bullet lists that are hard to understand.
- Commits that only weaken static analysis or checks without real improvements (e.g. loosening rules without justification).

