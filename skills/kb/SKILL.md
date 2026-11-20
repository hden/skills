---
name: kb
description: Shared agent memory kept in a Markdown directory, usually a Git repo or GitHub Wiki. Before work, sync and read what the team already knows; during work, record reusable findings; after work, publish without overwriting others. Use at the start and end of work in any project with a configured KB, and whenever the user asks to set up team memory, check prior findings ("did anyone look into this?"), record or tidy knowledge, or run `kb setup` / `kb migrate`.
---

# kb

Shared agent memory in a Markdown directory. An agent's own memory stays with one session or person; the KB lets the next agent, on any tool, start from what the team already learned.

## Configuration

The project's agent instructions (written by `kb setup`) name:

- KB directory: absolute, project-relative, or an environment variable
- Readership: who can read the KB once published
- Upstream: Git remote, if any
- Publication: `auto` (push after review) or `confirm` (show the diff, push after approval)
- Secret check: whether a secretlint pre-commit hook is installed

If there is no configuration, or a variable is unset, ask for the path or offer `kb setup`. Tell the user the resolved path before first use, so a wrong KB is caught early.

For `kb setup` read [setup](references/setup.md); for `kb migrate` read [migration](references/migration.md).

## Before work

1. Sync if Git-backed, so you read the team's latest state:
   - Directory missing: clone the upstream into it.
   - Leftover edits or unpushed commits: finish them via "After work" first; they are someone's unpublished knowledge.
   - Otherwise: `git -C "$KB" pull --rebase`.
2. Read the index page (`Home.md`, `_Sidebar.md`, `README.md`, `index.md`) if there is one, then only the relevant pages. Otherwise `grep -ril "<keyword>" "$KB" --include='*.md'`.
3. Treat entries as records of when they were written. Verify named files, commands, or flags still exist before relying on them.

## While working

Record as soon as you learn something; findings are lost if the session ends first.

Record: pitfalls, environment quirks, verified workarounds, procedures, decisions with their reasons, where external resources live.
Do not record: what code, docs, or Git history already say; one-off details; personal preferences (those go to the agent's own memory).

- Search before creating a page; update the page that covers the topic. Duplicates make recall miss.
- Fix or delete wrong statements instead of appending a contradiction.
- Separate observations (with evidence and an absolute date, e.g. `2026-11-20`) from hypotheses (with reasoning).
- Follow the KB's existing page format, language, and naming. Add each new page to the index.

## Never write

Whatever the publication mode, never write anything outside the readership's need to know:

- Secrets: tokens, passwords, API keys, connection strings
- Personal information or evaluations of individuals
- Customer data

When unsure, ask instead of writing. secretlint is strongly recommended but not required; it catches token-like strings only, so review personal and customer data yourself either way.

## After work

Skip if nothing changed. Without an upstream, report the changed paths and stop.

```sh
git -C "$KB" add <changed pages>
git -C "$KB" commit -m "<what was recorded and why>"
# confirm: show `git -C "$KB" show --stat -p HEAD` and wait for approval
git -C "$KB" pull --rebase
git -C "$KB" push
```

- Stage only pages you changed. If someone else's uncommitted edits share a file (another session in the same directory), stop and report; parallel sessions need separate clones.
- If the hook flags a secret, remove it and commit again. Never use `--no-verify`.
- On conflict, keep both sides; concurrent index entries usually both belong. If they contradict, keep both and ask the user. Then `GIT_EDITOR=true git -C "$KB" rebase --continue` and push again. If you cannot resolve it, `git rebase --abort` and report, leaving the commit for the next session.
- Never force-push or reset away others' commits.

Report the pushed commit and the changed pages, including what was written, even in `auto` mode, so humans know what the team now reads.
