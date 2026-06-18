# Add automated tests for export extraction

## Skills required

- Python
- JSON
- Unit testing
- ChatGPT export structure
- Fixture-based test design

## Skill level

Mid

## Ownership

- Owns the automated extraction test suite and documented test command.
- Depends on `docs/issues/004-add-deterministic-export-preprocessor.md` and
  `docs/issues/005-add-synthetic-parser-fixtures.md`.
- Does not own changing the preprocessor contract, creating human-facing
  examples, or evaluating report prose.

## Summary

Cover the traversal and extraction rules already specified in
`prompts/001-generate-reflective-report.md` and
`docs/chatgpt-export-schema.md`.

## Motivation

The skill currently depends on prompt instructions for correct export handling.
That is enough for small direct analysis, but any deterministic preprocessor
needs executable tests for graph traversal, filtering, text extraction, and
error handling.

Automated tests should make it hard to accidentally include inactive branches,
sort messages by timestamp instead of graph order, treat assistant/tool output
as primary evidence, or mistake image-reference objects for user text.

## Requirements

- Add a test suite for the preprocessor's export extraction layer.
- Prefer Python standard-library tests unless a third-party test dependency is
  clearly justified.
- Cover:
  - active-path traversal from `current_node`;
  - branch exclusion;
  - graph order preservation;
  - null-message exclusion;
  - user-message extraction;
  - optional assistant-context inclusion;
  - system and tool-message exclusion from substantive records;
  - `text` and `multimodal_text` extraction;
  - attachment metadata extraction;
  - duplicate conversation handling;
  - multi-file and directory input;
  - malformed input, broken parent references, and cyclic parent paths.
- Use the synthetic fixtures from
  `docs/issues/005-add-synthetic-parser-fixtures.md`.
- Include a smoke test against `examples/chat.json`.
- Document the test command in the relevant implementation or contributor
  notes.

## Acceptance criteria

- A single documented command runs the extraction tests locally.
- Tests pass without network access.
- Tests do not require private exports or private attachment files.
- Tests verify expected output records for the synthetic fixtures.
- Tests verify that `examples/chat.json` can be parsed without errors.
- Failure messages make it clear whether the problem is traversal, filtering,
  text extraction, deduplication, or malformed input handling.

## Out of scope

- Testing the quality of the reflective report prose.
- Running model-based evaluations.
- Adding CI configuration unless needed by a separate issue.
- Testing attachment contents that are not present in the export.
