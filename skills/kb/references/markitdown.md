# MarkItDown

MarkItDown converts supported sources to Markdown. Some web pages cannot be converted or produce incomplete output. In those cases, use another available source format, summarize verified content, or keep a source link.

## Setup

The skill bundles a Dockerfile at `assets/Dockerfile.markitdown`.

Build it from the skill directory:

```sh
docker build -f assets/Dockerfile.markitdown -t markitdown:local .
```

Then use `scripts/markitdown` from a scratch directory outside the KB:

```sh
path/to/skills/kb/scripts/markitdown input.pdf -o output.md
```

The wrapper preserves host absolute paths, mounts input directories read-only, mounts output directories read-write, and runs the `markitdown:local` image.

## Review Policy

Never accept converted markdown blindly. The agent must inspect the output and decide whether it is useful.

Accept when:

- title or topic is identifiable
- body has practical substance
- headings and paragraphs are mostly preserved
- UI, navigation, script, or comment noise does not dominate

If accepted, keep markdown as a supplemental artifact such as `markitdown.md`.

Review both the source and the converted output for sensitive content before copying any material into the KB.
