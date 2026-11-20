# kb setup

1. Settle with the user:
   - Storage and directory: reuse an existing Markdown directory, clone an existing upstream, or create a new one.
   - Readership: check the upstream's visibility. Warn if publishing would widen who can read the content.
   - Publication mode: `auto` (default) or `confirm`.
2. Verify access: the KB can be read, and for Git `git push --dry-run` succeeds.
3. Offer a secretlint pre-commit hook (strongly recommended, not required), e.g. one that runs `npx --yes @secretlint/quick-start` on staged files. Install it only if it runs on this machine. Hooks are per clone, so a new clone needs it again.
4. Write the configuration where every agent in use loads it (see agents), preserving other content. Use project scope unless the user asks for global; a global entry names the absolute project directory it applies to. Replace any earlier kb instruction instead of adding a second one.
5. Report the files changed.

Example:

```markdown
Use the kb skill for team memory in this project.
- KB: `$PLATFORM_KB_DIR`, GitHub Wiki https://github.com/example/platform.wiki.git
- Readership: Platform team (private repository)
- Publication: auto
- Secret check: secretlint pre-commit hook
```
