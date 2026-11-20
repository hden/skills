# kb setup

1. Settle with the user:
   - Storage and directory: reuse an existing Markdown directory, clone an existing upstream, or create a new one.
   - Readership: check the upstream's visibility. Warn if publishing would widen who can read the content.
   - Publication mode: `auto` (default) or `confirm`.
2. Verify access: the KB can be read, and for Git `git push --dry-run` succeeds.
3. Offer a secretlint pre-commit hook (strongly recommended, not required). Install it only if it runs on this machine; hooks are per clone, so each clone needs it.

   ```sh
   # $(git -C "$KB" rev-parse --git-path hooks)/pre-commit, mode 755
   #!/bin/sh
   [ -z "$(git diff --cached --name-only --diff-filter=ACMR)" ] && exit 0
   git diff --cached --name-only --diff-filter=ACMR -z | xargs -0 npx --yes @secretlint/quick-start
   ```
4. Write the configuration where every agent in use loads it (see agents), preserving other content. Use project scope unless the user asks for global; a global entry names the absolute project directory it applies to. Replace any earlier kb instruction instead of adding a second one.
5. Report the files changed.

Example:

```markdown
Use the kb skill for team memory in this project: its "Before work" at the start of each task, record findings as you go, and its "After work" when the task ends.
- KB: `$PLATFORM_KB_DIR`, GitHub Wiki https://github.com/example/platform.wiki.git
- Readership: Platform team (private repository)
- Publication: auto
- Secret check: secretlint pre-commit hook
```
