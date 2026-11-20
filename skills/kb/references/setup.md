# Setup

Settle: project directory, KB directory, readership, and for Git-backed KBs the upstream URL and publication mode (`auto` default, or `confirm`). Reuse, clone, or create the directory. Warn if publication widens readership.

Write the instruction in the project's `AGENTS.md`, or globally (naming the absolute project directory) when asked or the project file is not editable. Make sure every agent in use loads it; e.g. Claude Code reads `CLAUDE.md`, so import `@AGENTS.md` there. Preserve other content. The KB path may be absolute, project-relative, or an environment variable.

For Git-backed KBs, offer a secretlint pre-commit hook once; install it only if it runs here. Record the choice.

Example:

> Always load the kb skill for team memory in this project. KB: `$PLATFORM_KB_DIR`, cloned from `https://github.com/example/platform.wiki.git`, readable by the Platform team. Publication: auto. secretlint hook: yes. State the resolved KB path before use.
