---
description: Integrate features developed in parallel worktrees into one branch, without merging to the default branch
argument-hint: <feature-name> <feature-name> ...
allowed-tools: Bash(git:*), Bash(<LINT_COMMAND>:*), Bash(<BUILD_COMMAND>:*)
---

<!--
Setup: rename to <project-name>-integrate.md. Replace <DEFAULT_BRANCH>, <LINT_COMMAND>
and <BUILD_COMMAND>. Delete this comment when done.
-->

# Integrate parallel work

Integrate these parallel features: $ARGUMENTS

1. Check that every branch feature-<feature-name> exists and that its worktree has no uncommitted changes. If not, stop and tell me.
2. From <DEFAULT_BRANCH>, create a branch integration-<feature-names-joined-by-hyphens>.
3. Merge each feature branch in the order given. For every conflict, explain what each side wanted and how you resolved it.
4. Look for semantic conflicts Git cannot detect: features built without knowing about each other (styling and theming, shared state, layout, navigation, naming). Fix them and list each fix.
5. Run lint and build.
6. List the manual checks for the combined result, starting with the interactions between features.

Do not merge into <DEFAULT_BRANCH> and do not remove worktrees or branches: I review and merge myself.
