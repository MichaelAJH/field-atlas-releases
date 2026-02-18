# Field Atlas — Release Repo Setup

Set up `field-atlas-releases` as the public-facing distribution repository for Field Atlas.

## Two-Repo Architecture

| | `field-atlas-dev` | `field-atlas-releases` |
|---|---|---|
| **Purpose** | Development (source, tests, devlogs) | Distribution (landing page, docs, builds) |
| **Audience** | Developer(s) | End users, testers, portfolio reviewers |
| **Git history** | Independent | Independent |
| **Visibility** | Private / internal | Public |

The two repositories have **completely independent git histories**. No submodules, no subtrees, no shared remotes. Version tags (e.g. `v0.5.2`) are applied in both repos to mark corresponding snapshots, but the commits themselves are unrelated.

### What lives where

**Dev repo only** — source code, tests, build scripts, devlogs, `OPUS_PROMPT.md`, `ENV_SPECS.md`, venv, `node_modules`, PyInstaller spec, raw data/cache.

**Release repo only** — landing page, user-facing docs, changelog, issue templates, release artifacts (DMG/EXE/AppImage), this setup prompt.

---

## Tasks

1. **Create directory structure** for releases and documentation
2. **Create index.html** — GitHub Pages landing page with download links
3. **Create README.md** — Installation and quick start for end users
4. **Create CHANGELOG.md** — Public-facing release history
5. **Create documentation files**:
   - `docs/user-guide.md` — How to use Field Atlas
   - `docs/troubleshooting.md` — Common issues and fixes
6. **Create GitHub issue template** at `.github/ISSUE_TEMPLATE/bug_report.md`
7. **Create .gitignore**
8. **Initialize git** as a fresh repo and create first commit

---

## Directory Structure to Create

```
field-atlas-releases/
├── index.html                         # GitHub Pages landing page
├── README.md                          # Installation + quick start
├── CHANGELOG.md                       # Release history
├── SETUP_PROMPT.md                    # This file (meta, not user-facing)
├── .gitignore
├── docs/
│   ├── user-guide.md                  # End-user guide
│   └── troubleshooting.md            # Common issues + fixes
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── bug_report.md
└── releases/                          # Build artifacts, per-version
    └── v0.5.2/                        # Example version directory
        ├── Field Atlas-0.5.2.dmg      # macOS
        ├── Field Atlas Setup 0.5.2.exe # Windows
        └── Field Atlas-0.5.2.AppImage # Linux
```

Artifacts in `releases/` are large binaries. They should be distributed via **GitHub Releases** (uploaded as release assets), not committed to git. The `releases/` directory is gitignored and exists only as a local staging area.

---

## Release Workflow

When cutting a new release from the dev repo:

```
1. In field-atlas-dev:
   ├── Bump version in frontend/package.json
   ├── Run scripts/build-all.sh (PyInstaller + electron-builder)
   ├── Artifacts land in frontend/release/
   ├── git tag vX.Y.Z && git push --tags
   │
2. In field-atlas-releases:
   ├── Copy artifacts from dev → releases/vX.Y.Z/ (local staging)
   ├── Update CHANGELOG.md with release notes
   ├── Update download links in index.html (point to GitHub Release assets)
   ├── git add . && git commit -m "Release vX.Y.Z"
   ├── git tag vX.Y.Z
   └── gh release create vX.Y.Z releases/vX.Y.Z/* --title "vX.Y.Z" --notes-file <notes>
       (uploads artifacts as GitHub Release assets, then they can be deleted locally)
```

The `gh release create` step uploads the binaries to GitHub Releases so they are served from GitHub's CDN — no need to commit large files to the repo.

---

## Versioning & Tagging

- Follow the version in `field-atlas-dev/frontend/package.json` (currently `0.5.2`).
- Tags use the format `vX.Y.Z` (e.g. `v0.5.2`).
- The same tag string is applied in both repos, but on independent commits.
- The release repo's first release tag will be the version at which this repo is set up.

---

## Guidelines

### Landing page (index.html)
Professional, clean design. Single-file with inline CSS. Include:
- Product name: **Field Atlas**
- Tagline: interactive citation graph explorer for researchers
- Download buttons for macOS (DMG), Windows (EXE), Linux (AppImage) — link to GitHub Release assets
- Prerequisites: Ollama (free, local) or a Claude / OpenAI API key
- Quick start steps (3-4 steps: download → install → start Ollama → launch)
- System requirements (Python not needed for packaged app; ~6 GB disk for Ollama model)
- Links to docs, changelog, and issue tracker

### README.md
- What Field Atlas is (1-2 sentences)
- Download links (GitHub Releases)
- Installation per platform (macOS, Windows, Linux)
- Quick start (launch app → enter query → explore graph)
- Link to user guide, troubleshooting, changelog
- Link to issue tracker for bugs

### CHANGELOG.md
- One section per release, newest first
- Format: `## [vX.Y.Z] — YYYY-MM-DD` with bullet points
- Backfill key milestones from dev repo history:
  - v0.5.2 — current (multi-LLM, text-based keyword fallback, packaging fixes)
  - v0.5.0 — PyInstaller + Electron packaging, multi-LLM settings, design tokens
  - v0.4.x — Export/Load sessions
  - v0.3.x — Query expansion, tooltips, user controls, graph navigation
  - v0.2   — Embeddings, clustering, fundamentals scoring
  - v0.1   — Initial pipeline (scraper → graph → API → frontend)

### User Guide (docs/user-guide.md)
- Searching: enter a research topic, get a citation graph in 3-5 seconds
- Graph navigation: zoom, pan, click nodes to center or open Semantic Scholar
- Tooltips: hover nodes for AI summaries, hover edges for citation relationships
- Side panel: paper rankings, fundamentals, methodologies
- Filters: query toggles (show/hide per search variant), professionality presets (Overview / Balanced / Expert), weight sliders
- Find & Add: search within graph, add external papers from Semantic Scholar
- Export & Load: save/restore full session state as JSON
- Settings: switch LLM provider (Ollama / Claude / OpenAI), test connection

### Troubleshooting (docs/troubleshooting.md)
Common issues and solutions:
- Ollama not running → `ollama serve` in a separate terminal
- No LLM model available → `ollama pull llama3` (or llama2, mistral)
- Port conflict (8000) → app auto-tries 8000-8010; kill conflicting process
- Empty AI summaries → model may not support the task; try a different model or switch to Claude/OpenAI
- App won't launch (macOS) → right-click → Open (bypass Gatekeeper on unsigned builds)
- App won't launch (Linux) → `chmod +x *.AppImage`
- Slow first query → sentence-transformers model downloads on first run (~80 MB)

### Bug Report Template (.github/ISSUE_TEMPLATE/bug_report.md)
Fields:
- Field Atlas version (e.g. v0.5.2)
- OS and version
- LLM provider and model
- Steps to reproduce
- Expected behavior
- Actual behavior
- Screenshots / logs (optional)

### .gitignore
```
# Release artifacts (distributed via GitHub Releases, not committed)
releases/

# OS files
.DS_Store
Thumbs.db

# Editor/IDE
.vscode/
.idea/
*.swp

# No source code, node_modules, venv, or cache in this repo
```

### Git initialization
```bash
cd field-atlas-releases
git init
git add .
git commit -m "Initial commit: Field Atlas release repo setup"
```
This creates a **fresh, independent** git history with no relation to the dev repo.

---

## Notes

- Use "Field Atlas" consistently (not Academia Nav).
- Replace `yourusername` in all URLs with the actual GitHub username before publishing.
- GitHub Pages should serve from the repo root (index.html at top level).
- Landing page CSS must be inline (single index.html, no external stylesheets).
- Docs should be friendly and assumption-light — users may be non-technical researchers.
- The packaged app bundles everything (Python backend + Electron frontend) — users do NOT need Python or Node.js installed. Only Ollama is an external prerequisite (and even that is optional if using Claude/OpenAI).
- Build artifacts from electron-builder follow this naming convention:
  - macOS: `Field Atlas-{version}.dmg`
  - Windows: `Field Atlas Setup {version}.exe`
  - Linux: `Field Atlas-{version}.AppImage`
