---
name: kb
description: Use when creating, operating, or maintaining a lightweight docs-scoped knowledge base with commands such as kb init, kb ingest, kb query, kb editorial, or kb housekeeping. Supports boilerplate setup, source capture, evidence-backed retrieval, editorial refinement, consistency checks, and optional MarkItDown-assisted conversion.
---

# KB

Use this skill when the user wants to create or operate a small agent-maintained knowledge base.

## Command Routing

Treat the first command word as the operation:

- `kb init`: run `scripts/kb init` from the intended repository root.
- `kb doctor`: run `scripts/kb doctor` to check required KB structure.
- `kb sample-llm-wiki`: run after `kb init` to verify capture with the public LLM Wiki raw Markdown source.
- `kb ingest <source>`: capture external material into `docs/entities`.
- `kb query <question>`: answer from `docs/indexes` first, then inspect `docs/entities` when confidence requires it.
- `kb editorial <scope>`: refine or connect existing KB content after making a short plan.
- `kb housekeeping [target]`: repair consistency, stale indexes, broken links, or explicit failed-ingest records.

If the user names an operation without the `kb` prefix, map it to the matching operation when intent is clear.

## Public Content Boundary

Do not import private or previously collected KB content into a new public skill or user KB.

Allowed reusable material:

- operation instructions
- schema/layout conventions
- deterministic helper scripts
- public source URLs fetched at runtime

Disallowed material:

- private `entities/`, `indexes/`, or `logs/` contents
- private notes, summaries, links, tags, or collected artifacts
- bundled copies of copyrighted source payloads

## Read As Needed

- For layout and schema decisions, read `references/layout-and-schema.md`.
- For ingest, query, editorial, and housekeeping behavior, read `references/operations.md`.
- For MarkItDown setup and review policy, read `references/markitdown.md`.

## Operating Rules

- Keep canonical knowledge under `docs/entities`.
- Treat `docs/indexes` as rebuildable projections, not truth.
- Treat `docs/logs` as chronological operation records.
- Start shallow from indexes; drill into entities for precision, citation, comparison, or editing.
- Keep changes small, additive, and reviewable.
- State validation depth and uncertainty in the final response.
