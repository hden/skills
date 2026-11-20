# Setup

For `kb setup`, identify the project directory, KB directory, and intended readership. Reuse an existing Markdown directory or create the chosen directory for a new KB. Confirm any missing values. Check whether publication broadens who can read the files.

Add or update a short team-memory instruction in project `AGENTS.md`. If it cannot be edited, place the same instruction in the agent's global instructions and name the absolute project directory it applies to. Preserve unrelated instructions. Use an absolute KB path, a path relative to the named project directory, or an environment variable containing the path. If a configured variable is unset, ask for the path before using the KB.

Example project instruction:

> Use the kb skill for team memory. The KB is at `$PLATFORM_KB_DIR` and is readable by the Platform team.

If this project uses multiple KBs, give each a name for switching and record a default if requested. If the KB is rendered by a known platform, record it and follow the appropriate reference from the skill.

To replace an older Wiki setting, confirm the corresponding filesystem directory and readership, then update the old instruction.

Git synchronization is automatic when the KB branch has a configured upstream. Record any instruction to keep updates unpublished or require confirmation before publishing.
