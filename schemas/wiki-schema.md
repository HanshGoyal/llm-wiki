# LLM Wiki Schema

This file instructs the LLM on how to maintain the wiki.

## Directory Structure

```
llm-wiki/
├── raw/           # Immutable source documents (markdown, PDFs, etc.)
├── wiki/          # LLM-generated pages
│   ├── index.md   # Catalog of all pages
│   ├── log.md     # Chronological activity log
│   ├── entities/  # People, places, organizations
│   ├── concepts/  # Topics, ideas, theories
│   ├── sources/   # Source summaries
│   ├── analyses/  # Your questions and synthesized answers
│   └── comparisons/
└── schemas/       # Configuration files
```

## Page Types

### Source Pages (`wiki/sources/`)
- One page per source document
- Include: title, date, key takeaways, quotes, synthesis
- Frontmatter: `date`, `source_type`, `tags`

### Entity Pages (`wiki/entities/`)
- People, places, organizations, products
- Cross-reference all sources mentioning this entity
- Frontmatter: `type`, `tags`

### Concept Pages (`wiki/concepts/`)
- Topics, theories, ideas
- Link related entities and sources
- Frontmatter: `tags`

### Analysis Pages (`wiki/analyses/`)
- Answers to your questions
- Should be filed back into wiki for compounding

## Workflows

### Ingest a Source
1. Read the source from `raw/`
2. Create/update source page in `wiki/sources/`
3. Extract entities → create/update pages in `wiki/entities/`
4. Extract concepts → create/update pages in `wiki/concepts/`
5. Update `wiki/index.md` with new pages
6. Append entry to `wiki/log.md`

### Answer a Query
1. Read `wiki/index.md` to find relevant pages
2. Read relevant pages
3. Synthesize answer
4. **File answer as new page in `wiki/analyses/`**
5. Update `wiki/index.md`
6. Append to `wiki/log.md`

### Lint the Wiki
- Check for contradictions between pages
- Find stale claims superseded by new sources
- Find orphan pages with no inbound links
- Find concepts mentioned but lacking pages
- Suggest new sources to find
- Append lint results to `wiki/log.md`

## Formatting

### Log Entries
```
## [YYYY-MM-DD] ingest | Source Title
## [YYYY-MM-DD] query | Your question summary
## [YYYY-MM-DD] lint | Health check results
```

### Page Frontmatter
```yaml
---
title: Page Title
date: 2026-04-21
tags: [tag1, tag2]
---
```

## Notes

- Never modify raw sources
- Always update cross-references when adding new content
- File valuable answers back into the wiki
- Use simple `index.md` search before using vector search