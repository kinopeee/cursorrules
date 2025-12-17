# CHANGELOG

🇬🇧 English

[🌏 Back to Top](../README.md) | [🇯🇵 日本語](../ja/CHANGELOG.md)

This file records the update history of the cursorrules v5 project.

## Version 4.4 (2025-12-17)

### Highlights

#### 1. Rule file format migration (Cursor 2.2+ compatible)

- Migrated from `.mdc` format to new folder-based format (`rule-name/RULE.md`)
- Aligned with Cursor 2.2+ recommended format for improved readability and maintainability
- Each rule is now managed as a folder, enabling future addition of scripts and resources

#### 2. Updated document and command reference paths

- Updated rule references in README (root/ja/en) to new format
- Updated reference paths in workflow commands (`.cursor/commands/*.md`)
- Updated references in operational guides (`doc/rules-and-workflows.md`, `doc/prompt-injection-guard.md`)
- Updated file format descriptions in translation guide (`TRANSLATION_GUIDE.md`)

#### 3. Migrated rule files

The following rules have been migrated to the new format:

| Old format | New format |
|------------|------------|
| `v5.mdc` | `v5/RULE.md` |
| `commit-message-format.mdc` | `commit-message-format/RULE.md` |
| `pr-message-format.mdc` | `pr-message-format/RULE.md` |
| `test-strategy.mdc` | `test-strategy/RULE.md` |
| `prompt-injection-guard.mdc` | `prompt-injection-guard/RULE.md` |

#### 4. v5 coding support rule improvements

- **Standalone usage**: Removed dependency on workspace common rules, enabling independent use
- **Abstracted tool names**: Changed from specific tool names (`read_file`, `apply_patch`, etc.) to abstract operation types (`read/search`, `apply diff`), making the rule applicable across different environments
- **Clarified task judgment**: Added "when in doubt, treat as 🟡 standard task"
- **Simplified rule priority**: Explicitly stated the principle of "prioritize more specific/restrictive clauses" in case of conflicts
- **Improved section structure**: Changed from "Task classification and reasoning depth" to "Task classification and standard flow", integrating execution flows

## Version 4.3 (2025-11-29)

### Highlights

#### 1. Multi-language directory structure reorganization

- Reorganized into language-specific directories (`ja/` and `en/`)
- Unified documentation reference paths with language prefixes
- Improved maintainability and clarity of multi-language support

#### 2. Added external context injection defense feature

- Added new `prompt-injection-guard.mdc` rule file
- Added context-based detection and judgment criteria
- Provides defense against instruction execution from external file references
- Added operational guide documentation (`doc/prompt-injection-guard.md`)

#### 3. Refreshed README

- Renewed design with multi-language support
- Added Quick Start section for easy onboarding
- Simplified file list section for better readability

#### 4. Added Opus 4.5 notation

- Added references to Anthropic's Opus 4.5 model alongside GPT-5.1

## Version 4.2 (2025-11-17)

### Highlights

#### 1. Added commit/push/PR rules and custom command

- Added operational rules for commit messages, pushing, and PR creation
- Added a custom workflow command to streamline the commit/push/PR flow

#### 2. Separated rules and workflows and added documentation

- Separated rule definitions and workflow (custom command) definitions and organized them
- Added documentation explaining best practices for rules and workflows (doc/rules-and-workflows.md)

## Version 4.1 (2025-11-15)

### Highlights

#### 1. Added test strategy rules

- Added new test strategy rules (test-strategy.mdc/en.mdc)
- Mandated test perspective tables (equivalence partitioning and boundary value analysis)
- Standardized Given/When/Then comment format
- Clear verification requirements for exceptions, error messages, and error codes
- Explicit execution commands and coverage reporting
- Added mock usage guidelines and operational notes in both Japanese and English

#### 2. Major refactoring of v5 coding support rules

- Reduced verbosity and improved conciseness (509 lines removed, 425 lines added)
- Clarified task classification (🟢 Lightweight/🟡 Standard/🔴 Critical) and reasoning depth
- Reorganized tool usage policy (read_file/apply_patch/grep/parallel execution, etc.)
- Restructured standard flows (lightweight/standard/critical tasks) and output style
- Unified error, type, and security policies with a code-centric focus

#### 3. Unified model-neutral language

- Removed references to specific model names (GPT-5.1)
- Unified to adaptive reasoning expressions as generic AI assistant rules
- Improved future maintainability and generality

#### 4. Removed specific tool references

- Removed descriptions of Terraform/Pulumi/Snyk/AWS MCP tools
- Eliminated references to specific tools for better generality
- Unified under static analysis tools section

#### 5. Documentation updates

- Added references to test strategy rules in README (English and Japanese)
- Documented language-specific rule file saving procedures and test policy application

## Version 4 (2025-11-15)

### Highlights

#### 1. GPT-5.1 optimization

- Introduced a prompt layer that maximizes GPT-5.1 inference accuracy
- Refined instruction priority parsing to catch contradictions earlier
- Improved response stability with throttle controls tuned for GPT-5.1 constraints

## Version 3 (2025-08-30)

### Highlights

#### 1. Introduced adaptive process selection

- Classify tasks into three levels: Lightweight, Standard, and Critical
- Optimize execution process according to each level
- Use a simplified process for lightweight tasks and phased execution for critical tasks

#### 2. Optimized parallel execution

- Introduced guidelines for parallel execution of independent tasks
- Optimized execution order based on dependencies
- Improved overall processing speed

#### 3. Tiered error handling

- Four levels: Warning, Error, Critical, Security
- Implemented automated responses appropriate to each level
- Prevented infinite loops in error handling

#### 4. Improved progress tracking

- Checklist-style execution plan for standard and critical tasks
- Visual progress indicators (✅⏳⬜) for long-running work
- Simplified reporting rules for lightweight tasks with concise 1–2 sentence summaries instead of fixed-interval updates

#### 5. Strengthened quality management

- Introduced a stepwise verification process
- Improved handling of linter errors
- Enhanced type safety

#### 6. GPT-5 optimization

- Prompt design to maximize GPT-5 capabilities
- Execute more instructions without contradictions
- Improved adherence to custom instructions

#### 7. Simplified documentation structure

- Removed detailed examples of technology stacks
- Removed directory structure examples
- Focused the document on the update history

#### 8. Slash command conventions

- Added explicit rules for treating `/`-prefixed inputs as executable commands
- Clarified that the assistant should not modify command files
- Ensured only explicitly provided arguments are passed to slash commands, leaving other parameters to command defaults

## Version 2 (2024-03-02)

### Highlights

#### 1. Project Rules support

- Fully compatible with the Project Rules format introduced in Cursor 0.45
- Migration from the legacy `.cursorrules` format to Project Rules
- Manage rules within the `.cursor/rules` directory

#### 2. Optimized for Claude 3.7 Sonnet

- Prompt design to maximize the capabilities of Claude 3.7 Sonnet

## Previous versions

For older updates, please refer to the repository history.
