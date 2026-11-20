# Page template

Use when the KB has no page convention yet. Write in the KB's language.

````markdown
# <Topic>

<One or two sentences: what a reader learns from this page.>

## Observations

Verified facts only, each with evidence and the date it was checked.

- <fact> (evidence: <PR, ticket, file path, or command>; checked: YYYY-MM-DD)

## Hypotheses

Unverified ideas, each with the reasoning. Move an item to Observations once verified.

- <idea> (reason: <why you think so>)

## Related

- <related pages or external links>
````

- Drop "Hypotheses" when empty.
- File name: lowercase kebab-case, e.g. `ci-cache-misses.md`.
- Index entry: one line, `- [<Topic>](<link>) — <what it tells you>`, using the link style of the storage (see its reference).
