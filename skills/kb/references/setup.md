# Setup

For `kb setup`, identify the project directory, KB directory, and intended readership. Reuse an existing Markdown directory or create the chosen directory for a new KB. Confirm any missing values. Check whether publication broadens who can read the files.

Use project scope by default. Add or update the team-memory instruction in the project's `AGENTS.md`. Use global scope when requested or when the project file cannot be edited. In global scope, write the instruction in the agent's global instructions and name the absolute project directory it applies to. Preserve unrelated instructions. Use an absolute KB path, a path relative to the named project directory, or an environment variable containing the path. If a configured variable is unset, ask for the path before using the KB.

Example project instruction:

> Always load the kb skill for team memory in this project. The KB is at `$PLATFORM_KB_DIR` and is readable by the Platform team. After loading the skill, verify the resolved KB path and state it before using the KB.
