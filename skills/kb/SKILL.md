---
name: kb
description: Shared agent memory kept in a Markdown directory (a Git repository, GitHub Wiki, or local directory). Before work, sync and read what the team already knows; during work, record reusable findings; after work, publish without overwriting others. Use at the start and end of work in any project with a configured KB, and whenever the user asks to set up team memory, check prior findings ("did anyone look into this?"), record or tidy knowledge, or run `kb setup` / `kb migrate`.
---

# kb

Shared agent memory in a Markdown directory. An agent's own memory stays with one session or person; the KB lets the next agent, on any tool, start from what the team already learned.

This file is the workflow. Details that vary are in references; read only the ones that apply:

| Varies by | Reference |
|---|---|
| Storage: Git repository (GitHub or other remote) | [storage-git](references/storage-git.md) |
| Storage: GitHub Wiki | [storage-git](references/storage-git.md) and [storage-github-wiki](references/storage-github-wiki.md) |
| Storage: local directory, no remote | [storage-local](references/storage-local.md) |
| Agent: where instructions and memories live | [agents](references/agents.md) |
| `kb setup` | [setup](references/setup.md) |
| `kb migrate` | [migration](references/migration.md) |

## Configuration

The project's agent instructions, written by `kb setup`, name:

- KB directory (absolute, project-relative, or an environment variable) and storage type
- Readership: who can read the KB once published
- Publication: `auto` (publish after review) or `confirm` (show the diff, publish after approval)
- Secret check: whether a secretlint hook is installed

If there is no configuration or a variable is unset, ask for the path or offer `kb setup`. Tell the user the resolved path before first use, so a wrong KB is caught early.

## Before work

1. Sync to the team's latest state, as the storage reference describes. If unpublished work is left over from an earlier session, publish it first via "After work"; it is someone's knowledge that nobody else can see yet.
2. Read the index page if there is one, then only the relevant pages. Otherwise search the Markdown files for keywords.
3. Treat entries as records of when they were written. Verify named files, commands, or flags still exist before relying on them.

## While working

Record as soon as you learn something; findings are lost if the session ends first.

Record: pitfalls, environment quirks, verified workarounds, procedures, decisions with their reasons, where external resources live.
Skip: what code, docs, or history already say; one-off details; personal preferences (those belong in the agent's own memory).

- Search before creating a page and update the one that covers the topic. Duplicates make recall miss.
- Fix or delete wrong statements instead of appending a contradiction.
- Separate observations (with evidence and an absolute date, e.g. `2026-11-20`) from hypotheses (with reasoning).
- Follow the KB's existing format, language, and naming. Add each new page to the index.

## Never write

Whatever the publication mode, the readership is the boundary. Never write:

- Secrets: tokens, passwords, API keys, connection strings
- Personal information or evaluations of individuals
- Customer data

When unsure, ask instead of writing. secretlint is strongly recommended but not required. It only catches token-like strings, so review personal and customer data yourself either way.

## After work

Skip if nothing changed.

1. Review the diff of this session's changes against "Never write" and the readership.
2. Run the secret check if configured. If it flags something, remove it and retry; never bypass the check.
3. Publish as the storage reference describes. With `confirm`, show the diff and wait for approval first.
4. When others changed the same content concurrently, keep both sides; contradictions go to the user. Never discard others' work to make your publish succeed. If you cannot resolve it, leave your work unpublished and report.
5. Report what was written where, even in `auto` mode, so humans know what the team now reads.
