# Storage: Git repository

Applies to any Git remote: a GitHub repository, a GitHub Wiki, or another host. `$KB` is the clone.

## Sync

```sh
[ -d "$KB/.git" ] || git clone <upstream> "$KB"   # reinstall the secret-check hook after cloning
git -C "$KB" pull --rebase
```

`pull` fails on leftover local changes or commits: publish them first.

## Publish

```sh
git -C "$KB" add <changed pages>
git -C "$KB" commit -m "<what was recorded and why>"
# confirm: show `git -C "$KB" show --stat -p HEAD` and wait for approval
git -C "$KB" pull --rebase
git -C "$KB" push
```

- Stage only the pages this session changed. If uncommitted edits you did not make share a file (another session in the same clone), stop and report; parallel sessions need separate clones or worktrees.
- Do not use `--no-verify`.

## Conflicts

1. Keep both sides. Concurrent index entries usually both belong.
2. If the sides contradict, keep both and ask the user.
3. `git -C "$KB" add <files>` and `GIT_EDITOR=true git -C "$KB" rebase --continue` (otherwise an editor blocks), then push again. If rejected again, restart from `pull --rebase`.
4. If you cannot resolve it, `git -C "$KB" rebase --abort` and report; the commit stays local for the next session.

Never force-push or reset away others' commits.

## Report

The pushed commit and the changed pages (as URLs when the host renders them).
