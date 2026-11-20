# kb setup

1. Settle with the user: directory (reuse, clone, or create), readership (warn if publishing widens it), and publication mode (`auto` default, or `confirm`).
2. Verify the KB is readable and, for Git, `git push --dry-run` succeeds.
3. Offer a secretlint pre-commit hook; install it only if it runs here. Hooks are per clone.

   ```sh
   #!/bin/sh
   # $(git -C "$KB" rev-parse --git-path hooks)/pre-commit, mode 755
   [ -z "$(git diff --cached --name-only --diff-filter=ACMR)" ] && exit 0
   git diff --cached --name-only --diff-filter=ACMR -z | xargs -0 npx --yes @secretlint/quick-start
   ```
4. Write the configuration where every agent in use loads it (see agents), replacing any earlier kb instruction. Global scope, on request, names the absolute project directory.
5. Report the files changed.

Example:

```markdown
Use the kb skill: "Before work" at the start of each task, record findings as you go, "After work" at the end.
- KB: `$PLATFORM_KB_DIR`, GitHub Wiki https://github.com/example/platform.wiki.git
- Readership: Platform team (private)
- Publication: auto
- Secret check: secretlint hook
```
