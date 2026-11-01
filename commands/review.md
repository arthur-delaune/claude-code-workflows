---
description: Review files against <PROJECT_NAME> conventions and save a report
argument-hint: <file path(s)>
allowed-tools: Read, Glob, Grep, Write, Bash(<LINT_COMMAND>:*)
---

<!--
Setup: rename this file to <project-name>-review.md (e.g. acme-review.md) so it is
invoked as /acme-review. Do not name it code-review: the built-in command takes precedence.
Replace every <PLACEHOLDER>. Delete this comment when done.
-->

# Code Review

Review $ARGUMENTS against this project's conventions. Do not modify any source file.

## Reference files
Read these first; they define our patterns:
- CLAUDE.md (project rules)
- <REFERENCE_COMPONENT> (UI component pattern)
- <REFERENCE_STATE_MODULE> (state and persistence pattern)
- <REFERENCE_BUSINESS_LOGIC_FILE> (pure business logic pattern)
- <REFERENCE_SHARED_HELPER> (e.g. formatting, validation)
- <REFERENCE_TYPES_FILE> (core data shapes)

## Process
1. If $ARGUMENTS is empty or a path does not exist, stop and ask which file to review.
2. Read the reference files, then each file in $ARGUMENTS.
3. Run the linter on the reviewed files only, not the whole project: `<LINT_COMMAND> <path>` for each file. Note any warnings.
4. Assess each file against the checklist below.

## Checklist
### Correctness
Check this section first: conventions can be perfect while the code still fails at runtime.
- State initialisation and effects (flicker on first render, stale state on reopen)
- Async flows: errors attributed to the right step, races when the component unmounts or closes
- Disabled states match what is actually possible (e.g. no progressing with zero records)
- <ADD_DOMAIN_SPECIFIC_CORRECTNESS_CHECKS>

### Conventions
- Respects the layer separation defined in CLAUDE.md (<BUSINESS_LOGIC_DIR> / <UI_DIR> / <STATE_DIR>)
- Type safety: no `any`, no unsafe casts (adapt to your language)
- Shared helpers used instead of hand-rolled logic (<REFERENCE_SHARED_HELPER>)
- Styling follows the project's design system (<STYLING_RULES>)
- Accessibility: labels, roles, keyboard support
- Error handling and empty states
- No magic numbers or duplicated logic
- No risk to persisted data (<PERSISTED_DATA_SHAPES_AND_KEYS>)

## Output
Create <REPORTS_DIR> if it does not exist. Save one report per file to <REPORTS_DIR>/<path-name>.review.md, where <path-name> is the full path from the repo root without extension, with "/" replaced by "-" (e.g. `src/components/Modal.tsx` becomes `src-components-Modal.review.md`). Each report contains:
- Overall rating: Excellent / Good / Needs Improvement / Poor
- Issues ranked by severity (High / Medium / Low), each with file:line and a concrete fix
- What is done well (3 points maximum)
- Estimated refactoring effort: Low / Medium / High
- **Verified / not verified**: what you actually checked (lint run, code paths read, behaviour traced) and what you did not (runtime behaviour, tests, browser checks). Never imply a check you did not perform.

Then give a 5-line summary in the chat. Do not commit the reports.
