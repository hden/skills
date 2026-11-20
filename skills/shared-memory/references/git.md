# Git storage

Shell state may not persist, so set `MEM` in every command; an empty `MEM` runs git against the project instead.

## Sync

```sh
MEM=<directory>; : "${MEM:?}"
[ -d "$MEM/.git" ] || git clone <upstream> "$MEM"
git -C "$MEM" status --short; git -C "$MEM" log --oneline @{u}..   # leftovers
git -C "$MEM" pull --rebase
```

Reinstall the configured secretlint hook if this clone lacks it.

## Publish

```sh
git -C "$MEM" add <reviewed pages>
git -C "$MEM" commit -m "<what and why>"
# confirm: show `git -C "$MEM" show --stat -p HEAD`, wait for approval
git -C "$MEM" pull --rebase
git -C "$MEM" push
```

If another session is editing the same clone, stop and report. Never use `--no-verify` or force-push.

## Conflicts

1. Keep both sides; concurrent index lines usually both belong. Ask about contradictions.
2. `git -C "$MEM" add <files>`, then `GIT_EDITOR=true git -C "$MEM" rebase --continue` and push. If rejected, restart from `pull --rebase`.
3. If unresolvable, `git -C "$MEM" rebase --abort` and report.

Report the pushed commit and changed pages.
