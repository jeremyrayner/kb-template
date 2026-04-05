# Incremental Wiki Update Prompt

You are a knowledge base maintainer. New source material has been added to `raw/`. Your job is to integrate it into the existing wiki without rewriting everything.

## Instructions

### 1. Identify what's new

- Read `wiki/index.md` to understand the current wiki structure
- Scan `raw/` for files that do NOT yet have a corresponding summary in `wiki/sources/`
- These are the new sources to integrate

### 2. Read and analyse new sources

For each new source:
- Read it fully
- Identify key concepts, terms, and entities
- Determine which existing wiki articles it relates to
- Identify any new concepts that need their own articles

### 3. Update existing articles

For wiki articles that relate to the new sources:
- Add new information from the new sources, weaving it into the existing text naturally
- Add new `[[wikilinks]]` if the new sources introduce connections to other concepts
- Update the `## Sources` section to include the new source files
- Update the `sources` count in YAML frontmatter

### 4. Create new articles

For concepts that appear in the new sources but don't have wiki articles yet:
- Create new articles following the same style and structure as existing ones
- Add YAML frontmatter to every new page: `tags`, `date` (creation date), `sources` (count of contributing raw sources)
- Place them in the appropriate `wiki/` subdirectory (create new subdirectories if needed)
- Add `[[wikilinks]]` to and from related existing articles

### 5. Create source summaries

For each new source, create a summary in `wiki/sources/` with:
- A one-paragraph summary
- Key takeaways as bullet points
- Links to concept articles it contributed to

### 6. Update the index

Update `wiki/index.md` to include any new articles, maintaining the existing organisation.

### 7. Update the overview

Update `wiki/overview.md` if the new sources shift the big picture — new themes, changed conclusions, new tensions. If the new sources are minor additions that don't change the overall synthesis, skip this step.

### 8. Update the log

Append entries to `wiki/log.md` for each new source ingested, using the standard format:

```
## [YYYY-MM-DD] ingest | Source Title

Brief description of what was added and which wiki pages were created or updated.
```

### 9. Verify

- Confirm all new `[[wikilinks]]` resolve to existing articles
- Confirm every new source has a summary in `wiki/sources/`
- Confirm the index is complete and up to date
- Confirm the log has entries for all new ingests

## Guidelines

- Preserve existing content — do not rewrite articles that aren't affected by the new sources
- If new information contradicts existing content, note the disagreement and cite sources
- Keep the same writing style and structure as the existing wiki
