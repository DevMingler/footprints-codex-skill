# Expand example coverage

## Skills required

- JSON
- Prompting
- Synthetic data writing
- Report QA

## Skill level

Mid

## Ownership

- Owns human-facing synthetic or sanitized example exports and their generated
  Footprints reports.
- Depends on `docs/issues/001-add-report-QA-rubric.md`.
- Does not own parser edge-case fixtures, preprocessor implementation, or
  automated extraction tests.

## Summary

Add one or two more sanitized/synthetic exports: a tiny narrative example and
a larger multi-month example with clearer "seasons and shifts."

## Motivation

The current example is useful, coherent, and small, but it represents only one
kind of reflective report. Additional synthetic examples would help
contributors understand how Footprints should behave across sparse histories,
edge cases, and longer multi-month arcs.

Example coverage should support report review and prompt iteration. Parser-only
edge cases should remain in the dedicated fixture work unless they also help
explain the report experience.

## Requirements

- Add one tiny synthetic export that is useful for manual inspection and quick
  smoke testing.
- Add one larger synthetic or sanitized export that has clearer chronological
  seasons, returning themes, and unfinished threads.
- Include generated Markdown reports for each added export.
- Review generated reports against the QA rubric from
  `docs/issues/001-add-report-QA-rubric.md`.
- Consider using an AI assistant such as ChatGPT or Claude to draft synthetic
  conversation content or ChatGPT-style JSON scaffolding.
- Keep all example content synthetic, sanitized, or intentionally public.
- Avoid real private ChatGPT histories.
- Do not upload private exports or unsanitized conversation history to external
  AI tools while creating examples.
- Make the examples different enough from `examples/chat.json` to exercise new
  report behavior.
- Include attachment metadata only when it supports a specific report-handling
  scenario.
- Keep example filenames clear and stable.
- Update repository documentation if the examples change how contributors
  should test prompt or report changes.

## Acceptance criteria

- Added exports are valid ChatGPT-style JSON files.
- Added reports follow the current Footprints report structure.
- Each report includes accurate date-range and evidence anchors.
- Reports do not expose raw JSON, internal message IDs, private analysis notes,
  or unsupported sensitive inferences.
- The larger example clearly exercises `Seasons and Shifts`.
- The tiny example is small enough to inspect manually during review.
- All examples are safe to commit publicly.

## Out of scope

- Building the deterministic preprocessor.
- Creating a large benchmark corpus.
- Adding private exports.
- Guaranteeing exact report wording across future prompt versions.
