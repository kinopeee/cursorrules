# CHANGELOG

This file records the update history of the cursorrules v5 project.

## Version 3 (2024-08-30)

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

- Checklist-style execution plan
- Visual progress indicators (✅⏳⬜)
- 30-minute periodic progress checks

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
