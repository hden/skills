# Agents

| Agent | Project instructions | Global instructions | Own memory |
|---|---|---|---|
| Codex | `AGENTS.md` (`AGENTS.override.md` wins if present) | `$CODEX_HOME/AGENTS.md` (`~/.codex`) | `$CODEX_HOME/memories/`, `memories_v2/` |
| Claude Code | `CLAUDE.md`, which must import `@AGENTS.md` | `~/.claude/CLAUDE.md` | `~/.claude/projects/<project>/memory/` |

Others mostly read `AGENTS.md`. Keep the kb configuration in `AGENTS.md` and point other files to it.
