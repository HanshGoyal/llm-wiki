# LLM Wiki Template

A **hybrid personal knowledge base** combining Karpathy's LLM Wiki automation with Kanegan's Obsidian structure.

## Quick Start

1. **Download or fork** this template
2. **Open in Obsidian** (recommended)
3. **Drop sources** in `raw/`
4. **Ask an LLM** to ingest them
5. **Build knowledge** incrementally

## What This Is

This wiki:
- **Accumulates knowledge** over time (not just RAG)
- **Synthesizes automatically** - LLM updates multiple pages per source
- **Tracks provenance** - every page links to its raw source
- **Has daily notes** - track your learning sessions
- **Uses templates** - consistent format everywhere

## Directory Structure

```
llm-wiki/
├── README.md              # Full guide (you're reading it)
├── CLAUDE.md             # LLM agent instructions
├── .gitignore            # Ignores raw/ and wiki/ by default
├── raw/                  # YOUR SOURCES (add files here)
├── wiki/
│   ├── index.md         # Catalog of all pages
│   ├── log.md          # Activity history
│   ├── daily/          # Session notes
│   ├── templates/       # Page templates
│   ├── sources/        # Source summaries
│   ├── entities/       # People/places/orgs
│   ├── concepts/       # Topics/ideas
│   ├── analyses/      # Answered questions
│   └── comparisons/   # Comparisons
└── schemas/
    ├── wiki-agent-guide.md
    └── wiki-schema.md
```

## How It Works

### Add a Source
```
1. Drop file in raw/
2. Tell LLM: "Ingest [filename]"
3. LLM creates ~10-15 wiki pages
4. Knowledge compounds
```

### Ask Questions
```
1. Ask: "What do I know about X?"
2. LLM searches wiki
3. LLM synthesizes answer
4. Answer filed back → wiki/analyses/
```

### End Sessions
```
1. Tell LLM: "Create daily note"
2. Session documented
3. Patterns emerge over time
```

## Design Principles

| Principle | Why |
|-----------|-----|
| Raw sources immutable | Source of truth |
| Synthesize at ingest | Pay cost once |
| File answers back | Compounding knowledge |
| Track provenance | Always cite sources |
| Log everything | Patterns visible |

## Key Features

- **Templates** in `wiki/templates/`
- **Daily notes** in `wiki/daily/`
- **Reference links** in every page (to raw sources)
- **Dataview-ready** frontmatter

## Resources

- [Karpathy's LLM Wiki Gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [kepano-obsidian](https://github.com/kepano/kepano-obsidian)
- [Obsidian](https://obsidian.md/)

## License

MIT - Use freely, customize as needed.