# KB Operations

## Shared Posture

- Protect canonical truth in `docs/entities`.
- Use `docs/indexes` for speed and orientation.
- Drill down into `docs/entities` when precision matters.
- Keep operation boundaries explicit.
- Record what was validated and what remains uncertain.

## Ingest

Use ingest when adding external material such as a web article, PDF, video, note, or copied reference.

Workflow:

1. Identify the source, origin URL/path, capture time, and reason to keep it.
2. Try MarkItDown when available for web pages, PDFs, media, or office files.
3. Review generated markdown quality before accepting it.
4. Create a stable entity directory under `docs/entities`.
5. Store the canonical payload or source pointer and a concise `note.md`.
6. Add an ingest log under `docs/logs/ingest`.
7. Update only the minimum useful index entries.

Return an ingest record with:

- `Source`
- `Capture Time`
- `Canonical Location`
- `Next Step`

## Query

Use query when retrieving, comparing, or interpreting KB knowledge.

Workflow:

1. Start from `docs/indexes` for orientation and candidate paths.
2. Inspect `docs/entities` when the answer needs citation, comparison, editing, or higher confidence.
3. Answer directly and show the evidence path.
4. State whether confidence is shallow or deep.

Return:

- `Answer`
- `Evidence Path`
- `Confidence`

## Editorial

Use editorial when refining, connecting, comparing, or consolidating existing KB content.

Workflow:

1. Start with a short editorial plan.
2. Define scope and affected entities.
3. Preserve meaningful distinctions; avoid broad rewrites.
4. Improve canonical notes or links with the smallest useful change.
5. Record whether indexes need rebuilds.

Return:

- `Editorial Plan`
- `Edits`
- `Checks`

## Housekeeping

Use housekeeping when checking consistency, stale indexes, broken links, duplicates, naming drift, or failed ingest records.

Workflow:

1. Identify the concrete inconsistency or friction.
2. Prefer local repair before broad cleanup.
3. For explicit failed-ingest records, try MarkItDown remediation when available.
4. Keep canonical payloads unchanged unless the user asks for migration.
5. Record unresolved risk.

Return:

- `Issue List`
- `Actions`
- `Residual Risk`
