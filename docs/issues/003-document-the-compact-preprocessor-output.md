# Document the compact preprocessor output format

## Skills required

- JSON
- Technical writing
- Schema design
- Python familiarity

## Skill level

Junior

## Ownership

- Owns the compact preprocessor output contract.
- Depends on no other issue.
- Does not own implementing the preprocessor, creating parser fixtures, or
  writing automated extraction tests.

## Summary

Define the JSONL record schema, required fields, optional assistant-context
mode, and how attachment metadata is represented.

## Motivation

The optional preprocessor should reduce ChatGPT exports without losing the
evidence needed for a Footprints report. A documented output format gives
contributors a stable target before implementation and makes tests easier to
write.

The format should be compact enough for large exports, but explicit enough to
preserve traceability, chronology, source files, roles, and attachment
metadata.

## Requirements

- Add a document describing the preprocessor output format, such as
  `docs/preprocessor-output-format.md`.
- Define the primary message record fields, including:
  - record type;
  - source file;
  - conversation ID;
  - conversation title;
  - conversation create and update times;
  - active-path index;
  - message ID;
  - parent ID when useful for traceability;
  - role;
  - message create time;
  - content type;
  - extracted text;
  - attachment metadata.
- Specify required fields and optional fields.
- Document how assistant-context mode changes the included records.
- Document how warnings or errors should be represented, especially for
  malformed input.
- Include one short JSONL example.
- Explain that attachment metadata is not evidence of attachment contents.
- Keep the format local-first and free of network assumptions.

## Acceptance criteria

- The format document is specific enough for someone to implement against it.
- Example JSONL records are valid JSON when read line by line.
- The documented fields support the requirements in
  `docs/issues/004-add-deterministic-export-preprocessor.md`.
- The format preserves all report-relevant user-authored messages from active
  paths.
- The document clearly distinguishes user evidence, assistant context, and
  operational warnings.

## Out of scope

- Implementing the preprocessor.
- Choosing a long-term public API.
- Defining a report format.
- Reading or embedding attachment file contents.
