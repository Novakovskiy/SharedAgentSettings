# Shared Agent Settings

This repository is a central source for shared agent instructions and IDE configuration. Instruction sources live under `instructions/`; the generated entry points let compatible clients discover those rules.

## Instruction sources
- `instructions/core.md` — shared coding, safety, and quality rules.
- `instructions/project.md` — repository-specific tooling and conventions.
- `instructions/providers/copilot.md` — GitHub Copilot-specific behavior.
- `AGENTS.md` — generated instructions for agents that support the `AGENTS.md` convention.
- `.github/copilot-instructions.md` — generated instructions for GitHub Copilot clients.
- `scripts/sync_instructions.py` — generates or installs the entry-point files.

Edit the canonical files under `instructions/`, then regenerate the checked-in entry points:

```powershell
python scripts\sync_instructions.py
```

Install the generated files into another project:

```powershell
python scripts\sync_instructions.py --target C:\path\to\project
```

The script refuses to replace existing unmarked instruction files unless `--force` is provided. Back up or merge any project-specific rules before forcing an overwrite.

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
