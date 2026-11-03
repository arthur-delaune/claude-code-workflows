---
description: Turn a sketch, screenshot or whiteboard photo into a screen, after confirming how to read it
argument-hint: <image path> [notes]
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git checkout:*), Bash(git add:*), Bash(git commit:*), Bash(<LINT_COMMAND>:*), Bash(<BUILD_COMMAND>:*)
---

<!--
Setup: rename to <project-name>-from-mockup.md. Replace <LINT_COMMAND>, <BUILD_COMMAND>,
<SHARED_COMPONENTS> and <MOCKUPS_DIR>. Delete this comment when done.
-->

# Build from a mockup

Implement the screen shown in: $ARGUMENTS

A mockup is intent, not a specification. Work in two phases and stop between them.

## Phase 1: read the mockup (no code)
1. If no image path is given or the file does not exist, ask me for it and stop.
2. Describe what you see, element by element, top to bottom, including handwritten notes and arrows.
3. Classify each element:
   - Binding by default: the content and the layout order.
   - Not binding by default: drawing style, fonts, decoration, sample numbers, colours. Use the project's design system from CLAUDE.md.
   - Annotations state intent and override what is drawn.
4. Map every element to data the project already has. Flag any element that needs data it does not store: that needs my approval.
5. Flag any metric that would be misleading with our data (for example a number that can only take trivial values) and propose a more honest alternative.
6. List every ambiguity with your proposed resolution.

Then stop and wait for my approval.

## Phase 2: build (after my approval)
1. Work on a new feature branch from the default branch.
2. Reuse <SHARED_COMPONENTS> before creating new ones.
3. Handle empty states, theming and small screens.
4. Run lint and build, commit, and save the mockup to <MOCKUPS_DIR> as the design reference.

## Final message
List each ambiguity and how it was resolved, the manual checks to run, and what you verified versus did not.
