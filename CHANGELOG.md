# Changelog

All notable changes to Field Atlas are documented here. Versions correspond to tags in both the development and release repositories.

---
## [v0.7.0] - 2026-02-19

- Fix version control to use dev branch and SemVer-like versioning
- First stable beta release


## [v0.6.0] - 2026-02-19

- Continuous Integration (CI) for relases page

## [v0.5.2] — 2026-02-19

- Rebrand to Field Atlas (previously Academia Nav)

## [v0.5.1] — 2026-02-17

- Add text-based keyword extraction fallback when LLM is unavailable (bigram/unigram frequency from paper titles with stopword filtering)
- Fix OllamaClient host configuration not being applied

## [v0.5.0] — 2026-02-17

- Package as standalone desktop app (PyInstaller backend + Electron frontend)
- Cross-platform builds: macOS (DMG), Windows (NSIS), Linux (AppImage)
- Add LLM provider settings modal (Ollama / Claude / OpenAI) with connection testing
- Introduce design token system and reusable UI component library (Button, Input, StatusBar)
- Dynamic port allocation (8000-8010) to avoid conflicts

## [v0.4.1] — 2026-02-16

- Load previously exported JSON sessions to restore full graph views

## [v0.4.0] — 2026-02-16

- Client-side full-state export (graph data, queries, toggle states, ranking weights, fundamentals, methodologies)

## [v0.3.7] — 2026-02-16

- Sidebar paper hover highlights corresponding node in graph
- Pin year markers to left viewport edge during horizontal pan
- Fix temporal dead zone bug causing blank page on startup

## [v0.3.6] — 2026-02-15

- In-graph paper search with autocomplete (Find)
- External paper addition from Semantic Scholar with automatic related-paper fetch (Add)
- Recompute graph metrics after adding papers

## [v0.3.5] — 2026-02-15

- Hybrid query expansion: three-strategy approach (keyword sub-phrases + LLM semantic alternatives + cross-combo abbreviation matching)
- Dedicated expansion strategy slots to prevent query starvation

## [v0.3.4] — 2026-02-15

- Query toggles: show/hide papers per search variant
- Professionality presets: Overview (relevance-heavy), Balanced, Expert (PageRank-heavy)
- Manual weight sliders for continuous ranking adjustment
- LLM-powered keyword extraction for methodology identification

## [v0.3.3] — 2026-02-15

- On-demand AI summaries on node hover (cached in SQLite)
- Citation relationship explanations on edge hover
- Persistent tooltips with 300ms delayed hide
- Debounced tooltip switching to prevent hijacking during mouse transit

## [v0.3.2] — 2026-02-14

- Chronological graph layout (top-to-bottom by publication year)
- Quantile-based year distribution (dense eras get proportional vertical space)
- Directional edge coloring (indigo = outgoing, green = incoming)

## [v0.3.1] — 2026-02-14

- LLM query expansion (Ollama generates 4-5 search variants)
- Citation graph expansion (1-hop neighbor discovery)
- Multi-query Semantic Scholar search with deduplication

## [v0.2] — 2026-02-13

- Hierarchical clustering (scipy agglomerative, up to 8 clusters)
- Sentence-transformer embeddings (all-MiniLM-L6-v2, 384-dim)
- Semantic relevance scoring (cosine similarity to query)
- Fundamental paper identification (PageRank + citation count + age)
- Background enrichment: non-blocking graph rendering with async enrichment polling

## [v0.1] — 2026-02-13

- Semantic Scholar scraper with SQLite caching and retry logic
- NetworkX citation graph with PageRank and eigenvector centrality
- FastAPI REST API
- React + D3.js frontend with force-directed graph visualization
- Graph navigation: click to center, click to open paper URL
