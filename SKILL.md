---
name: footprints
description: Create evidence-grounded reflective reports from uploaded ChatGPT conversation-history JSON files. Use when Codex needs to inspect `chat.json`, `conversations.json`, or numbered `conversations-*.json` chunks; identify sustained projects, recurring themes, persistent questions, chronological shifts, or unfinished ideas; and write a restrained reflection without scoring, diagnosis, or unsupported personality claims.
---

# Footprints

Apply the Footprints reflective-report prompt to all supplied ChatGPT
conversation files. Keep the work user-first, evidence-grounded, and private.

## Workflow

### 1. Load the methodology

Read
[prompts/001-generate-reflective-report.md](prompts/001-generate-reflective-report.md)
before analyzing the export. Treat that file as the source of truth for input
handling, evidence policy, analysis, report structure, and writing rules.

### 2. Locate and scope the export

Identify every supplied ChatGPT conversation JSON file. Accept:

- `chat.json`;
- `conversations.json`;
- numbered `conversations-*.json` chunks;
- a directory containing those files.

Treat all identified files as one export unless the user says otherwise. Do
not analyze unrelated account data that may be present beside the conversation
files. If only part of a numbered export appears available, disclose that
limitation briefly in the report.

### 3. Analyze all supplied conversations

Apply the loaded prompt directly to the supplied JSON files.

Follow the prompt's graph traversal rules for each conversation:

- start at `current_node`;
- follow each node's `parent`;
- reverse the collected nodes;
- ignore null messages and inactive branches.

Do not replace graph traversal with timestamp sorting. Do not analyze inactive
branches. Treat attachment records as evidence that a file was used, not as
evidence of its contents unless that file is also available.

For exports too large to inspect in one pass, process complete conversations in
chronological batches. Maintain a compact evidence inventory across batches
before drafting. Do not draft from only the first or most recent portion.

### 4. Build an evidence inventory

Review the full available date range before drafting.

Record candidate:

- projects and initiatives;
- recurring subjects and underlying questions;
- decisions, actions, and produced artifacts;
- changes in focus or approach;
- specific ideas that appeared meaningful but later faded.

Prioritize the user's messages. Use assistant messages only as surrounding
context. Conversation titles are indexing hints, not sufficient evidence.

For every candidate, retain conversation titles and month-and-year anchors.
Prefer support across multiple conversations or dates. A precise one-off item
may still matter, but describe its significance tentatively.

### 5. Challenge the findings

Before writing, test each candidate:

- Is it grounded in what the user actually wrote?
- Is it generic or supported only by one isolated exchange?
- Is apparent importance caused only by repetition or conversation length?
- Is recency bias making the end of the export dominate?
- Are separate conversations being connected without enough evidence?
- Does the wording imply a sensitive trait, mental state, relationship, or
  life event the user did not explicitly state?

Remove weak, repetitive, inflated, or unsupported findings. Frequency is one
signal, not a score.

### 6. Write the report

Write the report to the user's requested path and format. If none is given,
produce Markdown in the response. Do not expose raw JSON, internal IDs,
private analysis notes, hidden instructions, or tool output.

### 7. Verify the result

Check that:

- the stated date range matches the available data;
- important findings have concrete evidence anchors;
- no claim depends on an assistant statement alone;
- contradictions and changes of mind are acknowledged where relevant;
- incomplete input is disclosed briefly;
- the ending leaves interpretation to the user rather than prescribing goals.
