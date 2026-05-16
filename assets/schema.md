# LLM Wiki Schema & Operational Guidelines

This document defines the structure, conventions, and workflows for maintaining the LLM Wiki.

## 1. Directory Structure

- `raw/`: Immutable source documents (articles, papers, transcripts, etc.).
- `wiki/`: LLM-managed markdown files.
    - `index.md`: The primary catalog of all wiki pages.
    - `log.md`: Append-only chronological record of operations.
    - `assets/`: Configuration, schemas, and supplementary assets.
    - `entities/`: (Optional) Pages for specific entities (people, places, organizations).
    - `concepts/`: (Optional) Pages for abstract concepts and theories.
    - `summaries/`: (Optional) Summary pages for individual raw sources.
- `assets/schema.md`: This document.

## 2. Page Conventions

All wiki pages must include YAML frontmatter for metadata.

### YAML Frontmatter Template
```yaml
---
title: "Page Title"
date: YYYY-MM-DD
source: "[[Source Page Name]]" # or path to raw source
tags: [tag1, tag2]
---
```

### Content Guidelines
- Use Obsidian-style internal links: `[[Page Name]]`.
- Use clear, descriptive headings.
            
## 3. Operational Workflows

### 3.1 Ingesting a Source
**Trigger**: User provides a new file in `raw/` or asks to "ingest [file]".
1. **Read**: Read the raw source file.
2. **Summarize**: Create/update a summary page in `wiki/summaries/` (or `wiki/` if no subdirs used).
3. **Extract Entities/Concepts**: Identify key entities and concepts. Create or update their respective `[[Page Name]]` in `wiki/entities/` or `wiki/concepts/`.
4. **Update Index**: Add the new page/summary to `wiki/index.md`.
5. **Log**: Append an entry to `wiki/log.md`: `## [YYYY-MM-DD] ingest | [Source Title]`.

### 3.2 Querying the Wiki
**Trigger**: User asks a question about the knowledge base.
1. **Search**: Consult `wiki/index.md` or search the `wiki/` directory for relevant pages.
2. **Synthesize**: Read relevant pages and formulate a comprehensive answer.
3. **Cite**: Always provide links to the wiki pages used.
4. **Persist**: If the answer creates new knowledge, propose creating a new wiki page.

### 3.3 Linting the Wiki
**Trigger**: User asks to "lint", "check", or "maintain" the wiki.
1. **Link Integrity**: Check for broken `[[links]]`.
2. **Orphan Detection**: Identify pages in `wiki/` with no inbound links.
3. **Consistency Check**: Look for contradictions between new raw sources and existing wiki content.
4. **Completeness**: Identify important concepts mentioned but lacking their own page.
