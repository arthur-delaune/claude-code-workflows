# Claude Code Workflows

Reusable, project-agnostic assets for working with Claude Code: two slash commands (code review and feature documentation) and a commented `CLAUDE.md` template. They were generalised from a sample Next.js project and keep the design choices that made them reliable. Copy them into your repo, fill in the placeholders, and adapt.

## Lessons learned

- **Prefix custom commands with a project name.** A custom `/code-review` was silently shadowed by the built-in command, so the custom version never ran. A project prefix avoids the collision.
- **A review only finds what its checklist asks for.** A conventions-only checklist missed three runtime bugs until a Correctness section was added. Keep both conventions and correctness in the checklist.
- **Write boundaries around the risk, not the mechanism.** The rule "ask before changing the category list" was ambiguous. Rewriting it around the actual risk (data loss) fixed it.
- **Run `/clear` before asking Claude to review its own work.** A fresh context stops the reviewer from defending decisions it made earlier in the session.

## What's inside

- `commands/review.md`: reviews files against your conventions, with a Correctness checklist and a "verified / not verified" section, and saves one report per file.
- `commands/docs.md`: generates developer and user documentation for a feature, strictly from what the code does.
- `templates/CLAUDE.md`: a commented project-instructions template, with boundaries written around the real risk.
- `LICENSE`: MIT.

## How to use

1. Copy the files from `commands/` into your project's `.claude/commands/`, and `templates/CLAUDE.md` to your repo root as `CLAUDE.md`.
2. Rename each command with a project prefix (for example `acme-review.md`, invoked as `/acme-review`).
3. Search for `<` placeholders (such as `<REFERENCE_COMPONENT>` or `<BUSINESS_LOGIC_DIR>`) and replace each with a value from your project. Delete the setup comments.
4. Run the command on a small file first and tighten the checklist where it misses things.

Built by Arthur Delaune, ESSEC Master in Strategy & Management of International Business (Singapore).

## License

MIT, see [LICENSE](LICENSE).
