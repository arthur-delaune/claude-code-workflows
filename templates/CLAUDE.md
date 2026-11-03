# CLAUDE.md

<!--
Template. Replace every <PLACEHOLDER>, delete sections that do not apply, and remove
all HTML comments. Keep it short: every line should change how Claude behaves.
-->

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

<!-- Only commands Claude should actually run. State what is NOT available (e.g. no test runner). -->
```bash
<DEV_COMMAND>     # start the dev server
<BUILD_COMMAND>   # production build
<LINT_COMMAND>    # lint
```

<TEST_RUNNER_STATUS: e.g. "There is no test runner configured.">

## Architecture

<!-- 2-3 sentences: what the project is, stack, where data lives, any import alias. -->
<PROJECT_NAME>: <ONE_LINE_DESCRIPTION> (<STACK>). <WHERE_DATA_LIVES>.

<!-- One bullet per module that is not obvious from its name: what it owns, and what breaks if it changes. -->
- `<ENTRY_POINT>` owns <RESPONSIBILITY>.
- `<STATE_OR_PERSISTENCE_MODULE>` is the sole <ROLE>. Changing <CORE_DATA_SHAPE> requires <REQUIRED_FOLLOW_UP>, or <CONSEQUENCE>.
- `<TYPES_FILE>` holds the domain types and <SOURCE_OF_TRUTH_CONSTANTS>.

### <SUBSYSTEM_NAME> (`<SUBSYSTEM_DIRS>`)
<!-- Optional. Include only for subsystems with an extension recipe. -->
- Entry point: `<ENTRY_FUNCTION>`.
- To add a <EXTENSION_POINT>: <STEP_1>, <STEP_2>, <STEP_3>.

## Development Workflow
1. Never commit directly to `<DEFAULT_BRANCH>`. Branch from it using `<BRANCH_PREFIX_1>-[short-description]` or `<BRANCH_PREFIX_2>-[short-description]`.
2. Use conventional commit messages: `feat:`, `fix:`, `refactor:`, `docs:`, `chore:`.
3. Never merge into `<DEFAULT_BRANCH>` yourself: <WHO_REVIEWS_AND_MERGES>.
4. For changes touching more than <N> files, present a plan first and save it to `<PLANS_DIR>/<feature>.md`.
5. Parallel worktrees: at integration, look for semantic conflicts Git cannot see (styling, theming, shared layout, navigation), not only text conflicts.

## Quality Gates (before every commit)
- `<LINT_COMMAND>` and `<BUILD_COMMAND>` must both pass with no errors.
- <WHAT_TO_DO_WITHOUT_TESTS: e.g. "List the manual checks needed to verify the change in your final message.">
- Always state clearly what you verified and what you did not.

## Code Standards
- <TYPE_SAFETY_RULE>
- Layering: business logic in `<BUSINESS_LOGIC_DIR>`, UI in `<UI_DIR>`, state in `<STATE_DIR>`.
- <STYLING_RULE>; reuse `<REFERENCE_COMPONENT>` for <PATTERN>.
- Always use `<SHARED_HELPER>` for <CONCERN>; never hand-roll it.
<!-- Allow what the rule is really for. A palette rule with no status colours forced warnings to be drawn in the brand colour. -->
- <DESIGN_SYSTEM_RULE, including the colours allowed for status: warning, error>.
- Metrics shown to users must mean what their label says. If a number can only take trivial values, flag it instead of displaying it.

## Boundaries

<!--
Write each boundary as the REAL RISK, not the mechanism. Name the harm (data loss,
broken migrations, leaked secrets), then list the actions that cause it. A rule like
"ask before changing X" is ambiguous; a rule like "X changes can silently destroy
user data, so ask first" tells Claude why and lets it generalise.
-->
<!-- Write down known risks you have found in the code: Claude cannot avoid what it has not been told about. -->
- Known risk: <KNOWN_RISK, e.g. "invalid records are filtered on load and the filtered list is saved back, so stricter validation deletes stored data">.
- Ask before adding any new dependency.
- Safe, no confirmation needed: <LOW_RISK_ACTION>. <WHY_IT_IS_SAFE>.
- Always ask first, even if I explicitly requested the change, before: <RISKY_ACTIONS>. Risk: <CONCRETE_HARM, e.g. existing user data silently dropped>. Agree on <MITIGATION: migration, version bump, backup> before touching it.
- Any simulated feature (fake email, mock sync, etc.) must be clearly labelled as simulated in the UI.
- Never run <DESTRUCTIVE_COMMAND, e.g. forced or bulk fix commands>.

## Subagents and unattended work

<!-- Subagents cannot ask questions, so "ask first" rules need a fallback. -->
Subagents cannot ask questions. When a task hits a boundary above, stop that part, explain why in the report, and finish the rest. Do not work around a boundary.
