# LLM Wiki

A persistent, interlinked knowledge base maintained by LLMs.

## Overview

The LLM Wiki is a pattern for building a compounding personal or team knowledge base. Unlike traditional RAG (Retrieval-Augmented Generation) which retrieves information from raw sources on every query, the LLM Wiki **independently builds, maintains, and evolves** a structured collection of markdown files.

The LLM acts as the "programmer" or "maintainer," handling the heavy lifting of summarizing sources, extracting entities, updating cross-references, and flagging contradictions, while you act as the "curator" and "researcher."

## Architecture

The system consists of three layers:

1.  **Raw Sources (`raw/`)**: Immutable source documents (articles, papers, transcripts, etc.) that serve as the single source of truth.
2.  **The Wiki (`wiki/`)**: A directory of LLM-managed markdown files, including summaries, entity pages, and concept pages.
3.  **The Schema (`wiki/assets/schema.md`)**: The set of instructions (the "code") that tells the LLM how to operate, ingest, and maintain the wiki.

## Directory Structure

- `raw/`: Immutable source collection.
- `wiki/`: The active knowledge base.
    - `assets/`: Configuration and schema files.
    - `comparisons/`: Detailed analysis and comparison of different topics or sources.
    - `concepts/`: Pages dedicated to abstract ideas and theories.
    - `entities/`: Pages for specific people, places, or organizations.
    - `index.md`: The master catalog of all wiki pages.
    - `log.md`: A chronological, append-only record of all wiki operations.
    - `queries/`: Notable answers and significant explorations.
    - `summaries/`: Summaries of individual raw sources.

## Core Operations

### 1. Ingest
When a new source is added to `raw/`, the LLM reads it, creates a summary, extracts key entities/concepts, updates the `index.md`, and logs the event in `log.md`.

### 2. Query
Ask questions against the wiki. The LLM searches the index, retrieves relevant pages, synthesively answers, and provides citations. Substantial answers can be saved as new pages in `wiki/queries/`.

### 3. Lint
Periodically, the LLM performs a health check to find broken links, orphan pages, or contradictions between new data and old wiki content.

## Getting Started

1.  Define your domain and preferences.
2.  Place your initial sources in `raw/`.
3.  Use the `llm-wiki` skill (or equivalent instructions) to start the ingestion process.
4.  Browse your evolving knowledge base using an editor like **Obsidian**.
