# Synchronization

A configured team KB with a Git upstream syncs automatically unless instructed otherwise. Apply the team's existing publication workflow when it specifies one.

- Before recalling memories, check the KB's Git status and sync with its configured upstream. Use a fast-forward update on a clean working tree. If the tree is dirty or the branches have diverged, preserve the existing work and review the state before editing or syncing.
- After recording memories, skip publication if this task changed no KB files. Review the exact changes for secrets, personal and customer data, and the destination's readership. Run configured checks, including secretlint where available. Stage only this task's reviewed KB changes and leave unrelated changes alone. Commit the reviewed changes and push to the verified upstream without waiting for a separate instruction. If unrelated staged changes prevent an isolated commit, leave the edits in place and report the blocker.
- If a push races with another update, fetch and integrate the upstream changes using the team's workflow. Preserve both contributors' edits, review the merged result, and retry once. If a conflict cannot be resolved confidently or publication fails again, retain the work and report the blocker. Avoid force pushes and destructive resets.
- A plain directory or Git branch without a configured upstream still supports the same memory operations. Save the edits in place and report their paths.

Report the pushed commit and changed pages when published. For unpublished edits, report the saved paths and any blocker.
