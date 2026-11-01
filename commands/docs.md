---
description: Generate developer and user documentation for a feature
argument-hint: <feature name>
allowed-tools: Read, Glob, Grep, Write, Bash(mkdir:*), Bash(git log:*), Bash(git check-ignore:*)
---

<!--
Setup: replace every <PLACEHOLDER>. Consider renaming to <project-name>-docs.md
to avoid clashing with built-in commands. Delete this comment when done.
-->

# Document Feature

Generate two documentation files for the feature: $ARGUMENTS

## Process
1. If $ARGUMENTS is empty, stop and ask which feature to document.
2. Read CLAUDE.md, then locate the feature's code with Glob and Grep (<SOURCE_DIRS>). If you cannot identify the relevant files with confidence, list your candidates and ask before writing anything.
3. Classify the feature, and state the classification with the files it is based on:
   - UI-only: mostly <UI_DIR>
   - Logic-only: mostly <BUSINESS_LOGIC_DIR> and <STATE_DIR>, no direct user interaction
   - Full-stack: both UI and logic layers
   For a logic-only feature, skip the user guide and explain why.
4. Run `git log --oneline` on the relevant files to understand how the feature evolved.
5. Search <DOCS_DIR> and README.md for related documentation. If docs already exist, follow their structure and tone, and link to the related ones.
6. Create <DOCS_DIR>/dev/ and <DOCS_DIR>/user/ if they don't exist.

## Output 1: <DOCS_DIR>/dev/<feature-slug>-implementation.md
- Overview: what the feature does and why (2-3 sentences)
- Classification and the files involved, with the role of each
- Data flow, from user action to result
- Public API: exported functions, hooks and components with their signatures
- Data impact: does it read or write <PERSISTED_DATA_SHAPES_AND_KEYS>?
- How to extend it safely
- Known limitations
- A link to the user guide

## Output 2: <DOCS_DIR>/user/how-to-<user-task>.md
Written for a non-technical user: no code, no file names, plain English.
- What you can do with this feature, in one sentence
- Numbered steps, one action per step
- At most 5 screenshot placeholders in total, one per key moment (not one per step), placed after the step where that moment occurs. Name each by what it shows, not by step number: `![short description](../images/<feature-slug>-<what-it-shows>.png)`
- Tips and common questions (3 maximum)
- A "For developers" footer linking to the developer documentation

## Rules
- Document only what the code actually does. Never describe a behaviour you have not found in the code; if something is unclear, add a "To verify" note.
- Use kebab-case for all file names.
- Do not modify any source file.
- Never reference git-ignored or local-only files (such as <REPORTS_DIR>) in the generated docs. Check with `git check-ignore` if unsure.
- If README.md is out of date for this feature, mention it in the final summary but do not edit it.
- At the end, list the files created, the classification, and every screenshot to capture.
