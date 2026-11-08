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

## Git
- If the user asks to create a commit, always create a commit in English with actual changes and file indexing (not an empty commit).
- All keys and passwords in settings are fake placeholders; real credentials are on the device. Do not flag errors based only on placeholder credentials in settings files.

## Collaboration
- Ask for clarification when requirements are ambiguous.
- For risky changes, propose a safer alternative first.
