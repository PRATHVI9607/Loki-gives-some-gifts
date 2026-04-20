# CLAUDE.md Agent Directives

Use this as a clean reference for strict execution behavior in coding sessions.

## Purpose

These directives are intended to enforce production-grade workflow discipline when operating under constrained context windows and strict system prompts.

## Pre-Work

### 1) Step 0 Rule

Before any structural refactor on a file larger than 300 LOC:

- Remove dead props
- Remove unused exports
- Remove unused imports
- Remove debug logs
- Commit cleanup separately before starting real refactor work

### 2) Phased Execution

- Do not attempt broad multi-file refactors in one response.
- Break work into explicit phases.
- Complete Phase 1, run verification, then wait for explicit approval before Phase 2.
- Keep each phase limited to 5 files max.

## Code Quality

### 3) Senior Dev Override

- Do not stop at surface-level changes when architecture is flawed.
- If state is duplicated or patterns are inconsistent, propose and implement structural fixes.
- Hold output to strict code-review quality.

### 4) Forced Verification

Do not report completion until verification passes:

- `npx tsc --noEmit` (or project equivalent)
- `npx eslint . --quiet` (if configured)

If no type-checker/linter is configured, state that explicitly.

## Context Management

### 5) Sub-Agent Swarming

For tasks touching more than 5 independent files:

- Use parallel sub-agents (5–8 files per agent)
- Avoid purely sequential handling for large scopes

### 6) Context Decay Awareness

After 10+ messages in a session:

- Re-read files before editing
- Do not rely on memory of prior file state

### 7) File Read Budget

- Each read is capped at 2,000 lines.
- For files over 500 LOC, read in sequential chunks.
- Never assume one read captured full file content.

### 8) Tool Result Blindness

- Very large command/search outputs may be truncated.
- If results look suspiciously small, rerun with narrower scope.
- State when truncation is suspected.

## Edit Safety

### 9) Edit Integrity

- Re-read file before every edit.
- Read again after edit to verify applied changes.
- Avoid batching more than 3 edits in one file without verification reads.

### 10) No Semantic Search Assumptions

When renaming/changing symbols, separately search for:

- Direct references/calls
- Type-level references (interfaces/generics)
- String literals containing the name
- Dynamic imports and `require()` calls
- Re-exports and barrel files
- Tests and mocks

Do not assume one grep pass found all usages.
