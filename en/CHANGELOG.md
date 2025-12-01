# CHANGELOG

🇬🇧 English

[🌏 Back to Top](../README.md) | [🇯🇵 日本語](../ja/CHANGELOG.md)

This file records the update history of the Windsurf / Antigravity Rules v5 project.

> **Note**: This repository is a port of [cursorrules](https://github.com/kinopeee/cursorrules) for Windsurf and Antigravity.

## Version 4.4 (2025-12-02)

### Highlights

#### 1. Windsurf / Antigravity Support

- Ported from [cursorrules](https://github.com/kinopeee/cursorrules) for Windsurf / Antigravity
- Added Windsurf rules (`.windsurf/rules/`) and workflows (`.windsurf/workflows/`)
- Added Antigravity rules (`.agent/rules/`) and workflows (`.agent/workflows/`)
- Added Antigravity-specific `planning-mode-guard.md` rule

#### 2. Documentation Generalization

- Updated Cursor-specific paths (`.cursor/rules/*.mdc`) for Windsurf / Antigravity
- Changed file extensions from `.mdc` to `.md`
- Changed `alwaysApply: true` to `trigger: always_on`
- Replaced Cursor-specific tool names (`read_file`, `apply_patch`, `run_terminal_cmd`) with generic expressions

#### 3. README Updates

- Completely revised root README for Windsurf / Antigravity
- Added links to related repository (cursorrules)
- Separated Quick Start section by Windsurf / Antigravity

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

## Version 2 (2025-03-01)

### Highlights

#### 1. Enhanced Control for Claude 3.7 Sonnet

- Prevented Claude 3.7 Sonnet from performing operations not explicitly instructed
- Optimized to execute only actions that follow explicit instructions

#### 2. File Operation Efficiency

- Reduced unnecessary segmentation of file read/write operations
- Improved ability to comprehend larger contexts in a single operation

#### 3. Optimization for Claude 3.7 Sonnet

- Adjusted instruction formats to leverage Claude 3.7 Sonnet's capabilities
- Enhanced efficiency in dialogue and processing

### Detailed Changes

- Improved file reading to process larger sections at once
- Reduced chains of unnecessary tool calls for more efficient processing flows
- Optimized instruction formats to maximize Claude 3.7 Sonnet's understanding and reasoning abilities
- Strengthened controls to prevent additional processing without explicit instructions

## Version 1 (Initial Release)

- Initial version of custom instructions (`.windsurfrules`) for Windsurf
- Optimized adaptation of [cursorrules](https://github.com/kinopeee/cursorrules) for Windsurf Cascade
- Included descriptions of basic tech stacks, API version management, and project structures
- Provided two configuration types: v1 (simplified version) and v5 (customizable version)
