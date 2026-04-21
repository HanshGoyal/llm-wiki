# LLM Wiki - Agent Guide

This file teaches any LLM agent how to maintain and query this personal wiki. Read this before working with the wiki.

## What Is This Wiki?

This wiki is a **persistent, compounding knowledge base** built and maintained by LLMs. Unlike traditional RAG systems that retrieve raw chunks at query time, this wiki **stores synthesized knowledge** that accumulates over time.

- **Raw sources** sit in `raw/` - immutable, never modified
- **Wiki pages** in `wiki/` - LLM-generated summaries, entity pages, cross-references
- When you add a source, the LLM updates many wiki pages at once - not just indexes it

The wiki grows richer with every source and every question. Cross-references already exist. Contradictions are flagged. Synthesis is already done.

## Core Philosophy

The human's job:
- Curate sources (add to `raw/`)
- Ask good questions
- Direct analysis
- Think about what it all means

The LLM's job:
- Read and synthesize sources
- Create and maintain wiki pages
- Update cross-references
- Flag contradictions
- Answer questions from the wiki (not from scratch)
- File valuable answers back into the wiki

## Directory Structure

```
llm-wiki/
├── raw/                    # Source documents (markdown, PDFs, articles)
│   └── [source files]
├── wiki/                   # LLM-generated wiki
│   ├── index.md           # Catalog of all wiki pages
│   ├── log.md             # Chronological activity log
│   ├── entities/          # People, places, organizations
│   ├── concepts/          # Topics, theories, ideas
│   ├── sources/           # Summaries of each source
│   ├── analyses/          # Answers to questions (filed back)
│   └── comparisons/       # Comparison tables
└── schemas/                # Configuration
    └── wiki-schema.md     # Detailed schema (you are here)
```

## Operations

### 1. INGEST - Adding a Source

When user drops a file in `raw/` and asks to process it:

```
Step 1: Read the source
- Open and read the file from raw/
- Understand its key content, claims, entities

Step 2: Create source summary page
- File: wiki/sources/[slugified-title].md
- Include: title, date added, key takeaways (bullet points), notable quotes
- Add frontmatter with tags

Step 3: Extract and update entities
- For each person, place, organization mentioned:
  - If exists: update their entity page with new info
  - If new: create wiki/entities/[slugified-name].md
- Add cross-references between source and entities

Step 4: Extract and update concepts
- For each topic, theory, idea:
  - If exists: update concept page
  - If new: create wiki/concepts/[slugified-concept].md

Step 5: Update index.md
- Add new pages to the catalog with one-line summaries

Step 6: Log the ingest
- Append to wiki/log.md:
  ## [YYYY-MM-DD] ingest | Source Title

Tip: A single source typically touches 10-15 wiki pages.
```

### 2. QUERY - Answering Questions

When user asks a question:

```
Step 1: Find relevant pages
- Read wiki/index.md first for overview
- Search for relevant entities, concepts, sources

Step 2: Read relevant pages
- Open the pages found above
- Understand the current state of knowledge

Step 3: Synthesize answer
- Combine info from multiple pages
- Cite sources with links
- Generate markdown answer

Step 4: FILE THE ANSWER BACK (CRITICAL)
- Save answer to wiki/analyses/[slugified-question].md
- This is what makes knowledge compound!
- Don't let good answers disappear into chat history

Step 5: Update index.md
- Add the new analysis page

Step 6: Log the query
- Append to wiki/log.md:
  ## [YYYY-MM-DD] query | Your question summary

Output formats allowed: markdown, tables, Marp slides, matplotlib charts
```

### 3. LINT - Health Check

Periodically check wiki health:

```
Run these checks:
1. Contradictions - do newer sources conflict with existing pages?
2. Stale info - are any claims outdated by newer sources?
3. Orphans - any pages with no inbound links?
4. Missing pages - concepts mentioned but without dedicated pages?
5. Cross-refs - are links consistent?
6. Gaps - what topics need more research?

Report findings and suggest new sources to find.
Log to wiki/log.md:
  ## [YYYY-MM-DD] lint | Findings summary
```

## Log Format

Always use consistent prefixes for parseability:

```markdown
## [2026-04-21] ingest | Article Title
## [2026-04-21] query | How does X relate to Y?
## [2026-04-21] lint | Found 2 contradictions, 3 orphans
```

Unix utility: `grep "^## \[" wiki/log.md | tail -5`

## Page Templates

### Source Page
```markdown
---
title: Source Title
date: 2026-04-21
source_type: article|paper|book|video|conversation
tags: [tag1, tag2]
---

## Key Takeaways

- Point 1
- Point 2
- Point 3

## Notable Quotes

> "Quote here"

## Synthesis

Summary of how this fits with existing knowledge...

## Sources

- [[entities/person-name]]
- [[concepts/concept-name]]
```

### Entity Page
```markdown
---
title: Entity Name
type: person|place|organization|product
date: 2026-04-21
tags: []
---

## Overview

Brief description...

## Appears In

- [[sources/source-name]]
- [[sources/another-source]]

## Related Entities

- [[entities/related-entity]]

## Related Concepts

- [[concepts/concept]]
```

### Concept Page
```markdown
---
title: Concept Name
date: 2026-04-21
tags: []
---

## Definition

What it is...

## Key Points

- Point 1
- Point 2

## Connected Entities

- [[entities/entity]]

## Sources

- [[sources/source]]
```

## Important Rules

1. **Never modify raw sources** - they are immutable
2. **Always update cross-references** - when you add content, link it
3. **File answers back** - don't let synthesized knowledge disappear
4. **Keep log entries consistent** - enables unix tools
5. **Flag contradictions** - note when new sources conflict with old claims
6. **Use index.md first** - before any search, check the index
7. **One source, many updates** - expect to touch 10-15 pages per ingest
8. **Human defines scope, LLM fills details** - user provides sources and questions

## Scaling

At small scale (~100 sources, hundreds of pages):
- index.md is sufficient for retrieval
- No vector search needed

At larger scale:
- Consider tools like qmd for hybrid BM25/vector search
- Knowledge graph for deterministic retrieval first, then LLM reasoning

## This Is a Git Repo

The wiki is a git repository. You get version history, branching, and collaboration for free. Commit changes periodically.

---

Read `wiki/index.md` to see current state. Read `wiki/log.md` for history. Begin working!