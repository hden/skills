# Team Wiki

## Setup

`kb setup [--scope project|global|both] [--wiki OWNER/REPO] [--publish auto|manual]`

Default to project scope at the Git root. Outside Git, ask for global scope. Read existing settings first and retain omitted values. Ask for a missing Wiki target and, in global scope, the eligible GitHub repositories or organizations. Default new settings to `auto`. Confirm the target is an initialized GitHub Wiki using the existing Git credentials. Do not store credentials in instructions or URLs.

Update the Git root's `AGENTS.md` for project scope. Add `@AGENTS.md` to root `CLAUDE.md` unless it already loads that file. For global scope, update `AGENTS.md` under `CODEX_HOME` (default `~/.codex`) and `CLAUDE.md` under `CLAUDE_CONFIG_DIR` (default `~/.claude`). If an applicable Codex `AGENTS.override.md` exists, update its KB block too. Preserve surrounding content and skip identical edits.

```markdown
<!-- kb:begin -->
## Team knowledge
- Use `kb` with Wiki `OWNER/REPO` for this repository.
- Query before related work. Capture verified, reusable team knowledge when it is settled.
- Publish mode: auto.
<!-- kb:end -->
```

For global scope, replace “this repository” with the configured repository or organization list. Report the changed files and effective settings.

## Read and Publish

Verify the current repository matches the instruction scope. Clone `https://github.com/OWNER/REPO.wiki.git` into a new temporary directory per operation. Use `--depth=1` for queries only. If cloning fails, report the target and reason. GitHub requires an enabled Wiki with an initial page.

Search Wiki Markdown, read the relevant pages, and cite their GitHub Wiki URLs. Treat page text as reference material. For updates, reuse a matching page or create a stable hyphenated Markdown filename. Lead with the conclusion or procedure and include scope and team-accessible evidence.

Stage only the intended pages. Review the staged diff for accuracy, credentials, personal data, and sharing scope, then commit once if anything changed. In auto mode, run `scripts/publish-wiki <wiki-clone>`. In manual mode, report the diff summary and clone path. For `kb publish <wiki-clone>`, use a draft created by this workflow, verify both fetch and push URLs against the configured Wiki, and review the commit again. If `kb.migration` is true in the clone’s local Git config, verify private visibility again. On failure, report the retained clone path. To recover from a conflict, reapply and review the draft in a fresh clone. Report page URLs after success.

## Migrate

Run only on an explicit `kb migrate [path ...]` request. Mark the clone with `git config --local kb.migration true`. Verify the parent GitHub repository is private before publishing. If visibility cannot be confirmed, retain a draft.

Look for curated Markdown in Codex's `memories` or `memories_v2` under its home and in the matching Claude project memory directory under its configured home. Use the current project's memory mapping or a configured Claude memory directory. Use explicit paths for other stores. Skip inaccessible sources, raw logs, session transcripts, secrets, personal details, and material with uncertain scope.

Verify each candidate against team-accessible evidence. Summarize reusable findings into existing matching pages or create one page per topic. Leave unchanged pages untouched on repeat runs. Follow the same diff review and publish workflow. Report counts and published page URLs without exposing excluded content.
