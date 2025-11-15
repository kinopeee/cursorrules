# cursorrules "v5"

English | [日本語](README.md)

This repository manages custom instructions for Cursor.

## Premise

- This `v5` is a set of custom instructions optimized for the Cursor Agent.
- For the Cursor Agent to operate autonomously (without human intervention), Auto-Run must be configured appropriately.
- See the [changelog](CHANGELOG.en.md) for the latest updates.

## Overview

- After the release of Cursor's agent features, I noticed a recurring issue: insufficient analytical rigor. I began crafting custom instructions to better draw out the model's inherent analytical ability (originally Claude 3.5 Sonnet at the time).
- The early themes were improving analytical capability and autonomous execution. Later iterations also targeted preventing duplicate module/resource generation, unintended design changes by the AI, and infinite loops in error handling. These efforts, combined with model refreshes and performance gains, have produced reasonable results.
- The focus of this version upgrade is GPT-5.1 optimization:
    1. We create a checklist-style execution plan first, then verify completion item-by-item for a more disciplined process.
    1. Tasks are classified into Lightweight, Standard, and Critical levels, with simplified reporting for lightweight tasks and more thorough processes for heavier ones.
    1. Independent tasks are executed in parallel to improve throughput.
- In addition, this version defines explicit slash command conventions (treating `/`-prefixed input as commands, not modifying command files, and passing only explicitly provided arguments) so that Cursor Agent can safely execute local commands.
- `v5` was initially created with Anthropic Prompt Generator and has since gone through cycles of evaluation by contemporary models and practical improvements. When customizing, we recommend having your chosen AI evaluate it as well.

- For detailed updates, including task classification, error handling tiers, and slash command conventions, see [CHANGELOG.en.md](CHANGELOG.en.md).

## Usage

1. If `.cursor/rules` does not exist yet, create the folder.
2. If the path exists, save `v5.mdc` (Japanese) and/or `v5.en.mdc` (English) there.
3. If you also want to enforce the test strategy rules, save `test-strategy.mdc` (Japanese) and/or `test-strategy.en.mdc` (English) under the same `.cursor/rules` folder.
- Because their application condition is "always", they will be referenced in subsequent chats as long as they exist at the designated path.
- Both Japanese and English versions are set to `alwaysApply: true`, so you may want to adjust this setting based on your preferred language and whether you want the test rules enabled by default.

## Translation Guide

For the recommended prompt to translate custom instructions into other languages, see [TRANSLATION_GUIDE.md](TRANSLATION_GUIDE.md).

## Notes

- If there are instructions in User Rules or Memories that conflict with v5, the model may become confused and effectiveness may decrease. Please check the contents carefully.

## License

Released under the MIT License. See [LICENSE](LICENSE) for details.

## Support

- There is no official support for this repository, but feedback is welcome. I also share Cursor-related information on X (Twitter).
[Follow on X (Twitter)](https://x.com/kinopee_ai)
