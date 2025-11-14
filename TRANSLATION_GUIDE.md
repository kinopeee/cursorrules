 # Custom Instructions Translation Guide

## Purpose
Provide a practical template to translate custom instructions into other languages so that models can understand and comply with them, while producing natural, idiomatic target-language text.

## Scope
- Source to translate: `./.cursor/rules/v5.en.mdc` (English version of cursor custom instructions)
- This guide provides a template to translate it into any target language while preserving functionality
- The source file includes task classification, error-handling tiers, and slash command conventions; translations must preserve their operational meaning.
- Placement of translated output: place the translated file in `./.cursor/rules/` (adjust file name as needed, e.g., `v5.ja.mdc`)

## Recommended Prompt Template

````text
You are a bilingual technical translator and editorial optimizer.

Goal:
- Translate the following "custom instructions" into the target language so that:
  1) The model reading them can fully understand and follow them as operational rules
  2) The text feels natural and idiomatic in the target language, while strictly preserving the original intent, constraints, structure, and enforceability

Input:
- Source language: English (for v5.en.mdc)
- Target language: Specify your target language and regional variant (e.g., Spanish (ES), German (DE), Portuguese (BR))
- Formality/Tone: FORMAL (prefer clarity and imperative voice for rules)
- Style guidance: none
- Glossary/Terminology to enforce: none
- Do-not-translate items (keep verbatim):
  - Code blocks
  - Inline code `like_this`
  - File/dir names
  - Functions/classes
  - CLI commands
  - URLs
  - Variables/placeholders (e.g., {{instructions}}, {placeholders})
  - Markdown anchor IDs / link targets (e.g., #custom-instructions)
  - Config keys
  - JSON/YAML keys
  - Identifiers
  - Brand names
  - Issue/PR numbers
  - Commit prefixes
- Original text: paste the full content of `./.cursor/rules/v5.en.mdc` between triple backticks:

```
[PASTE v5.en.mdc CONTENT HERE]
```

Strict requirements:
- Preserve:
  - Section hierarchy, headings, numbering, and bullet structure
  - Code fences, inline code, and technical formatting (backticks, parentheses, brackets). Do not change code-fence language tags (e.g., ```ts, ```bash)
  - Whitespace and indentation, including front matter and code blocks (do not change width or style)
  - Variables/placeholders (e.g., {{var}}, {var}), anchors, and link targets (localize only visible anchor text if needed)
  - Commit message prefixes, command flags, config keys, and file paths
  - Structural markers and metadata specific to `v5.en.mdc` (e.g., front matter separators `---`, keys like `alwaysApply:`, or tags)
  - Also preserve/do not translate: special markers (BREAKING CHANGE/Refs/Closes), file paths and extensions, and technical identifiers (API/function/config names)
- Optimize for target-language clarity:
  - Use imperative forms for rules/guidelines where natural
  - Normalize awkward literal phrasing into native, concise expressions without changing meaning
  - Resolve minor ambiguity via phrasing; if non-trivial, flag clearly in Notes
- Do not add new rules, remove constraints, or soften requirements
- Do not explain the translation process or include hidden reasoning

Quality checklist (internal; reflect results succinctly in Notes):
- Semantics and constraints preserved
- Role and responsibility wording preserved
- Structure (headings/lists/code) intact
- Terminology consistent
- Non-translatable items unchanged
- Numbers, examples, and references accurate

Output format:
1) Final translation only (complete, ready to use), preserving markdown/format
2) Notes (bullet list, brief). If none, write: Notes: none
````

## Usage Tips

1. **Before translating**: Read through `v5.en.mdc` to understand its structure and technical requirements
2. **Target language**: Specify any target language and regional variant (e.g., Spanish (ES), German (DE), Portuguese (BR))
3. **Glossary**: Build a consistent terminology mapping for technical terms used throughout the instructions
4. **Testing**: After translation, verify the translated instructions work correctly in Cursor by placing them in `./.cursor/rules/`



### Key Items to Preserve
- Commit prefixes: `feat:`, `fix:`, `docs:`, `chore:`, etc.
- Special markers: `BREAKING CHANGE`, `Refs:`, `Closes:`
- File paths and extensions: `.mdc`, `.cursor/rules/`
- Technical identifiers: API names, function names, configuration keys