# Synchronization

For Git-backed KBs. Without an upstream, just save and report paths.

Start:
- Missing directory: clone the recorded upstream; reinstall the recorded hook.
- Fetch. On failure, skip publication this task and say why.
- Leftover edits or unpushed commits from earlier work: review and publish them first, or ask. Never discard.
- Then fast-forward, or rebase local commits.

End (skip if nothing changed):
- Review the diff for secrets, personal and customer data, and readership. Run configured checks.
- Changes you did not make in the same files (e.g. another session): stop and report. Parallel sessions need separate clones or worktrees.
- Commit only reviewed changes on top of the fetched upstream. `auto`: push. `confirm`: show the diff, push after approval.
- Push rejected: fetch and rebase (no merge). On conflicts keep both sides; concurrent index lines usually both belong. Contradictions: keep both and ask. Retry once, then report.
- No force push, no destructive reset.

Report the pushed commit and changed pages, or the saved paths and blocker.
