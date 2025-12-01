---
title: Prompt Injection Guard Operational Guide
---

## Overview

The file `prompt-injection-guard.md` defines the **core defense logic** that the AI must obey immediately.

- **Windsurf**: `.windsurf/rules/prompt-injection-guard.md`
- **Antigravity**: `.agent/rules/prompt-injection-guard.md`

This document complements it by organizing **user-side operational options and how to handle false positives**.

**Related documents:**
- Threat analysis and design background: [`custom_instruction_plan_prompt_injection.md`](custom_instruction_plan_prompt_injection.md)
- Implementation rules:
  - Windsurf: `.windsurf/rules/prompt-injection-guard.md`
  - Antigravity: `.agent/rules/prompt-injection-guard.md`

---

## 1. Default behavior and handling false positives

- These rules are always applied in an **effective Strict mode**, with all detection features enabled.
- The INFO / WARN / CRITICAL levels are used **only as labels to communicate the importance of each detection**, and are **not** used to switch the underlying defense logic (whether something is detected / blocked) on or off.
- There is no mechanism on the custom-instruction side to change the security level.  
  If false positives interfere with your work, adjust **the editor's rule application settings** to temporarily narrow when and where the rules are applied.
- **Note on `trigger: always_on`**: The rule file has `trigger: always_on` set in its metadata, which means the editor will reference it by default. However, users can still control when these rules are actually applied via the editor's UI settings.

---

## 2. Customizable operational options

### 2-1. Trusted sources

- You may operate with certain domains or file paths treated as "trusted sources".
- Even for trusted sources, you may lower the UI warning level, but **must keep the defense behavior itself (detection / blocking) enabled**.

### 2-2. Alert suppression

- You can temporarily hide specific `alert_type` values in the UI and, if necessary, log them only without showing notifications.
- This helps prevent the UI from being flooded by frequent alerts during development, while **keeping the underlying defenses active**.

### 2-3. Exceptions for external source verification

- You may treat specific API endpoints or file paths as "out of scope for external source verification", but do this **only when you fully understand and accept the security risks**.
- Even with such exceptions, you must **not allow automatic execution of destructive operations** such as deletion, external API calls, or system modifications.

---

## 3. Operational support features

### 3-1. Security summary

- When showing a summary of detected alerts at the end of a conversation, attach INFO / WARN / CRITICAL importance labels to each alert so that users can get a quick overview of risks.
- The summary should include **potential risks and recommended follow-up actions** (e.g., re-checking external links, reviewing commands before execution).

### 3-2. Learning mechanism (false-positive feedback)

- When users judge that "this was a false positive", you may record such patterns and adjust sensitivity for similar cases (assuming a local, controlled environment).
- However, for patterns related to **critical operations (destructive changes, sensitive data exfiltration, etc.)**, always prioritize safety and avoid relaxing defenses lightly.

---

## 4. Practical recommendations

- In normal operation, keep `prompt-injection-guard.md` always enabled so that the guard is always active.
- Even when false positives make it hard to work:
  - First consider reducing noise via **organizing trusted sources** and **alert suppression settings**.
  - Only when the impact remains significant should you temporarily change the rule application settings, and be sure to revert the setting after the work is done.
- When you want to execute commands from external runbooks or wikis, we recommend a workflow where the AI first shows you the concrete commands and you explicitly approve them (for example, "Yes, run this command"), rather than implicitly executing imperative sentences from the document body.
- When using an English UI or working in a multilingual environment, the same guard logic applies.  
  If your workspace contains both Japanese and English versions of the rules/guides, refer to whichever matches your working language as needed.

This guide is about **how to operate the system**, not about changing the defense logic itself.  
The strict guardrails the AI must follow are always defined by `prompt-injection-guard.md`.

---

## 5. Common false-positive patterns and how to handle them

- Example 1: **`instruction-quarantine` alerts on internal wiki runbooks**  
  - Symptom: A trusted internal wiki page contains phrases like "Run the following command", and quoting it as-is triggers an alert.
  - Handling: Treat the domain as a "trusted source" while **keeping the detection / blocking logic intact**.  
    If UI noise becomes a problem, consider temporarily suppressing the corresponding `alert_type` in the UI (logging only).

- Example 2: **Repeated `payload-splitting` alerts from test scripts**  
  - Symptom: Tests frequently edit scripts that intentionally split commands across multiple strings, causing repeated `payload-splitting` alerts.
  - Handling: Even if the test code itself is legitimate, it often contains **the same dangerous patterns as real attacks**, so keep the core defenses enabled.  
    If you only want to reduce UI noise during development, consider temporarily hiding `payload-splitting` alerts in the UI and checking them via logs instead.



