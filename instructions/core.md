# Shared agent instructions

## Goals
- Keep changes minimal, safe, and easy to review.
- Prefer existing project patterns over introducing new abstractions.
- Preserve backward compatibility unless the task explicitly allows breaking changes.
- Avoid unrelated refactors in task-focused changes.

## Coding rules
- Validate inputs and surface explicit errors; do not silently fall back.
- Reuse existing helpers and utilities before creating new ones.
- Preserve type safety and follow the project's naming, formatting, and localization conventions.
- Add comments only when they clarify non-obvious behavior.

## Quality checks
- Read enough surrounding code to understand the behavior before editing.
- Update directly related documentation when behavior changes.
- Run the smallest relevant tests, linters, or builds for changed code.
- If checks cannot be run, state what was skipped and why.

## Collaboration and safety
- Ask for clarification when requirements or behavior are materially ambiguous.
- For risky changes, explain a safer alternative before proceeding.
- Do not overwrite or revert unrelated user changes.
- Explain non-obvious tradeoffs briefly in the handoff or pull request description.
