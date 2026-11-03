# Claude Code Workflows

Reusable, project-agnostic assets for working with Claude Code: seven slash commands covering the full feature cycle (plan, build from a mockup, parallel work, integration, review, documentation, pre-merge check) and a commented `CLAUDE.md` template. They were generalised from a sample Next.js project and keep the design choices that made them reliable. Copy them into your repo, fill in the placeholders, and adapt.

## Lessons learned

**Writing rules**
- **Prefix custom commands with a project name.** A custom `/code-review` was silently shadowed by the built-in command, so the custom version never ran.
- **Write boundaries around the risk, not the mechanism.** "Ask before changing the category list" was ambiguous. Rewriting it around the actual risk (data loss) fixed it.
- **A rule that is too strict forces a bad result.** A palette rule with no status colours made Claude draw budget warnings in the brand colour, where no user would read them as warnings. Fix the rule, not only the code.

**Planning and specs**
- **The value of thinking first is in reviewing the plan.** A deep first plan ended with ten open questions and could not be executed. Answering them took two minutes and turned it into an implementation order; fixing the code afterwards would have taken far longer.
- **A mockup is intent, not a specification.** Ask Claude to describe the image and list ambiguities before coding, and say what is binding (content, layout) and what is not (style, sample numbers).
- **A metric that looks meaningful may not be.** A sketched "budget streak" could only equal the days elapsed or zero with monthly budgets. It became an honest on-budget status instead.

**Reviews**
- **A review only finds what its checklist asks for.** A conventions-only checklist missed three runtime bugs until a Correctness section was added.
- **Run `/clear` before asking Claude to review its own work.** A fresh context stops the reviewer from defending decisions it made earlier in the session.

**Parallel work**
- **Git detects text conflicts, not semantic ones.** Two features built in parallel merged cleanly, but the new budgets panel had no dark-mode styling because it was built without knowing dark mode existed.
- **Subagents cannot ask questions, so every boundary must be written in advance.** A feature that needed a data field the app did not have was replaced before launch; left to itself, a subagent would have improvised one.

## What's inside

| File | Use it to |
| --- | --- |
| `commands/plan.md` | Write a decision-ready plan with defaults for every question, no code |
| `commands/from-mockup.md` | Read a sketch or screenshot, confirm ambiguities, then build the screen |
| `commands/parallel-agents.md` | Build several features at once with worktrees and one subagent each |
| `commands/integrate.md` | Merge parallel branches and fix the semantic conflicts Git cannot see |
| `commands/review.md` | Review files against conventions and correctness, one report per file |
| `commands/docs.md` | Generate developer and user documentation strictly from what the code does |
| `commands/premerge.md` | Read-only GO / NO-GO check of a branch before merging |
| `templates/CLAUDE.md` | Project instructions with risk-based boundaries and rules for subagents |

## How to use

1. Copy the files from `commands/` into your project's `.claude/commands/`, and `templates/CLAUDE.md` to your repo root as `CLAUDE.md`.
2. Rename each command with a project prefix (for example `acme-review.md`, invoked as `/acme-review`).
3. Search for `<` placeholders (such as `<DEFAULT_BRANCH>` or `<LINT_COMMAND>`) and replace each with a value from your project. Delete the setup comments.
4. Run each command on a small task first and tighten it where it misses things.

Built by Arthur Delaune, ESSEC Master in Strategy & Management of International Business (Singapore).

## License

MIT, see [LICENSE](LICENSE).
