# Advanced Ingest & Knowledge Structuring Workflow

## Overview
This workflow defines the process of transforming raw input (clippings, articles, or logs) into a structured, interconnected knowledge graph within the Wiki.

## Workflow Steps

# Advanced Ingest & Knowledge Structuring Workflow

## Overview
This workflow defines the process of transforming raw input (clippings, articles, or logs) into a structured, interconnected knowledge graph within the Wiki.

## Workflow Steps

### 1. Classification (Identification)
Analyze the input source to determine its nature:
- **Event/News (Low Density)**: News, updates, or time-sensitive events. 
  - *Action*: Create a `summaries/` page. Update `index.md` (Sources) and `log.md`.
- **Fundamental Principle/Technology (High Density)**: Definitions, frameworks, or architectural patterns.
  - *Action*: Proceed to **Atomization**.

### 2. Atomization (Deconstruction)
Break down high-density information into atomic knowledge objects:
- **Summary Layer**: Retrieving context and background into `summaries/`.
- **Concept Layer**: Extracting core definitions, architectures, and logic into `concepts/`.
- **Entity Layer**: Identifying key actors, tools, and protocols, creating entries in `entities/`.

### 3. Graph Integration (Linking)
Establish bidirectional relationships:
- **Vertical Link**: Ensure `summaries/` link to their respective `concepts/`.
- **Horizontal Link**: Ensure `concepts/` reference relevant `entities/` and other `concepts/`.
- **Index Update**: Update `index.md` (Sources, Concepts, Entities) and `entities/` registry.
- **Root Directory Management**: Ensure raw source files are stored in the project root `raw/` directory and not in temporary wiki folders.

### 4. Verification (Validation)
- **Link Check**: Run a lint process to ensure no broken `[[Links]]`.
- **Consistency Check**: Ensure `log.md` tracks the ingestion event.
- **Structure Audit**: Use `ls -R` to verify that files are in their correct permanent directories (`summaries/`, `concepts/`, `entities/`, and root `raw/`) and that no temporary folders (`wiki/raw/`, `wiki/summary/`) remain.

## Decision Matrix
| Input Type | Primary Destination | Secondary Destination |
| :--- | :--- | :--- |
| News/Clip | `summaries/` | `index.md` (Sources) |
| Technical Architecture | `concepts/` | `summaries/` & `entities/` |
| Tool/Protocol | `entities/` | `concepts/` |


## Decision Matrix
| Input Type | Primary Destination | Secondary Destination |
| :--- | :--- | :--- |
| News/Clip | `Summaries/` | `index.md` (Sources) |
| Technical Architecture | `concepts/` | `Summaries/` & `entities/` |
| Tool/Protocol | `entities/` | `concepts/` |
