---
description: Think before coding - write a decision-ready plan for a feature, with no code
argument-hint: <feature description>
allowed-tools: Read, Glob, Grep, Write, Bash(git log:*), Bash(git status:*), Bash(git checkout:*), Bash(git add:*), Bash(git commit:*)
---

<!--
Setup: rename to <project-name>-plan.md. Replace <PLANS_DIR> (e.g. docs/plans).
Delete this comment when done.
-->

# Plan a feature

Write an implementation plan for: $ARGUMENTS

Do not write or change any code. The plan is the deliverable.

## Process
1. If $ARGUMENTS is empty or too vague to plan, ask me one question and stop.
2. Read CLAUDE.md, then the code the feature depends on. Quote the facts you rely on with file:line.
3. Check the feature against the boundaries in CLAUDE.md before designing it:
   - Does it need data the project does not store, or a change to a core data shape? Say so at the top: it needs my approval.
   - Does it need a new dependency? Name it, its size and why the existing stack is not enough.
4. Compare 2 or 3 approaches in a short table (complexity, files touched, risk to existing data, explainability). Recommend the simplest one that works.
5. For every open question, propose a default answer. Leave a question open only if it is a real trade-off I must decide.

## Output: <PLANS_DIR>/<feature-slug>.md (150 lines maximum)
- Goal (2 sentences) and the CLAUDE.md constraints that apply
- Decisions: each with its default answer, marked "proposed" until I confirm
- v1 scope: In / Out
- Implementation order: numbered steps, each with the files created or changed
- Files that must not change
- Risks and edge cases
- How we will know it works; mark any target "unverified" if no real data exists to measure it
- Later: what is deferred, and the condition that would bring it back

Commit the plan on a new docs branch. Do not merge.

## Final message
Summarise the recommendation in 3 lines, list the decisions I must confirm, and state what you checked in the code versus assumed.
