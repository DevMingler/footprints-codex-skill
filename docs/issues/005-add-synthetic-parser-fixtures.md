# Add synthetic parser fixtures

## Skills required

- JSON
- ChatGPT export structure
- Test fixture design
- Privacy-aware synthetic data writing

## Skill level

Mid

## Ownership

- Owns parser-focused synthetic input fixtures and expected extraction outputs.
- Depends on `docs/issues/003-document-the-compact-preprocessor-output.md` and
  `docs/issues/004-add-deterministic-export-preprocessor.md`.
- Does not own the preprocessor implementation or the automated test runner.

## Summary

Create small JSON fixtures for active-path traversal, inactive branches,
multimodal text, attachments, malformed graphs, cyclic parents, duplicate
chunks, and missing numbered chunks.

Main question: "Did extraction handle this JSON correctly?"
Used by: automated tests.

## Motivation

The current `examples/chat.json` file is useful as a realistic sample, but it
does not cover every edge case that the optional preprocessor and extraction
tests will need. Small synthetic fixtures make parser behavior easier to
review, easier to debug, and safer to share publicly.

These fixtures should support the deterministic export-preprocessor work
without requiring contributors to inspect private ChatGPT exports.

## Requirements

- Add a small fixture directory for parser-focused exports, such as
  `examples/fixtures/parser/`.
- Include fixtures for:
  - a simple active-path conversation;
  - a conversation with inactive branches that must be ignored;
  - `multimodal_text` content with both string parts and image-reference
    objects;
  - attachment metadata with names and MIME types;
  - malformed input with a missing `current_node`;
  - malformed input with a broken parent reference;
  - malformed input with a cyclic parent path;
  - duplicate conversations across numbered chunk files;
  - a directory with multiple numbered `conversations-*.json` files;
  - a numbered export with an intentionally missing chunk.
- Keep all conversation content synthetic and clearly non-private.
- Keep each fixture small enough to inspect manually.
- Add expected normalized output for valid fixtures in the documented compact
  preprocessor format.
- Run valid fixtures through the preprocessor and update expected output when
  the documented format requires it.
- Add a concise fixture manifest that explains what behavior each fixture is
  meant to exercise.

## Acceptance criteria

- Every fixture is valid JSON unless it is intentionally malformed for error
  handling.
- Malformed fixtures are named and documented so tests can assert the expected
  failure mode.
- Valid fixtures include expected output records for active-path extraction.
- Expected outputs match the preprocessor output or document a clear bug to be
  fixed before the automated tests are added.
- Fixtures do not contain real personal conversation data, private account
  identifiers, or real attachment contents.
- The fixture set can be used by the automated extraction tests in
  `docs/issues/006-add-automated-tests-for-export-extract.md`.

## Out of scope

- Implementing the preprocessor itself.
- Creating the automated test runner.
- Generating reflective reports from these fixtures.
- Creating large benchmark exports.
- Testing private or unsanitized ChatGPT histories.
