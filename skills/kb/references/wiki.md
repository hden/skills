# Team Wiki

## Setup

`kb setup [--scope project|global|both] [--wiki OWNER/REPO] [--publish auto|manual]`

Default to project scope and auto publish. Retain existing settings. Ask for missing values. Verify the Wiki can be cloned.

Write one managed line between `<!-- kb:begin -->` and `<!-- kb:end -->`:

> Read the `kb` skill for team knowledge in `OWNER/REPO`.

Add eligible repos or orgs for global scope and `publish=manual` if selected. Preserve other text and report changes.

- Project: Git-root `AGENTS.md`. Add `@AGENTS.md` to root `CLAUDE.md` if needed.
- Global: `AGENTS.md` in `CODEX_HOME` (default `~/.codex`), and `CLAUDE.md` in `CLAUDE_CONFIG_DIR` (default `~/.claude`).
- Update applicable Codex `AGENTS.override.md` files too.

## Use

- Before work: clone the configured `https://github.com/OWNER/REPO.wiki.git` into a fresh directory (shallow for queries only). Read `Home.md` if present, then relevant pages. Search Markdown as needed.
- During work: update the matching page with verified findings, scope, and evidence. If the Wiki uses a maintained index, add one line per new page.
- After work: check the staged diff for secrets, personal or customer data, and audience. Run existing secret checks too. Commit once if changed. Auto mode runs `scripts/publish-wiki <clone>`; manual mode reports the draft path.
- `kb publish <clone>`: verify both remote URLs and review again. For `kb.migration` drafts, recheck the audience. Report the commit and page URLs, or the retained draft path. On index conflicts, reapply in a fresh clone and keep both distinct entries.

## Migrate

On explicit `kb migrate [path ...]`, inspect curated Codex `memories` / `memories_v2`, matching Claude project memory, and supplied paths. Exclude transcripts and material with uncertain scope.

Verify evidence and audience, then merge reusable findings into existing pages. Mark the clone with `git config --local kb.migration true`. Publish only to a verified private or internal Wiki when all its readers may see the material. Otherwise keep a draft. Report counts and page URLs.
