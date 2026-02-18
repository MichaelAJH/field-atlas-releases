# User Guide

This guide walks through everything you can do in Field Atlas.

---

## Searching

1. Type a research topic into the query bar at the top of the window (e.g. "transformer architectures for protein folding").
2. Press **Enter**.
3. Field Atlas expands your query into multiple search variants, searches Semantic Scholar, and builds a citation graph. The graph appears in **3-5 seconds**.
4. A background process then enriches the graph with additional cited papers, semantic relevance scores, fundamental paper identification, and field keywords. This takes 10-30 seconds and updates automatically — you can start exploring immediately.

## The Citation Graph

Papers are shown as **circles** (nodes) connected by **directed edges** (citation links).

- **Node size** reflects the paper's PageRank score (larger = more structurally important).
- **Node color** indicates the cluster the paper belongs to (related papers share a color).
- **Vertical position** is chronological — older papers at the top, newer papers at the bottom. Year markers appear along the left edge.

### Navigation

- **Zoom**: scroll wheel or trackpad pinch.
- **Pan**: click and drag on empty space.
- **Center on a paper**: click a paper's name in the side panel — the graph will zoom and center on it.
- **Open on Semantic Scholar**: click a node directly in the graph to open its Semantic Scholar page in your browser.

### Edges

Edges are kept very faint by default to reduce visual clutter. When you hover a node:

- **Outgoing edges** (papers this node cites) highlight in **indigo**.
- **Incoming edges** (papers that cite this node) highlight in **green**.

## AI Summaries and Relations

### Paper Summaries

Hover over any node in the graph. After a brief moment, a tooltip appears with:
- The paper's title, authors, and year.
- An **AI-generated summary** (50-80 words) of the paper's abstract.

Summaries are generated on demand and cached — the first hover may take a second or two, but subsequent hovers are instant.

### Citation Relationships

Hover over an **edge** (the line between two nodes). A tooltip explains **why** one paper cites the other, based on the abstracts of both papers.

### Tooltip Behavior

- Tooltips **stay open** when you move your mouse over them, so you can read and select text.
- Moving to a different node switches the tooltip after a short delay (300ms), preventing flicker when passing over intermediate nodes.

## Side Panel

The panel on the right shows ranked lists of papers and field metadata.

### Paper Rankings

Papers are ranked by a weighted composite score combining:
- **Relevance** — semantic similarity to your original query.
- **PageRank** — structural importance in the citation network.
- **Centrality** — eigenvector centrality (connectedness).

### Professionality Presets

Three preset weight configurations are available:

| Preset | Relevance | PageRank | Centrality | Best for |
|--------|-----------|----------|------------|----------|
| **Overview** | 70% | 20% | 10% | Getting started in a new field |
| **Balanced** | 40% | 35% | 25% | General exploration |
| **Expert** | 15% | 50% | 35% | Finding foundational work |

### Weight Sliders

Below the presets, manual sliders let you adjust the three weights continuously. The ranking updates in real time as you drag.

### Fundamentals

A list of papers identified as **foundational** to the field. The score combines PageRank, raw citation count, and publication age (older, highly-cited, structurally important papers rank highest).

### Methodologies / Keywords

Field-specific keywords extracted from paper titles. These help you quickly learn the terminology and key techniques of the field.

## Query Toggles

When your query is expanded into multiple search variants, each variant appears as a **toggle checkbox** in the side panel. Uncheck a variant to hide the papers that were found by that specific search — useful for narrowing the graph to a particular facet of the topic.

Papers found by multiple variants remain visible as long as at least one of their source variants is checked.

## Find and Add Papers

### Find (in-graph search)

Click the **Find** button (or use the search bar when it's in Find mode) to search for papers already in the current graph by title. Results appear as autocomplete suggestions — click one to center the graph on that paper.

### Add (external search)

Switch to **Add** mode to search Semantic Scholar for papers not currently in the graph. Select a result to add it, along with its related papers. Graph metrics are automatically recomputed.

## Export and Load

### Export

Click the **Export** button to save your entire session as a JSON file. This captures:
- All papers and citation edges.
- Query variants and toggle states.
- Ranking weights and presets.
- Fundamental papers and methodology keywords.

The file is named `field_atlas_<your query>.json`.

### Load

Click the **Load** button and select a previously exported JSON file. The full session is restored — graph, side panel, toggles, weights, and all.

## Settings

Open the Settings modal (gear icon) to configure your LLM provider:

### Ollama (default)
- Free, runs locally.
- Requires Ollama to be installed and running (`ollama serve`).
- Select your preferred model (llama3, mistral, etc.).

### Claude
- Requires an Anthropic API key.
- Enter the key in Settings and test the connection.

### OpenAI
- Requires an OpenAI API key.
- Uses GPT-4o-mini by default.

Use the **Test Connection** button to verify that the selected provider is working before closing the modal. If no LLM is available, Field Atlas still works — graph construction and structural analysis don't require an LLM. Only AI summaries, query expansion, and keyword extraction are affected, and these fall back to text-based alternatives when possible.
