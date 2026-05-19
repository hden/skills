# KB Layout and Schema

## Layout

This skill uses a docs-scoped KB layout:

```text
docs/
  entities/
  indexes/
  logs/
    ingest/
    editorial/
    housekeeping/
    query/
```

`docs/entities` contains canonical knowledge objects. If a fact must survive index rebuilds, it belongs in an entity.

`docs/indexes` contains derived views that help browsing, recall, and candidate discovery. Indexes are projections and should be rebuildable from entities.

`docs/logs` contains chronological operation records. Logs describe what happened; they are not substitutes for canonical entities.

## Entity Shape

Each entity should live in its own directory:

```text
docs/entities/<stable-entity-id>/
  entity.edn
  note.md
  body.md | original.pdf | source.html | transcript.md | attachments/
```

Prefer stable, lowercase hyphen-case entity IDs. Avoid deep category trees unless repeated use proves they are necessary.

## Minimal `entity.edn`

Use the smallest useful structured record:

```clojure
{:entity/id "source-example"
 :entity/title "Example Source"
 :entity/created-at "2026-05-19T00:00:00Z"
 :entity/roles #{:role/source}
 :entity/links {}
 :source/url "https://example.com"
 :source/path "body.md"
 :capture/collected-at "2026-05-19T00:00:00Z"
 :capture/reason "Why this was kept."}
```

Keep unstable interpretation in `note.md` until structure has repeated value.

## Placement Rule

Ask these questions in order:

1. Is it canonical truth? Put it in `docs/entities`.
2. Is it rebuildable from entities? Put it in `docs/indexes`.
3. Is it operation history? Put it in `docs/logs`.
4. Is it about how the KB works? Put it in documentation or the skill references.

Do not duplicate canonical facts into indexes or logs for convenience.
