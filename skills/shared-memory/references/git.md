# Git storage

Shell state may not persist: start every block with `set -e; MEM=<directory>; : "${MEM:?}"`. An empty `MEM` runs git against the project, and `set -e` stops a block at the first failure.

## Sync

```sh
set -e; MEM=<directory>; : "${MEM:?}"
[ -e "$MEM/.git" ] || git clone <upstream> "$MEM"
[ "$(git -C "$MEM" rev-parse --show-toplevel)" = "$(cd "$MEM" && pwd -P)" ]   # not a parent repo
git -C "$MEM" status --short; git -C "$MEM" log --oneline @{u}..
```

If a secret check is configured and this clone lacks the hook, install it (below) before anything else. Output from the last line is a leftover: publish it first (below). Otherwise:

```sh
set -e; MEM=<directory>; : "${MEM:?}"
git -C "$MEM" pull --rebase
```

## Publish

```sh
set -e; MEM=<directory>; : "${MEM:?}"
git -C "$MEM" add <reviewed pages>      # skip add and commit if only unpushed commits remain
git -C "$MEM" diff --cached              # must match the reviewed diff exactly
git -C "$MEM" commit -m "<what and why>"
git -C "$MEM" pull --rebase
git -C "$MEM" log -p @{u}..               # everything the push publishes
git -C "$MEM" push
```

- Stop if the staged diff contains anything unreviewed.
- `confirm`: show the `log -p @{u}..` output and push only after approval. On rejection, `git -C "$MEM" reset --soft @{u}` and `git -C "$MEM" stash push -m "shared-memory: rejected"` so later syncs are not blocked, and report.
- Never use `--no-verify` or force-push.

## Conflicts

1. Keep both sides; concurrent index lines usually both belong. Ask about contradictions.
2. `git -C "$MEM" add <files>`, then `GIT_EDITOR=true git -C "$MEM" rebase --continue`, and resume Publish from `log -p @{u}..`. If the push is rejected, restart from `pull --rebase`.
3. If unresolvable, `git -C "$MEM" rebase --abort` and report.

## Secretlint hook

Requires Node.js. Pin secretlint the way the memory repository manages its tools, if it does. If a `pre-commit` hook already exists, ask instead of overwriting it.

```sh
set -e; MEM=<directory>; : "${MEM:?}"
hooks=$(cd "$MEM" && cd "$(git rev-parse --git-path hooks)" && pwd); : "${hooks:?}"
cat > "$hooks/pre-commit" <<'HOOK'
#!/bin/sh
[ -z "$(git diff --cached --name-only --diff-filter=ACMR)" ] && exit 0
# secretlint reads the working tree, so it must match the index
git diff --cached --name-only --diff-filter=ACMR -z | xargs -0 git diff --quiet -- || { echo "re-add files edited after staging" >&2; exit 1; }
git diff --cached --name-only --diff-filter=ACMR -z | xargs -0 npx --yes @secretlint/quick-start
HOOK
chmod 755 "$hooks/pre-commit"
```
