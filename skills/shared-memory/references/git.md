# Git storage

Shell state may not persist: start every block with `MEM=<directory>; : "${MEM:?}"`. An empty `MEM` runs git against the project.

## Sync

```sh
MEM=<directory>; : "${MEM:?}"
[ -d "$MEM/.git" ] || git clone <upstream> "$MEM"
git -C "$MEM" status --short; git -C "$MEM" log --oneline @{u}..
```

Output from either command is a leftover: publish it (below) before pulling. Then:

```sh
MEM=<directory>; : "${MEM:?}"
git -C "$MEM" pull --rebase
```

If a secret check is configured and this clone lacks the hook, install it (below).

## Publish

```sh
MEM=<directory>; : "${MEM:?}"
git -C "$MEM" add <reviewed pages>
git -C "$MEM" diff --cached --name-only   # must list only reviewed pages
git -C "$MEM" commit -m "<what and why>"
git -C "$MEM" pull --rebase
git -C "$MEM" log -p @{u}..               # everything the push publishes
git -C "$MEM" push
```

- Stop if anything unreviewed is staged, or if another session is editing the same clone.
- `confirm`: show the `log -p @{u}..` output and push only after approval. On rejection, `git -C "$MEM" reset --soft @{u}` and report.
- Never use `--no-verify` or force-push.

## Conflicts

1. Keep both sides; concurrent index lines usually both belong. Ask about contradictions.
2. `git -C "$MEM" add <files>`, then `GIT_EDITOR=true git -C "$MEM" rebase --continue`, and resume Publish from `log -p @{u}..`. If the push is rejected, restart from `pull --rebase`.
3. If unresolvable, `git -C "$MEM" rebase --abort` and report.

## Secretlint hook

```sh
MEM=<directory>; : "${MEM:?}"
hooks=$(cd "$MEM" && cd "$(git rev-parse --git-path hooks)" && pwd); : "${hooks:?}"
cat > "$hooks/pre-commit" <<'HOOK'
#!/bin/sh
[ -z "$(git diff --cached --name-only --diff-filter=ACMR)" ] && exit 0
git diff --cached --name-only --diff-filter=ACMR -z | xargs -0 npx --yes @secretlint/quick-start
HOOK
chmod 755 "$hooks/pre-commit"
```

Report the pushed commit and changed pages.
