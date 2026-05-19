# Skills

A repository for managing multiple agent skills in one place.

Skills are reusable instruction packages for coding agents. This repository follows the common Agent Skills layout used by the `npx skills` ecosystem.

## Layout

```text
skills/
  example-skill/
    SKILL.md
    agents/
      openai.yaml
    scripts/
    references/
    assets/
docs/
kb/
```

Only `SKILL.md` is required for each skill. Add `scripts/`, `references/`, and `assets/` only when they make the skill more reliable or easier to maintain.

## Creating a Skill

1. Create `skills/<skill-name>/SKILL.md`.
2. Use lowercase hyphen-case for the folder and `name`.
3. Put the trigger behavior in the `description` frontmatter.
4. Keep core workflow instructions in `SKILL.md`.
5. Move detailed material into `references/` and helper automation into `scripts/`.

See [docs/skill-authoring.md](docs/skill-authoring.md) for authoring rules.

## Smoke Check

After adding skills, check that the repository can be discovered:

```sh
npx skills add . --list
```

If publishing to GitHub, consumers should be able to install with:

```sh
npx skills add owner/repo
npx skills add owner/repo --skill skill-name
```
