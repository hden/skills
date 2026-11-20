---
name: kb
description: Shared agent memory in a Markdown directory. Use when a project has a configured KB, or when asked to set up the KB, recall prior findings, record reusable knowledge, tidy it, or migrate agent memories into it.
---

# kb

Shared agent memory in a Markdown directory, so findings outlive a session and reach the whole team.

## Key points

- Recall before work; record during work.
- Keep it small and current: update the best-matching page, fix stale claims, note sources and dates, mark hypotheses.
- Record only reusable knowledge not already in code or docs. Personal notes stay in the agent's own memory.
- Write only what every reader may see. No secrets, personal or customer data, or evaluations of individuals. secretlint is strongly recommended, not required.
- If Git-backed, sync before reading and publish after writing. Never lose others' work: keep both sides of conflicts, ask on contradictions, no force push.
- State the KB path in use. If none is configured or it is unclear, ask.

## Commands

- `kb setup`: record in the project's agent instructions, where every agent in use loads them, the KB location, readership, Git upstream if any, and whether to push automatically or after confirmation.
- `kb migrate`: move reusable findings from agent memories into the KB under the same rules; confirm before publishing.
