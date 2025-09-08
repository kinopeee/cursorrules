# cursorrules "v5"

This repository manages custom instructions for Cursor.

## Premise

- This `v5` is a set of custom instructions optimized for the Cursor Agent.
- For the Cursor Agent to operate autonomously (without human intervention), Auto-Run must be configured appropriately.
- See the [changelog](CHANGELOG.en.md) for the latest updates.

## Overview

- After the release of Cursor's agent features, I noticed a recurring issue: insufficient analytical rigor. I began crafting custom instructions to better draw out the model's inherent analytical ability (originally Claude 3.5 Sonnet at the time).
- The early themes were improving analytical capability and autonomous execution. Later iterations also targeted preventing duplicate module/resource generation, unintended design changes by the AI, and infinite loops in error handling. These efforts, combined with model refreshes and performance gains, have produced reasonable results.
- The focus of this version upgrade is GPT-5 optimization:
    1. GPT-5 sometimes omits explanations until a task is complete, so this version ensures planning before starting and short explanations before tool calls.
    1. We create a checklist-style execution plan first, then verify completion item-by-item for a more disciplined process.
    1. For light tasks, the process is simplified to avoid overhead; for heavier tasks, a more thorough process is used.
    1. Independent tasks are executed in parallel to improve throughput.
- `v5` was initially created with Anthropic Prompt Generator and has since gone through cycles of evaluation by contemporary models and practical improvements. When customizing, we recommend having your chosen AI evaluate it as well.

- For detailed updates, see [CHANGELOG.en.md](CHANGELOG.en.md).

## Usage

1. If `.cursor/rules` does not exist yet, create the folder.
2. If the path exists, save `v5.mdc` there.
- Because its application condition is "always", it will be referenced in subsequent chats as long as it exists at the designated path.
- An English version `v5.en.mdc` is also provided. It ships with `alwaysApply: false` to avoid double application; enable it as needed in your environment.

## Notes

- If there are instructions in User Rules or Memories that conflict with v5, the model may become confused and effectiveness may decrease. Please check the contents carefully.

## License

Released under the MIT License. See [LICENSE](LICENSE) for details.

## Support

- There is no official support for this repository, but feedback is welcome. I also share Cursor-related information on X (Twitter).
[Follow on X (Twitter)](https://x.com/kinopee_ai)
