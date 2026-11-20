# shared-memory setup

1. Settle with the user: directory (reuse, clone, or create), readership (warn if publishing widens it), and publication mode (`auto` default, or `confirm`).
2. Verify the directory is readable and, for Git, `git push --dry-run` succeeds.
3. Offer the secretlint pre-commit hook from git; install it only if it runs here. Hooks are per clone.
4. Write the configuration where every agent in use loads it, replacing any earlier one. Global scope, on request, names the absolute project directory.
5. Report the files changed.

Example:

```markdown
Use the shared-memory skill: "Before work" at the start of each task, record findings as you go, "After work" at the end.
- Directory: `$PLATFORM_MEMORY_DIR`, GitHub Wiki https://github.com/example/platform.wiki.git
- Readership: Platform team (private)
- Publication: auto
- Secret check: secretlint hook
```
