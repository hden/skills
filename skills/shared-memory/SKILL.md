---
name: shared-memory
description: Memory that a team's coding agents share through a Markdown directory (Git repository, GitHub Wiki, or local folder). Before work, sync it and read what teammates already found; during work, record reusable findings; after work, publish without overwriting others. Use at the start and end of work in any project configured for shared memory, and whenever the user asks whether anyone looked into something before, asks to save a finding for the team, tidy the team's notes, or run `shared-memory setup` / `shared-memory migrate`.
---

# shared-memory

An agent's own memory stays with one person and tool. Shared memory is a Markdown directory the whole team's agents read and write, so the next agent starts from what the team already learned.

Read the references that apply:

| When | Reference |
|---|---|
| Git repository | [git](references/git.md) |
| GitHub Wiki | [git](references/git.md), [github-wiki](references/github-wiki.md) |
| Local folder | [local-folder](references/local-folder.md) |
| Where each agent keeps instructions and memory | [agents](references/agents.md) |
| `shared-memory setup` | [setup](references/setup.md) |
| `shared-memory migrate` | [migrate](references/migrate.md) |
| First page where no convention exists | [page-template](references/page-template.md) |

## Configuration

Setup records in the project's agent instructions: directory and storage, readership, publication mode (`auto` or `confirm`), and whether a secretlint hook is installed.

Without a configuration, ask for the directory or offer setup. State the directory you use at first use and in the final report.

## Before work

1. Sync as the storage reference describes. Publish leftovers from an earlier session first, always with `confirm`: nobody has reviewed them.
2. Read the index, then only the relevant pages; otherwise search.
3. Pages are as of when they were written. Verify named files, commands, or flags before relying on them.

## While working

Record findings as soon as you learn them.

- Record: pitfalls, environment quirks, verified workarounds, procedures, decisions with reasons, where resources live.
- Skip: what code, docs, or history already say; one-off details; personal preferences (the agent's own memory).
- If a page covers the same topic, update it; otherwise add a page. Fix wrong statements instead of appending contradictions.
- Separate observations (evidence, absolute date) from hypotheses (reasoning).
- Follow the existing format, language, and naming, or the page template if there is none. Add new pages to the index.

## What may be written

1. Never, whatever the readership: secrets, personal information or evaluations of individuals, customer data.
2. Otherwise, only what every configured reader may see. Keep internal hostnames, IPs, and URLs out of public memory.

When unsure, ask. secretlint is strongly recommended, not required; it catches only token-like strings.

## After work

Skip if nothing changed.

1. Review the full diff, leftovers included, against "What may be written".
2. If the secret check flags something, remove it and retry. Never bypass it.
3. Publish as the storage reference describes; with `confirm`, wait for approval of the diff.
4. On concurrent edits keep both sides and ask about contradictions. Never discard others' work; if stuck, leave yours unpublished and report.
5. Report what was written where, even in `auto` mode.
