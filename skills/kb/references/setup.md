# kb setup

1. Settle with the user:
   - KB directory. Reuse an existing Markdown directory, clone an existing upstream (e.g. `https://github.com/OWNER/REPO.wiki.git`), or create a new one.
   - Readership. Check the upstream's visibility; warn if publishing would widen who can read the content.
   - Publication mode: `auto` (default) or `confirm`.
2. Verify access: the KB can be read, and for Git-backed KBs `git push --dry-run` succeeds.
3. Offer a secretlint pre-commit hook (strongly recommended, not required). Install it only if it runs on this machine, e.g. a hook that runs `npx --yes @secretlint/quick-start` on the staged files. Hooks are per clone, so a new clone needs it again.
4. Write the configuration where every agent in use loads it, preserving existing content:
   - Project scope (default): the project's `AGENTS.md`. Claude Code reads `CLAUDE.md` instead, so make sure it imports `@AGENTS.md`.
   - Global scope (on request): the agent's global instruction file, naming the absolute project directory it applies to.
   - Replace any earlier kb instruction rather than adding a second one.
5. Report the files changed.

Example instruction:

```markdown
Use the kb skill for team memory in this project.
- KB: `$PLATFORM_KB_DIR` (clone of https://github.com/example/platform.wiki.git)
- Readership: Platform team (private repository)
- Publication: auto
- Secret check: secretlint pre-commit hook
```
