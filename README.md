# Copilot Base Settings

This folder is a starter kit for shared Copilot behavior across projects and clients.

## Included files
- `.github/copilot-instructions.md` — project-level behavior and coding rules.
- `.mcp.json` — MCP servers template, including MarkItDown presets.
- `skills/` — place reusable skill docs/templates here.

## How to use
1. Copy this folder into a new repository root.
2. Install MarkItDown MCP locally:
   - `py -m pip install markitdown-mcp`
3. For HTTP mode (optional), run:
   - `markitdown-mcp --http --host 127.0.0.1 --port 3001`
4. Add only real MCP servers you actually use.
5. Tune `copilot-instructions.md` for your team conventions.
6. Commit these files so Desktop/CLI/IDE clients can share the same baseline.

## Notes
- Keep secrets out of git; use environment variables or client secret storage.
- Client support differs by app/version; repo files provide the most portable baseline.
- For MarkItDown, prefer `stdio` setup; HTTP should target `http://127.0.0.1:3001/mcp` only when the local server is running.
