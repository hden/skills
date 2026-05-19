# Repository Guidance

## Scope
This repository collects multiple agent skills. Follow this file for all paths in this repository unless a deeper `AGENTS.md` exists.

## Repository Shape
- Put each skill in `skills/<skill-name>/`.
- Every skill must have `skills/<skill-name>/SKILL.md`.
- Optional per-skill resources:
  - `agents/openai.yaml` for UI metadata.
  - `scripts/` for deterministic helpers that should be executed rather than rewritten.
  - `references/` for detailed docs loaded only when needed.
  - `assets/` for templates or binary/static resources used by the skill.
- Use `docs/` for repository-level procedures and `kb/` for raw notes or source material that may later be distilled into skills.

## Skill Authoring
- Use lowercase hyphen-case names with letters, digits, and hyphens only.
- Keep `SKILL.md` concise and procedural. Move detailed references into `references/`.
- `SKILL.md` frontmatter must include only `name` and `description` unless a target agent explicitly requires more.
- Make the `description` the trigger surface: include what the skill does and when an agent should use it.
- Do not add README, changelog, or process notes inside individual skill folders. Put repository documentation under `docs/`.
- Keep references one level deep from `SKILL.md`; avoid nested documentation chains.

## Editing
- Prefer small, reviewable changes that add or improve one skill at a time.
- Use English for repository files and skill instructions unless a skill is explicitly language-specific.
- Default to 2-space indentation when no file-local convention exists.
- Do not introduce host-level dependencies. Prefer repository scripts or portable POSIX shell.

## Validation
- For each changed skill, verify:
  - The folder name matches `name` in `SKILL.md`.
  - `SKILL.md` has valid YAML frontmatter with `name` and `description`.
  - Referenced `scripts/`, `references/`, and `assets/` files exist.
  - Any changed script has been run with a representative input.
- If `npx skills` is available, use `npx skills add . --list` as a repository-level smoke check.
