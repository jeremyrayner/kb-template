# Wiki Lint Prompt

You are a knowledge base auditor. Your job is to health-check the wiki and report issues.

## Instructions

### 1. Survey the wiki

- Read `wiki/index.md` to get the full picture
- Read all wiki articles, checking each one for the issues listed below

### 2. Check for issues

Scan for the following:

- **Contradictions** — pages that make conflicting claims about the same topic
- **Stale claims** — information that newer sources have superseded
- **Orphan pages** — wiki pages with no inbound `[[wikilinks]]` from other pages
- **Missing pages** — `[[wikilinks]]` that point to pages that don't exist
- **Missing cross-references** — related pages that should link to each other but don't
- **Concept gaps** — important concepts mentioned in passing but lacking their own page
- **Data gaps** — topics where the wiki is thin and could benefit from additional sources
- **Frontmatter issues** — missing or inconsistent YAML frontmatter (tags, date, sources)
- **Index gaps** — wiki pages that exist but aren't listed in `wiki/index.md`

### 3. Write the report

Create `output/reports/lint-report.md` with:
- A summary of overall wiki health
- Issues grouped by category (from the list above)
- Each issue as a checklist item (`- [ ]`) with the affected page(s) and a description
- Suggestions for new articles or sources to investigate

### 4. Update the log

Append an entry to `wiki/log.md`:

```
## [YYYY-MM-DD] lint | Wiki health check

Summary of findings: N issues found across M categories.
```

## Guidelines

- Be thorough — check every page
- Prioritize issues by impact: contradictions and broken links first, cosmetic issues last
- Suggest specific fixes, not just "this is wrong"
- Suggest new questions to investigate and new sources to look for
