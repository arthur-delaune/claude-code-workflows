---
description: Build several features in parallel with Git worktrees and one subagent per feature
argument-hint: <feature descriptions>
---

<!--
Setup: rename to <project-name>-parallel-agents.md and run it from the parent folder of
the repo. Replace <REPO_DIR>, <DEFAULT_BRANCH>, <INSTALL_COMMAND>, <LINT_COMMAND>,
<BUILD_COMMAND> and <REPORTS_DIR> (a folder outside the repo). Delete this comment when done.
-->

# Parallel features with subagents

Develop these features in parallel: $ARGUMENTS

You are in the parent folder of <REPO_DIR>.

## Phase 1: setup
For each feature:
1. From <REPO_DIR> on a clean, up-to-date <DEFAULT_BRANCH>, create a worktree at ../<REPO_DIR>-<feature-name> with a new branch feature-<feature-name>.
2. Run <INSTALL_COMMAND> in each worktree: dependencies are not shared.
3. List all worktrees.

## Phase 2: subagents (in parallel, one per feature)
Subagents cannot ask questions, so every boundary is written here in advance. Instructions for each subagent:
- Work only in your worktree. Read its CLAUDE.md first and follow it strictly.
- Never change core data shapes or persisted keys, and never add a dependency. If the feature cannot be built without one of these, stop and explain why in the report instead of building it. Do not work around a boundary.
- Run <LINT_COMMAND> and <BUILD_COMMAND>; do not start a dev server.
- Commit on the feature branch with a conventional commit message.
- Write a report to <REPORTS_DIR>/<feature-name>.md: what was built, files changed, lint and build results, what was not verified, and likely integration conflicts.

## Phase 3: summary
Read every report, check the commits yourself rather than trusting the reports, and give me: the status of each feature, the files touched by more than one feature, missing glue (for example navigation no single feature added), and the next integration steps.

Do not merge anything.
