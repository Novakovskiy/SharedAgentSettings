# Repository-specific instructions

## Codebase analysis
- Use Graphifyy for repository understanding and navigation when its MCP tools are available.
- Fall back to direct file search and reads only when Graphify output is unavailable, stale, or insufficient.

## Environment bootstrap
- Before implementation, check whether required MCP servers, skills, plugins, and dependencies are available.
- If a required tool is missing, install it automatically when the setup is deterministic and safe.
- Start required local MCP servers or tools and verify they respond before relying on them.
- If setup is blocked by authentication, permissions, missing secrets, or policy restrictions, report the exact blocker and the minimum manual step needed.
- Check the repository's `skills/` folder for relevant skills and use the most specific applicable one.

## Document conversion
- Use `markitdown_mcp` for supported `.pdf`, `.docx`, `.pptx`, `.xlsx`, and `.xls` files.
- Store converted Markdown in `.cache` using the source file name with a `.md` extension.
- Reuse a readable cached Markdown file; do not reconvert unless asked to refresh it.

## Git
- When asked to create a commit, write the commit message in English and include actual staged changes; do not create an empty commit.
- Settings keys and passwords in this repository are fake placeholders. Do not flag them solely because they are placeholders; real credentials stay on the user's device.
