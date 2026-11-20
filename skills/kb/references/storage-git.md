# Storage: Git

Shell state may not persist, so set `KB` in every command; an empty `KB` runs git against the project instead.

## Sync

```sh
KB=<path>; : "${KB:?}"
[ -d "$KB/.git" ] || git clone <upstream> "$KB"
git -C "$KB" status --short; git -C "$KB" log --oneline @{u}..   # leftovers
git -C "$KB" pull --rebase
```

Reinstall the configured secretlint hook if this clone lacks it.

## Publish

```sh
git -C "$KB" add <reviewed pages>
git -C "$KB" commit -m "<what and why>"
# confirm: show `git -C "$KB" show --stat -p HEAD`, wait for approval
git -C "$KB" pull --rebase
git -C "$KB" push
```

If another session is editing the same clone, stop and report. Never use `--no-verify` or force-push.

## Conflicts

1. Keep both sides; concurrent index lines usually both belong. Ask about contradictions.
2. `git -C "$KB" add <files>`, then `GIT_EDITOR=true git -C "$KB" rebase --continue` and push. If rejected, restart from `pull --rebase`.
3. If unresolvable, `git -C "$KB" rebase --abort` and report.

Report the pushed commit and changed pages.
