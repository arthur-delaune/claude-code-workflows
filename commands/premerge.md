---
description: Read-only go/no-go check of a branch before it is merged
argument-hint: <branch name>
allowed-tools: Read, Glob, Grep, Bash(git status:*), Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(git merge-base:*), Bash(<LINT_COMMAND>:*), Bash(<BUILD_COMMAND>:*)
---

<!--
Setup: rename to <project-name>-premerge.md. Replace <DEFAULT_BRANCH>, <LINT_COMMAND>,
<BUILD_COMMAND> and adapt the checklist to your CLAUDE.md. Delete this comment when done.
-->

# Pre-merge check

Check whether branch $ARGUMENTS is ready to merge into <DEFAULT_BRANCH>.

This command is read-only: never edit files, commit, merge or delete anything.

## Process
1. If $ARGUMENTS is empty, list the local branches not merged into <DEFAULT_BRANCH> and ask which one to check.
2. The branch must be checked out and the working tree clean. If not, give me the exact command to run and stop.
3. Show the scope: git log <DEFAULT_BRANCH>..HEAD --oneline and git diff <DEFAULT_BRANCH>...HEAD --stat.
4. Run lint and build.
5. Read the full diff and check each item below. Cite file:line for every finding.

## Checklist
Data safety (any finding here is a NO-GO):
- Changes to core data shapes, their validation, or persisted keys and schemas
- Code that writes back data it filtered or failed to parse

Dependencies and config:
- Any change to the dependency manifest or to build, lint or type-checking config

Conventions (from CLAUDE.md):
- Shared helpers bypassed (formatting, validation)
- Styling or theming rules broken
- Unsafe types or unchecked casts
- Simulated features not labelled as simulated
- Non-conventional commit messages

Correctness:
- Empty states, first render before data loads, effects that could flicker or leave stale state
- Shared components changed: list every screen that uses them, since each needs a regression check

## Output
- Verdict: GO, GO WITH NOTES or NO-GO, with the reason in one line
- Findings ranked High / Medium / Low, each with file:line and a concrete fix
- Manual checks, starting with the areas most at risk
- Verified versus not verified

Never merge.
