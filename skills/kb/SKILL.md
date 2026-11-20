---
name: kb
description: Manages team memory in a Markdown knowledge base. Applies when a project has a configured KB or the user asks to set up team memory, look up prior findings, record reusable knowledge, tidy the KB, or migrate agent memories.
---

# kb

Team-shared agent memory in a Markdown directory. A team can have one member.

## Locate

Precedence: explicitly named team or directory, project instruction, global instruction scoped to this project. Several KBs: use the default or ask. No configured KB: use only on explicit request. State the resolved absolute path before first use and when switching; ask if it looks wrong.

`kb setup`: [Setup](references/setup.md). Conventions: [GitHub Wiki](references/wiki.md), [GitHub Pages](references/pages.md).

## Recall and remember

- Before work: read the index if any, search, read relevant pages. Verify time-sensitive claims.
- During work: record reusable findings (pitfalls, workarounds, decisions with reasons, pointers to sources). Personal notes stay in the agent's own memory. Skip what code or docs already say.
- Update the best-matching page instead of adding one; fix stale claims; record source and date; label hypotheses; keep navigation current.
- Cleanup on request: duplicates, stale claims, broken links.

## Before writing

Write only what every reader may see. Never write secrets, personal information, evaluations of individuals, or customer data; ask when unsure. secretlint is strongly recommended, not required; when configured, run it and never bypass it. Manual review applies either way.

## Handoff

- `kb migrate`: [Memory migration](references/migration.md).
- Start and end of work: [Synchronization](references/sync.md).
