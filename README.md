# Plumb

Engineering rules for [Claude Code](https://claude.com/claude-code). Add them to a project and Claude follows the same conventions for architecture, code style, API errors, testing and pull requests, in TypeScript, Go or Java.

## Usage

Copy the `.claude/` folder into the root of your project:

```sh
cp -r plumb/.claude your-project/
```

Claude Code loads `.claude/CLAUDE.md` and the files in `.claude/rules/` at the start of each session. If your project already has a `.claude/CLAUDE.md`, merge the two instead of overwriting yours.

Then add a short `## Project` section to your project's `.claude/CLAUDE.md` with what Claude can't learn from the code: commands, where conventions live and what not to touch. Keep it to a few lines, not a folder tree — Claude can explore the structure itself, and a written tree goes stale.

```markdown
## Project

- Test: `pnpm test` · E2E: `pnpm test:e2e` · Lint: `pnpm lint`
- Features live in `src/modules/<feature>/`; shared helpers in `src/lib/`.
- Never edit `src/gen/` (generated) or existing files in `migrations/`.
```

## What's inside

| File                             | Covers                                                                                              |
| -------------------------------- | --------------------------------------------------------------------------------------------------- |
| `.claude/CLAUDE.md`              | How Claude works: ask instead of guessing, simplicity first, surgical changes, commit conventions   |
| `.claude/rules/architecture.md`  | Layers, query performance, coupling, and adding new variants without rewriting the system           |
| `.claude/rules/code-style.md`    | Naming, small functions, parameters, reuse, strict typing, no comments                              |
| `.claude/rules/api-errors.md`    | Error responses as [RFC 9457](https://www.rfc-editor.org/info/rfc9457) Problem Details              |
| `.claude/rules/testing.md`       | Given/When/Then test names, coverage thresholds, integration and E2E tests first                    |
| `.claude/rules/pull-requests.md` | Descriptions that list every behavior change with its location, before, after and reason           |

## Existing codebases

The rules apply to new code and to the lines Claude changes. Existing code is refactored to match them only when you ask, so you can adopt Plumb without rewriting your codebase.

## License

[MIT](LICENSE)
