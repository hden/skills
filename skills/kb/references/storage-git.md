# Storage: Git repository

Applies to any Git remote: a GitHub repository, a GitHub Wiki, or another host. `$KB` is the clone.

Shell state may not persist between commands, so set `KB` in every command and stop if it is empty; otherwise git runs against the project repository instead.

## Sync

```sh
KB=<resolved path>; : "${KB:?}"
[ -d "$KB/.git" ] || git clone <upstream> "$KB"
git -C "$KB" status --short; git -C "$KB" log --oneline @{u}..   # leftovers: publish them first
git -C "$KB" pull --rebase
```

If the configuration records a secretlint hook and this clone lacks it (new clone, new machine), install it as in setup.

## Publish

```sh
git -C "$KB" add <changed pages>
git -C "$KB" commit -m "<what was recorded and why>"
# confirm: show `git -C "$KB" show --stat -p HEAD` and wait for approval
git -C "$KB" pull --rebase
git -C "$KB" push
```

- Stage only the reviewed pages: this session's changes and reviewed leftovers. If another session is still editing the same clone, stop and report; parallel sessions need separate clones or worktrees.
- Do not use `--no-verify`.

## Conflicts

1. Keep both sides. Concurrent index entries usually both belong.
2. If the sides contradict, keep both and ask the user.
3. `git -C "$KB" add <files>` and `GIT_EDITOR=true git -C "$KB" rebase --continue` (otherwise an editor blocks), then push again. If rejected again, restart from `pull --rebase`.
4. If you cannot resolve it, `git -C "$KB" rebase --abort` and report; the commit stays local for the next session.

Never force-push or reset away others' commits.

## Report

The pushed commit and the changed pages (as URLs when the host renders them).
