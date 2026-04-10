# CLAUDE.md

This repo is a compiled knowledge base for daily reading on LLM and agent topics.

Operating rules:

1. Treat `raw/` as immutable source material.
2. Create or update one article card per meaningful source in `wiki/articles/`.
3. Merge reusable ideas into `wiki/concepts/` instead of leaving everything inside article pages.
4. Create `wiki/maps/` pages only when a topic has become a stable navigation entry point.
5. Keep `index.md` thin and `log.md` chronological.
6. Prefer synthesis, comparison, and backlinks over long copied summaries.
7. When a claim is uncertain, keep the uncertainty explicit and point back to the source file in `raw/`.

Default workflow:

1. inspect `index.md`
2. inspect relevant `wiki/` pages
3. inspect the corresponding source in `raw/`
4. update article page
5. merge relevant changes into concept or map pages
6. append a short note to `log.md`
