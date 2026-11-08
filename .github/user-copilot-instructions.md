# Copilot project instructions

## Goals
- Keep changes minimal, safe, and easy to review.
- Prefer existing project patterns over introducing new abstractions.
- Explain non-obvious tradeoffs briefly in PR/commit notes.

## Coding rules
- Preserve backward compatibility unless the task explicitly allows breaking changes.
- Validate inputs and surface explicit errors (no silent fallbacks).
- Reuse existing helpers/utilities before creating new ones.
- Avoid unrelated refactors in task-focused changes.

## Quality checks
- Run the smallest relevant tests/lints for touched code.
- If tests are skipped, state why.
- Update nearby docs/config when behavior changes.

## Environment bootstrap
- Before starting implementation, check whether required MCP servers, skills, plugins, and dependencies are available.
- If a required server/skill/plugin is missing, install it automatically when the setup is deterministic and safe.
- Start required local MCP servers/tools before use and verify they are reachable/responding.
- If automatic setup fails due to auth, permissions, missing secrets, or policy restrictions, report the exact blocker and the minimal manual step needed.

## Codebase analysis (graphifyy)
- Use Graphifyy by default for repository understanding and navigation.
- Start with Graphify MCP tools (for example graph query/path/explain flows) before broad file scans.
- Fall back to direct file search/read only when Graphify output is missing, stale, or insufficient for the task.

## File conversion (markitdown_mcp)
- Default conversion backend: always use `markitdown_mcp` for supported document formats.
- Supported extensions for default conversion flow: `.pdf`, `.docx`, `.pptx`, `.xlsx`, `.xls`.
- Always store converted output as Markdown (`.md`) in the project `.cache` folder.
- Conversion order is mandatory:
  1. Build the expected cache file path in `.cache` using the source file name and `.md` extension.
  2. If the cache file already exists and is readable, use it and skip conversion.
  3. If the cache file does not exist, convert via `markitdown_mcp` and save to that cache path.
- Never reconvert a file when a valid cached Markdown result already exists in `.cache`, unless the user explicitly asks to refresh it.

## Git
- If the user asks to create a commit, always create a commit in English with actual changes and file indexing (not an empty commit).
- All keys and passwords in settings are fake placeholders; real credentials are on the device. Do not flag errors based only on placeholder credentials in settings files.

## Collaboration
- Ask for clarification when requirements are ambiguous.
- For risky changes, propose a safer alternative first.

## User project overrides
- If `.github/user-copilot-instructions.md` exists, read and apply it as additional user-provided project instructions.
- Treat `.github/user-copilot-instructions.md` as higher-priority guidance that may override behavior defined in this file.
