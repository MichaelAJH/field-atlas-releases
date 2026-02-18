# Field Atlas

An interactive citation graph explorer that helps researchers navigate unfamiliar academic fields.

Enter a research topic, and Field Atlas discovers ~50-70 relevant papers from Semantic Scholar, builds a citation graph, and provides AI-powered summaries — all in seconds.

## Download

Get the latest release for your platform:

| Platform | Format | Link |
|----------|--------|------|
| macOS    | `.dmg` | [Download](https://github.com/yourusername/field-atlas-releases/releases/latest) |
| Windows  | `.exe` | [Download](https://github.com/yourusername/field-atlas-releases/releases/latest) |
| Linux    | `.AppImage` | [Download](https://github.com/yourusername/field-atlas-releases/releases/latest) |

See all versions on the [Releases page](https://github.com/yourusername/field-atlas-releases/releases).

## Installation

### macOS

1. Download the `.dmg` file.
2. Open it and drag **Field Atlas** to your Applications folder.
3. On first launch, macOS may block the app (unsigned). Right-click the app and select **Open**, then confirm.

### Windows

1. Download the `.exe` installer.
2. Run the installer and follow the prompts.
3. Launch Field Atlas from the Start menu or desktop shortcut.

### Linux

1. Download the `.AppImage` file.
2. Make it executable: `chmod +x Field\ Atlas-*.AppImage`
3. Run it: `./Field\ Atlas-*.AppImage`

## Quick Start

1. **Install Ollama** (recommended) — download from [ollama.com](https://ollama.com/download), then pull a model:
   ```bash
   ollama pull llama3
   ```
   Start the Ollama service if it isn't running: `ollama serve`

2. **Launch Field Atlas**.

3. **Enter a research topic** (e.g. "diffusion models for speech recognition") and press Enter.

4. **Explore** the citation graph — zoom, pan, hover papers for AI summaries, hover edges for citation explanations.

Ollama is optional if you have a **Claude** (Anthropic) or **OpenAI** API key. Configure your provider in the app's Settings.

## Documentation

- [User Guide](docs/user-guide.md) — detailed walkthrough of all features
- [Troubleshooting](docs/troubleshooting.md) — solutions for common issues
- [Changelog](CHANGELOG.md) — release history

## Reporting Issues

Found a bug or have a feature request? Open an issue on the [issue tracker](https://github.com/yourusername/field-atlas-releases/issues).
