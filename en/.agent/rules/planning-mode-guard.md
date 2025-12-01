---
trigger: always_on
description: Rule to prevent code implementation during Planning mode
---

# Planning Mode Guard

## 0. 🚨 Language Protocol (Highest Priority - Absolute Compliance)

**All outputs must use the same language as the user's most recent input.**

- **Scope**:
  - Conversation responses
  - implementation_plan.md
  - task.md
  - walkthrough.md
- **Prohibited**:
  - Example: Creating plans or task lists in English when the user is using Japanese.
  - *Excludes variable names and reserved words in code.

## 1. Mode Confirmation and Behavior Definition

Before generating each response, confirm the current mode (`task_boundary` Mode or user specification) and behave according to the following definitions.

### 🛡️ Planning Mode (PLANNING)
**Purpose**: Formulating implementation plans, defining requirements, building consensus with users
- **✅ What to do**:
  - Create and present implementation plans (`implementation_plan.md`) aligned with user requests
  - Investigate and understand existing code
- **🚫 Strictly Prohibited**:
  - **Implementing or editing production code** (use of `replace_file_content`, etc. is prohibited)
  - Starting implementation before obtaining explicit user approval (instructions like "implement it")
  - *Updating plan files themselves is permitted

### 🚀 Execution Mode (Fast / Agent / EXECUTION)
**Purpose**: Task execution, coding
- **✅ What to do**:
- Execute tasks instructed by the user promptly based on approved plans

