# Copilot Base Settings

This folder is a starter kit for shared Copilot behavior across projects and clients.

## Included files
- `.github/copilot-instructions.md` — project-level behavior and coding rules.
- `.mcp.json` — stdio MCP setup for MarkItDown and Graphify.
- `skills/` — place reusable skill docs/templates here.

## How to use
1. Copy this folder into a new repository root.
2. Install required tooling:
   - `py -m pip install markitdown-mcp`
   - `uv tool install "graphifyy[mcp]"`
3. Open the project in your IDE and use MCP normally.
4. Add only real MCP servers you actually use.
5. Tune `copilot-instructions.md` for your team conventions.
6. Commit these files so Desktop/CLI/IDE clients can share the same baseline.

## Graphify auto-update (watch)
- A ready-to-run VS Code task is included: `.vscode/tasks.json` → `Graphify: Watch`.
- It is configured to auto-start on folder open (`runOn: "folderOpen"`).
- Start it from **Terminal → Run Task → Graphify: Watch**.
- The task runs:
  - `uv run --with "graphifyy[watch]" -m graphify watch .`
- On first launch, VS Code may ask for permission to run automatic tasks in this workspace.

## Notes
- Keep secrets out of git; use environment variables or client secret storage.
- Client support differs by app/version; repo files provide the most portable baseline.
- This setup uses standard `stdio` transport via `py -m markitdown_mcp` (more reliable on Windows PATH) without Docker.
