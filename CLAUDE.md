# Knowledge Base — Schema

> **Portability note:** This file is named `CLAUDE.md` for Claude Code. Rename it to match your LLM agent's convention (e.g. `AGENTS.md` for Codex). The instructions are AI-agnostic.

This is an LLM-maintained knowledge base. The LLM writes and maintains all wiki content. The human curates sources, directs analysis, and asks questions. All data is stored as plain files in universal formats (markdown, images) — the human owns the data and can use any AI agent or tool over it.

## Architecture

Three layers:

- **`raw/`** — Immutable source documents. Articles, papers, images, data files. The LLM reads from these but **never modifies them**. This is the source of truth.
- **`wiki/`** — LLM-generated and LLM-maintained markdown files. Summaries, entity pages, concept pages, comparisons, synthesis. The LLM owns this layer entirely.
- **`output/`** — Generated artifacts (reports, slide decks, charts). These are outputs of Q&A and analysis operations.

## Wiki conventions

### Page format

Every wiki page must have YAML frontmatter:

```yaml
---
tags: [topic-a, topic-b]
date: YYYY-MM-DD
sources: 3
---
```

- `tags`: relevant topic tags
- `date`: creation date of the page
- `sources`: count of raw sources that contributed to this page

### Links

Use `[[wikilinks]]` for all internal links. Never use `[text](path.md)` style.

### Page structure

Each page should follow this pattern:

```markdown
---
frontmatter
---

# Page Title

Main content with [[wikilinks]] to related concepts.

## Sources

- [[raw/articles/source-file]]
```

### Special files

- **`wiki/index.md`** — Content catalog. Every wiki page listed with a link, one-line summary, and metadata. Organised by category. The LLM reads this first when answering queries.
- **`wiki/overview.md`** — Top-level synthesis page. A narrative that ties together the main themes, key findings, open questions, and tensions across all sources. Not a table of contents — that's the index. Update this whenever an ingest shifts the big picture.
- **`wiki/log.md`** — Append-only chronological record of operations. Each entry uses the format `## [YYYY-MM-DD] type | Title` where type is one of: `ingest`, `query`, `lint`, `update`. This format is grep-friendly: `grep "^## \[" wiki/log.md | tail -5`.

## Workflows

### Ingest (adding new sources)

1. Read the new source in `raw/`
2. Discuss key takeaways with the user
3. Write a summary page in `wiki/sources/`
4. Update `wiki/index.md`
5. Create or update relevant entity/concept pages across the wiki
6. Update `wiki/overview.md` if the new source shifts the big picture
7. Append an entry to `wiki/log.md`

A single source may touch 10-15 wiki pages.

See `_prompts/compile-wiki.md` for initial compilation and `_prompts/update-wiki.md` for incremental updates.

### Query (answering questions)

1. Read `wiki/index.md` to find relevant pages
2. Read the relevant wiki articles
3. Synthesize an answer with citations back to wiki pages
4. Output as a markdown file in `output/reports/`, or as slides (Marp), charts (matplotlib), or other formats as requested
5. Optionally file valuable answers back into the wiki as new pages — explorations should compound
6. Append an entry to `wiki/log.md`

### Lint (health checks)

1. Scan all wiki articles
2. Check for: contradictions, stale claims, orphan pages, missing cross-references, broken links, data gaps, concepts mentioned but lacking their own page
3. Suggest new questions to investigate and new sources to look for
4. Report findings in `output/reports/lint-report.md`
5. Append an entry to `wiki/log.md`

## File locations

| Directory | Purpose |
|-----------|---------|
| `raw/articles/` | Web-clipped articles, blog posts |
| `raw/papers/` | Academic papers, whitepapers |
| `raw/images/` | Diagrams, screenshots, figures |
| `raw/assets/` | Downloaded image attachments |
| `wiki/` | LLM-maintained knowledge base |
| `wiki/sources/` | Per-source summary pages |
| `output/reports/` | Q&A reports and lint reports |
| `output/slides/` | Marp-format slide decks |
| `output/charts/` | Generated charts and visualizations |
| `_prompts/` | Reusable prompt templates |
| `docs/` | Usage guide and founding documents |

## Raw source naming convention

Files in `raw/` follow: `YYYY-MM-DD_short-slug.ext` — see `raw/README.md` for details.

## Search tooling

At small scale (~100 sources), reading `wiki/index.md` first is sufficient for finding relevant pages. As the wiki grows, consider adding a dedicated search tool. [qmd](https://github.com/tobi/qmd) is a good option: local markdown search with hybrid BM25/vector search and LLM re-ranking, available as both CLI and MCP server. You can also build a simple search script — the LLM can help with that as the need arises.

## Important rules

- **Never modify files in `raw/`** — they are immutable source documents.
- **Always update `wiki/index.md`** after creating or modifying wiki pages.
- **Always append to `wiki/log.md`** after any operation (ingest, query, lint).
- **Use `[[wikilinks]]`** for all internal links, never markdown-style links.
- **Add YAML frontmatter** to every wiki page.
- **Note contradictions** — if sources disagree, document both sides with citations.
- **Don't invent information** — if something is mentioned but unexplained, flag it as a gap.
- **Image handling** — LLMs can't read markdown with inline images in one pass. When processing image-heavy sources, read the text first, then view referenced images separately (e.g. using the Read tool on each image file) to gain additional context. Embed relevant images in wiki pages with `![[raw/images/filename.png]]` or `![[raw/assets/filename.png]]`.
