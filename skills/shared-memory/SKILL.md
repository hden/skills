---
name: shared-memory
description: Memory that a team's coding agents share through a Markdown directory (Git repository, GitHub Wiki, or local folder). Before work, sync it and read what teammates already found; during work, record reusable findings; after work, publish without overwriting others. Use at the start and end of work in any project configured for shared memory, and whenever the user asks whether anyone looked into something before, asks to save a finding for the team, tidy the team's notes, or run `shared-memory setup` / `shared-memory migrate`.
---

# shared-memory

Memory that a team's coding agents share through a Markdown directory, so the next agent, on any tool, starts from what the team already learned. Recall before work, record reusable findings as you go, and publish after work.

## Configuration

The project's agent instructions name the directory and storage (Git repository, GitHub Wiki, or local folder), the readership, the publication mode (`auto` or `confirm`), and whether a secret check is installed. Without them, ask for the directory or offer setup. State the directory you use.

## Rules

- Readership is the boundary. Never write secrets, personal information, evaluations of individuals, or customer data. Keep out anything else a configured reader may not see, such as internal hosts in a public directory.
- Record what is reusable and not already in code or docs. Personal preferences stay in the agent's own memory.
- Publish only reviewed changes. With `confirm`, and for anything nobody has reviewed (leftovers from an earlier session, migrated memories), get the user's approval of exactly what will be published.
- Never discard others' work or bypass a secret check. Leave source memories in place unless asked.
- Report what was written where, even in `auto` mode.

## Conventions

- Follow the existing page format and index. If there is none, use the [page template](references/page-template.md).
- secretlint as a pre-commit hook is strongly recommended, not required.

## Setup

Agree on the directory, readership (warn if publishing widens it), and mode (`auto` by default). Verify the directory is writable and, with a Git remote, that you can push. Offer the secretlint hook without overwriting an existing one. Write the configuration where every agent in use loads it: `AGENTS.md`, imported from `CLAUDE.md` with `@AGENTS.md` for Claude Code.

## Migrate

From paths the user gives or the agents' own memory files, move only findings that are reusable and fit the readership. Skip transcripts.

## Known pitfalls

- Claude Code in the cloud, including Routines, cannot select a GitHub Wiki as a source; use a regular repository there.
