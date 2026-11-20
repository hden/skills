---
name: kb
description: Shared agent memory kept in a Markdown directory (a Git repository, GitHub Wiki, or local directory). Before work, sync and read what the team already knows; during work, record reusable findings; after work, publish without overwriting others. Use at the start and end of work in any project with a configured KB, and whenever the user asks to set up team memory, check prior findings ("did anyone look into this?"), record or tidy knowledge, or run `kb setup` / `kb migrate`.
---

# kb

Shared agent memory in a Markdown directory, so the next agent on any tool starts from what the team already learned.

Read only the references that apply:

| When | Reference |
|---|---|
| Git repository | [storage-git](references/storage-git.md) |
| GitHub Wiki | [storage-git](references/storage-git.md), [storage-github-wiki](references/storage-github-wiki.md) |
| Local directory | [storage-local](references/storage-local.md) |
| Instruction and memory locations per agent | [agents](references/agents.md) |
| `kb setup` | [setup](references/setup.md) |
| `kb migrate` | [migration](references/migration.md) |
| New page in a KB with no convention | [page-template](references/page-template.md) |

## Configuration

`kb setup` records in the project's agent instructions: KB directory and storage, readership, publication mode (`auto` or `confirm`), and whether a secretlint hook is installed.

Without a configuration, ask for the path or offer `kb setup`. State the resolved path at first use and in the final report.

## Before work

1. Sync as the storage reference describes. Publish leftovers from an earlier session first, always with `confirm`: nobody has reviewed them.
2. Read the index, then only the relevant pages; otherwise search.
3. Entries are as of when they were written. Verify named files, commands, or flags before relying on them.

## While working

Record findings as soon as you learn them.

- Record: pitfalls, environment quirks, verified workarounds, procedures, decisions with reasons, where resources live.
- Skip: what code, docs, or history already say; one-off details; personal preferences (the agent's own memory).
- Update the page that covers the topic instead of adding one. Fix wrong statements instead of appending contradictions.
- Separate observations (evidence, absolute date) from hypotheses (reasoning).
- Follow the KB's format, language, and naming, or the page template if there is none. Add new pages to the index.

## What may be written

1. Never, whatever the readership: secrets, personal information or evaluations of individuals, customer data.
2. Otherwise, only what every configured reader may see. Keep internal hostnames, IPs, and URLs out of public KBs.

When unsure, ask. secretlint is strongly recommended, not required; it catches only token-like strings.

## After work

Skip if nothing changed.

1. Review the full diff, leftovers included, against "What may be written".
2. If the secret check flags something, remove it and retry. Never bypass it.
3. Publish as the storage reference describes; with `confirm`, wait for approval of the diff.
4. On concurrent edits keep both sides and ask about contradictions. Never discard others' work; if stuck, leave yours unpublished and report.
5. Report what was written where, even in `auto` mode.
