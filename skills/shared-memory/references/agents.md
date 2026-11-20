# Agents

| Agent | Project instructions | Global instructions | Own memory |
|---|---|---|---|
| Codex | `AGENTS.md` (`AGENTS.override.md` wins if present) | `$CODEX_HOME/AGENTS.md` (`~/.codex`) | `$CODEX_HOME/memories/`, `memories_v2/` |
| Claude Code | `CLAUDE.md`; import `@AGENTS.md` there so it loads the configuration | `~/.claude/CLAUDE.md` | `~/.claude/projects/<project>/memory/` |

Others mostly read `AGENTS.md`. Keep the shared-memory configuration in `AGENTS.md` and point other files to it.
