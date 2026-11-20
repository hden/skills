# Agents

Where each agent reads instructions and keeps its own memory. For agents not listed, check their documentation; most read `AGENTS.md`.

| Agent | Project instructions | Global instructions | Own memory |
|---|---|---|---|
| Codex | `AGENTS.md` (an `AGENTS.override.md` in the same directory takes precedence) | `$CODEX_HOME/AGENTS.md` (default `~/.codex`) | `$CODEX_HOME/memories/` |
| Claude Code | `CLAUDE.md`; it does not read `AGENTS.md` unless `CLAUDE.md` imports `@AGENTS.md` | `~/.claude/CLAUDE.md` | `~/.claude/projects/<project>/memory/` |

Write the kb configuration once in `AGENTS.md` and make every other agent's file point to it, so the settings do not drift.
