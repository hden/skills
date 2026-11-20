# Team Wiki

## Setup

`kb setup [--scope project|global|both] [--wiki OWNER/REPO] [--publish auto|manual]`

Default to project scope and auto publish. Keep existing values for omitted options. Ask for a missing Wiki or scope, and for eligible repos or orgs in global scope. Verify the initialized Wiki with existing Git credentials.

Write one managed line between `<!-- kb:begin -->` and `<!-- kb:end -->`:

> Read the `kb` skill for team knowledge in `OWNER/REPO`.

Add the eligible repos or orgs for global scope and `publish=manual` only when selected. Preserve surrounding text and skip identical edits. Report changed files.

- Project: Git-root `AGENTS.md`. Add `@AGENTS.md` to root `CLAUDE.md` if needed.
- Global: `AGENTS.md` in `CODEX_HOME` (default `~/.codex`), and `CLAUDE.md` in `CLAUDE_CONFIG_DIR` (default `~/.claude`).
- Update the managed line in applicable Codex `AGENTS.override.md` files too.

## Use

Query before related work. Capture verified, reusable team knowledge when settled.

- Clone `https://github.com/OWNER/REPO.wiki.git` into a fresh temporary directory, shallow for queries only. Report clone failures.
- Search Markdown and cite Wiki URLs. Reuse topic pages. Lead with the conclusion or procedure, then give scope and evidence.
- Check the intended diff for accuracy, secrets, personal data, and audience. Commit once. Auto mode runs `scripts/publish-wiki <clone>`; manual mode reports the draft path.
- `kb publish <clone>`: verify both remote URLs and review the draft again. If `kb.migration` is set, reconfirm private visibility. Report published URLs or the retained draft path. Resolve conflicts in a fresh clone.

## Migrate

On explicit `kb migrate [path ...]`, inspect curated Codex `memories` / `memories_v2`, the matching Claude project memory, and supplied paths. Skip transcripts, personal data, secrets, and uncertain material.

Verify team-accessible evidence and merge reusable findings into existing pages. Mark the clone with `git config --local kb.migration true`. Keep a draft unless the Wiki is verified private. Report counts and published URLs.
