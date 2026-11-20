---
name: kb
description: Use to set up or maintain team memory, recall prior findings, record reusable lessons, tidy a knowledge base, or selectively migrate agent memories into shared Markdown.
---

# Team Memory

A team can have one member. Work with the team's Markdown directory through the filesystem.

## Choose the team

Use an explicitly named team or directory first, then the project's configured team, then a global instruction scoped to this project. If several teams are configured, use the default or ask which one to use. Confirm the destination if the selected path is missing or unclear. Without a configured team, use the KB only on explicit request.

For `kb setup`, see [Setup](references/setup.md). Resolve the path once from those instructions for routine work. For presentation conventions, use [GitHub Wiki](references/wiki.md) or [GitHub Pages](references/pages.md) when applicable.

## Recall and remember

- Before work in a configured project, use the existing index if available, then search Markdown and read relevant pages. Verify time-sensitive details against their sources before relying on them.
- During work, capture reusable findings such as pitfalls, verified workarounds, decision rationale, and pointers to authoritative sources. Leave personal preferences and scratch notes to the agent's own memory. Skip details readily available from the project's code or documentation.
- Search before creating a page. Update the best match, consolidate duplicates, and replace stale statements when the evidence supports a correction. Record the source and verification date. Label hypotheses and unresolved contradictions. Keep existing navigation current and report the paths changed.
- On an explicit cleanup request, review the requested scope for duplicates, stale claims, and broken links. Preserve evidence and flag unresolved discrepancies.

## Review before writing

Check the actual readership. Keep secrets, personal information, individual evaluations, and customer data out of pages, attachments, and indexes. Ask before writing when eligibility is unclear. Review source material and converted output outside the KB before copying either in.

Recommend secretlint. When configured, run it on changed files before handing them off for publication. Review personal and customer data separately. Remove flagged secrets from proposed edits and report only the affected path and kind of issue.

## Import and handoff

- On explicit `kb migrate`, use [Memory migration](references/migration.md).
- At the start and end of work in a configured KB, follow [Synchronization](references/sync.md). Synchronize automatically when a Git upstream is configured, unless instructions disable it. Report saved pages and publication status.

## Tool reference

[MarkItDown](references/markitdown.md) describes the bundled Docker wrapper for converting supported sources to Markdown.
