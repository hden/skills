# Skill Authoring

Use this guide when adding or revising skills in this repository.

## Required Structure

Each skill lives in its own directory:

```text
skills/<skill-name>/
  SKILL.md
```

`SKILL.md` must start with YAML frontmatter:

```markdown
---
name: skill-name
description: What the skill does. Use when an agent needs to...
---
```

The folder name and `name` should match exactly.

## Optional Resources

Add optional resources only when they directly support the skill:

- `scripts/`: executable helpers for repeatable or fragile operations.
- `references/`: longer supporting docs loaded only when needed.
- `assets/`: templates, static files, or binary resources used in outputs.
- `agents/openai.yaml`: agent UI metadata when needed.

Do not add README files, changelogs, or implementation notes inside individual skill folders.

## Writing Guidelines

- Write instructions for another coding agent, not for an end user.
- Keep the main workflow in `SKILL.md` short and imperative.
- Put all trigger cues in the frontmatter `description`.
- Prefer concise examples over broad explanations.
- Link directly from `SKILL.md` to every reference file that may be needed.
- Keep reference files one level deep.

## Review Checklist

Before finishing a skill change:

- Confirm `skills/<skill-name>/SKILL.md` exists.
- Confirm the frontmatter has `name` and `description`.
- Confirm the folder name matches `name`.
- Confirm referenced resource files exist.
- Run changed scripts with representative inputs.
- Run `npx skills add . --list` when the CLI is available.
