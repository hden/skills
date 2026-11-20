# Storage: GitHub Wiki

A Wiki is a separate Git repository; sync and publish as in storage-git.

- Upstream: `https://github.com/OWNER/REPO.wiki.git`. The Wiki must already have one page (created in the web UI) before it can be cloned.
- Index: `Home.md` is the landing page; `_Sidebar.md`, if present, is navigation. Add new pages to whichever the Wiki uses.
- Page names: the file name becomes the title and URL (`Some-Page.md` → `/wiki/Some-Page`). Link with `[[Some Page]]` or relative links, matching existing pages.
- Readership follows the repository's visibility: public repositories have public Wikis.
- Page URLs for the report: `https://github.com/OWNER/REPO/wiki/<page>`.
- Some cloud agent environments can only reach repositories, not Wikis. Use a regular repository there.

[GitHub Wiki documentation](https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis)
