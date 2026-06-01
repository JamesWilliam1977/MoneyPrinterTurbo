---
name: refactor-hardcoded-data-to-json
description: Workflow command scaffold for refactor-hardcoded-data-to-json in MoneyPrinterTurbo.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /refactor-hardcoded-data-to-json

Use this workflow when working on **refactor-hardcoded-data-to-json** in `MoneyPrinterTurbo`.

## Goal

Extracts large hardcoded data structures from Python source files into separate JSON files, updates the code to load from JSON, and adds regression tests to ensure behavior is unchanged.

## Common Files

- `app/services/data/*.json`
- `app/services/*.py`
- `test/services/test_*.py`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Create a new JSON file in the appropriate data directory with the extracted data.
- Modify the relevant Python service to load data from the new JSON file, using a helper or caching if needed.
- Add or update regression tests to confirm the refactor does not change behavior.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.