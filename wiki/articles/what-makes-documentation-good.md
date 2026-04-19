# What Makes Documentation Good

## Source

- URL: https://cookbook.openai.com/articles/what_makes_documentation_good
- Author: OpenAI
- Published: 2023-11-07 inferred from local clone git history
- Captured: 2026-04-16
- Raw file: `raw/sources/2023/2023-11-07-what-makes-documentation-good.md`
- Imported from workspace path: `../openai-cookbook/articles/what_makes_documentation_good.md`

## Main Claims

- Good documentation should be easy to skim, not just correct
- Titles, section structure, and topic sentences should help readers find the right answer quickly
- Takeaways should appear up front instead of after a long buildup
- Clarity comes from short paragraphs, simple sentences, consistent terminology, and unambiguous phrasing
- Documentation should stay broadly helpful by explaining terminology, offering likely fixes, and avoiding jargon or hidden assumptions

## Why It Matters

This article is less about documentation style in the abstract and more about making repo-local knowledge usable by another agent or human. If the knowledge base is meant to survive interruption, the pages have to be skimmable, self-contained, and explicit about the outcome first.

## Relation To Existing Concepts

- [Agent Knowledge Compilation](../concepts/agent-knowledge-compilation.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)

## Tensions Or Disagreements

- Applying these rules everywhere can make docs feel repetitive if the repo already has a strong shared vocabulary
- A strict skim-first style can overcompress nuance if the topic needs careful framing
- Documentation advice is easy to agree with but hard to enforce consistently across many files

## Open Questions

- Which repo docs should be held to this standard most strictly: AGENTS, task files, concept pages, or article cards
- How much structural polish is enough before the maintenance cost outweighs the readability gain
- What minimal doc-quality rules should be encoded in repo policy instead of left to judgment

## Merge Candidates

- knowledge pages should put the takeaway up front and use informative section headings
- article cards should be written for skimming first, not only for completeness
- repository-local docs should avoid vague nouns, hidden assumptions, and long buildup before the point
