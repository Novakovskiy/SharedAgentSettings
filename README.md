# Shared Agent Settings

This repository is a central source for shared agent instructions and IDE configuration. Instruction sources live under `instructions/`; the generated entry points let compatible clients discover those rules.

## Instruction sources
- `instructions/core.md` — shared coding, safety, quality, and repository rules.
- `instructions/providers/` — provider-specific rules for Claude Code and OpenAI Codex.
- `instructions/current-project.md` — project-specific settings, conventions, and decisions, maintained by agents as they are established; it is read last by all agents and takes priority over other instruction files.
- `AGENTS.md` and `.github/copilot-instructions.md` — generated entry points that direct agents to read `instructions/core.md` first, provider and other instruction files next, and `instructions/current-project.md` last.
- `scripts/sync_instructions.py` — generates or installs the entry-point files.

Edit the canonical files under `instructions/`, then regenerate the checked-in entry points:

```powershell
python scripts\sync_instructions.py
```

Install the generated files into another project:

```powershell
python scripts\sync_instructions.py --target C:\path\to\project
```

With `--target`, the script installs or updates `AGENTS.md`, `.github/copilot-instructions.md`, the full `instructions/`, `skills/`, and `.claude/` trees, plus `.mcp.json`, `mcp.json`, and `.vscode/mcp.json`. Existing source files are refreshed, and missing files are added. Existing MCP configurations are merged: shared server definitions are updated while target-only servers and settings are preserved.

The script also installs `.vscode/tasks.json`. If the target already has tasks, shared tasks with new labels are appended; target tasks with matching labels are preserved. Other target task settings are kept. An existing `instructions/current-project.md` is preserved because it contains project-specific settings; it is only copied when missing.

Existing generated entry points are refreshed. If either entry point exists without the generator marker, the script stops rather than replacing project-specific content; use `--force` only after backing up or merging those rules.

The script does not copy other IDE settings or project files.

There is no single instruction-file format or global configuration location shared by every IDE and model. These entry points cover clients that recognize `AGENTS.md` or GitHub Copilot instructions. Add a provider-specific adapter when another client requires a different format; keep MCP configuration in the client's expected file and format.

## IDE configuration
- `.mcp.json` — repository MCP configuration, including a portable `mcpServers` format.
- `mcp.json` — MCP configuration for IDEs or workflows expecting that filename and `servers` format.
- `.vscode/mcp.json` — VS Code workspace MCP configuration.
- `skills/` — reusable skills available to compatible agent clients.

The MCP files point to the same local servers (`graphify` and `markitdown`) using standard `stdio` transport. Add only servers you use and keep secrets out of the repository.

## Initial setup
1. Install required tooling:
   - `python -m pip install markitdown-mcp`
   - `python -m pip install "graphifyy[mcp,watch]"`
2. Open the project in your IDE and configure or enable its MCP integration.
3. Use **Terminal → Run Task → Graphify: Watch** in VS Code to start the included graph watcher. It is configured to run on folder open; VS Code may first ask permission for automatic tasks.
4. Commit the canonical instruction sources and generated entry points so the baseline stays versioned.
