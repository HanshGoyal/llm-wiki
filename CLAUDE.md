# CLAUDE.md - LLM Wiki Agent Guide

This file provides guidance to LLM agents working with this wiki.

## Project Overview

This is a **hybrid LLM Wiki** combining:
- **Karpathy's LLM Wiki** pattern - AI synthesizes and maintains knowledge
- **Stephen Kanegan's Obsidian** structure - organized folders and templates

## Core Philosophy

- **Raw sources** in `raw/` are immutable - never modify them
- **Wiki pages** are AI-generated synthesis - LLM creates and maintains
- **Human role**: Add sources, ask questions, think about meaning
- **LLM role**: Do all the work - ingest, synthesize, cross-reference, maintain

## Directory Structure

```
llm-wiki/
├── raw/                    # Your sources - ADD FILES HERE
├── wiki/
│   ├── index.md           # Catalog - check this first
│   ├── log.md             # Activity history
│   ├── daily/             # Session notes
│   ├── templates/         # Page templates
│   ├── sources/           # Source summaries
│   ├── entities/          # People, places, organizations
│   ├── concepts/          # Topics, ideas, theories
│   ├── analyses/         # Answers to questions
│   └── comparisons/       # Comparison tables
└── schemas/
    └── wiki-agent-guide.md  # Detailed instructions (READ THIS)
```

## Key Workflows

### 1. INGEST - Adding Sources
1. User drops file in `raw/`
2. Read the source
3. Create source page in `wiki/sources/`
4. Extract/update entities in `wiki/entities/`
5. Extract/update concepts in `wiki/concepts/`
6. Update `wiki/index.md`
7. Append to `wiki/log.md` with format: `## [YYYY-MM-DD] ingest | Title`
8. Create/update daily note in `wiki/daily/`

### 2. ANSWER - Responding to Questions
1. Read `wiki/index.md` to find relevant pages
2. Read those pages
3. Synthesize answer
4. **File answer as new page in `wiki/analyses/`** (critical!)
5. Update index.md
6. Append to log.md: `## [YYYY-MM-DD] query | Question summary`

### 3. DAILY - Session Notes
At end of every session:
- Create `wiki/daily/YYYY-MM-DD.md`
- Document: learnings, questions, wiki updates, ideas
- Template in `wiki/templates/daily-template.md`

### 4. LINT - Health Check
Periodically check for:
- Contradictions between pages
- Stale information
- Orphan pages (no inbound links)
- Missing concepts
- Broken references

## Critical Rules

1. **ALWAYS include Reference section** - Every wiki page must link to its raw source: `[[raw/filename]]`
2. **File answers back** - Never let synthesized knowledge disappear into chat
3. **Use templates** - Check `wiki/templates/` for format standards
4. **Log consistently** - Use prefix format for grep-ability
5. **Cross-reference everything** - Link related entities, concepts, sources

## Page Template

Use this structure:

```markdown
---
title: {Title}
date: {YYYY-MM-DD}
tags: []
---

## Key Content

{...}

## Connected Pages

- [[entities/...]]
- [[concepts/...]]
- [[sources/...]]

## Reference

[[raw/filename]]
```

## Important Files

- `wiki/index.md` - Start here for any query
- `wiki/log.md` - Check recent activity
- `wiki/daily/` - Session tracking
- `wiki/templates/` - Format standards

## Before Responding

1. Check `wiki/index.md` for relevant pages
2. Read `wiki/log.md` for recent activity
3. Use templates from `wiki/templates/`
4. Always add Reference section

## This Is a Git Repo

The wiki is version-controlled. Commit meaningful changes.