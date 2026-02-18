# Troubleshooting

Solutions for common issues with Field Atlas.

---

## Ollama Not Connected

**Symptom**: The app shows a warning that no LLM provider is connected, or AI summaries fail to load.

**Solution**:
1. Make sure Ollama is installed. Download it from [ollama.com](https://ollama.com/download).
2. Start the Ollama service in a terminal:
   ```bash
   ollama serve
   ```
3. Verify it's running:
   ```bash
   curl http://localhost:11434
   ```
   You should see `Ollama is running`.
4. In Field Atlas, open **Settings** and click **Test Connection** on the Ollama tab.

---

## No LLM Model Available

**Symptom**: Ollama is running but summaries are empty or query expansion doesn't work.

**Solution**: You need to download at least one model:
```bash
ollama pull llama3
```
Other options: `mistral`, `llama2`, `codellama`. Each model is approximately 4 GB.

After pulling, restart Field Atlas or re-test the connection in Settings.

---

## Empty AI Summaries

**Symptom**: Hovering a paper shows the tooltip but the summary section is blank.

**Possible causes**:
- The selected Ollama model returned an empty response. Some models hosted remotely via Ollama may not support all query types.
- **Fix**: Try a different model in Settings (e.g. switch from a remote model to a locally-pulled one like `llama3`).
- Alternatively, switch to Claude or OpenAI in Settings if you have an API key.

---

## Port Conflict

**Symptom**: The app fails to start or shows a connection error to the backend.

**Explanation**: Field Atlas's backend needs a TCP port (default 8000). If another application is using it, the app automatically tries ports 8001 through 8010.

**If all ports are taken**:
1. Find what's using port 8000:
   ```bash
   lsof -i :8000
   ```
2. Stop the conflicting process, or close other Field Atlas instances.

---

## App Won't Launch — macOS

**Symptom**: macOS shows "Field Atlas can't be opened because it is from an unidentified developer" or moves the app to Trash.

**Solution**: The app is not currently code-signed.
1. Right-click (or Control-click) the app in Finder.
2. Select **Open** from the context menu.
3. In the dialog that appears, click **Open** to confirm.

You only need to do this once. macOS will remember your choice.

If macOS Sequoia (15+) blocks the app entirely:
```bash
xattr -rd com.apple.quarantine /Applications/Field\ Atlas.app
```

---

## App Won't Launch — Linux

**Symptom**: Double-clicking the `.AppImage` file does nothing.

**Solution**: AppImage files need to be marked as executable:
```bash
chmod +x Field\ Atlas-*.AppImage
./Field\ Atlas-*.AppImage
```

---

## Slow First Query

**Symptom**: The very first query after installation takes much longer than expected (30+ seconds).

**Explanation**: On first run, Field Atlas downloads the sentence-transformer model (`all-MiniLM-L6-v2`, ~80 MB). This is a one-time download. Subsequent queries will be much faster (3-5 seconds for initial results).

---

## Graph Appears Empty

**Symptom**: The query returns but no nodes appear in the graph.

**Possible causes**:
- The query was too specific or used unusual terminology. Try broader terms.
- Semantic Scholar may not have papers matching the query. Try rephrasing.
- If you have query toggles, make sure at least one toggle is checked.

---

## Papers Missing After Enrichment

**Symptom**: Papers you added manually disappear after background enrichment completes.

**Solution**: This was fixed in v0.3.6+. If you're on an older version, update to the latest release.

---

## Claude / OpenAI API Errors

**Symptom**: After entering an API key, the test connection fails or summaries return errors.

**Check**:
- Verify the API key is correct and has not expired.
- For Claude: ensure your Anthropic account has API access enabled.
- For OpenAI: ensure your account has available credits.
- Check your network connection — these providers require internet access (unlike Ollama).

---

## Still stuck?

If none of the above helps, [open an issue](https://github.com/yourusername/field-atlas-releases/issues) with:
- Your Field Atlas version
- Your operating system
- The LLM provider you're using
- What you expected vs. what happened
- Any error messages or screenshots
