# Add an optional deterministic ChatGPT export preprocessor

## Summary

Create an optional preprocessing utility for large ChatGPT conversation
exports. The current Footprints skill intentionally applies
`prompts/001-generate-reflective-report.md` directly to uploaded JSON files.
The new utility should improve repeatability and reduce context size without
becoming a requirement for normal skill use.

## Motivation

ChatGPT exports contain graph metadata, inactive branches, assistant and tool
messages, and other operational data that are not primary evidence for a
Footprints report. Larger exports may benefit from deterministic reduction
before reflective analysis.

This work was deferred so the first reusable skill remains prompt-first and
easy to understand.

## Requirements

- Accept `chat.json`, `conversations.json`, numbered
  `conversations-*.json` files, and directories containing those files.
- Optionally support ChatGPT export ZIP files.
- Reconstruct each conversation from `current_node` by following parent links.
- Preserve graph order within each conversation.
- Exclude inactive branches and null messages.
- Extract string content from `text` and `multimodal_text` parts without
  treating image-reference objects as text.
- Retain conversation titles, timestamps, message roles, and attachment names
  and MIME types.
- Default to user-authored messages while allowing assistant context to be
  included explicitly.
- Deduplicate conversations when numbered chunks overlap.
- Produce a compact, documented output format such as JSONL.
- Process data locally and avoid network dependencies.
- Report malformed input and broken or cyclic graph paths clearly.

## Acceptance criteria

- Automated tests cover active-path traversal, branches, multimodal content,
  attachments, malformed input, duplicate conversations, and multiple files.
- The utility is tested against `example-chats/chat.json`.
- Output preserves all report-relevant user messages from the active paths.
- Direct JSON analysis remains the default Footprints workflow.
- `SKILL.md` documents when preprocessing is useful and how to invoke it only
  after the utility has been implemented and validated.
- The implementation includes concise usage documentation and has no
  third-party runtime dependency unless clearly justified.

## Out of scope

- Generating the reflective report itself.
- Scoring, classifying, or profiling the user.
- Reading attachment contents that are not present in the export.
- Replacing `prompts/001-generate-reflective-report.md` as the report
  methodology.

