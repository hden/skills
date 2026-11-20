# kb migrate

Promote team-worthy knowledge from agents' own memories into the KB.

1. Collect sources: paths the user supplies, or curated memory files of the agents in use (e.g. Codex `memories/`, Claude Code's project memory directory). Skip raw transcripts.
2. Select only findings that are reusable for this project and fit the KB's readership. Drop personal preferences and anything whose audience is unclear.
3. Verify each finding still holds, then merge it into existing pages following "While working" in SKILL.md.
4. Publish with `confirm`, whatever the configured mode: migrated material was written for a narrower audience.
5. Leave the source memories in place unless the user asks to remove them.
6. Report the changed pages and the number of findings skipped, without quoting them.
