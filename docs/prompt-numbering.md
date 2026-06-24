# Prompt Numbering

Footprints report behavior is controlled primarily by
`prompts/001-generate-reflective-report.md`. Use the numbered prompt filename
as the version. The first prompt is `001`, the next substantial revision is
`002`, then `003`, and so on.

## When to create a new prompt

Create a new numbered prompt file when a change is expected to alter generated
reports in a meaningful way.

Examples:

- evidence policy changes;
- input handling changes;
- report section changes;
- analysis workflow changes;
- writing-rule changes that affect tone, structure, or claims.

Keep small clarifications, typo fixes, and non-behavioral documentation edits in
the current prompt file.

## How to add a new prompt

1. Copy the current prompt to the next numbered filename, such as
   `prompts/002-generate-reflective-report.md`.
2. Make the behavior change in the new file.
3. Add a short entry to the prompt's `Prompt History` section with the prompt
   number, date, and one or two bullets describing the change.
4. Update `SKILL.md` to load the new prompt file.
5. Update `README.md` if the repository map or contributor guidance needs to
   name the new file.

Repository-only documentation changes do not require a new prompt number.

## Example refreshes

Refresh generated examples when a prompt change is expected to alter report
content, structure, evidence anchors, or tone.

Do not refresh examples for typo-only prompt edits unless the example itself
contains the typo. When examples are refreshed, rerun the prompt against the
same fixture and review that:

- the stated date range still matches the input;
- evidence anchors still come from user-authored messages;
- report sections still follow the current prompt contract;
- omitted or changed findings are explainable by the prompt change;
- no private or unsanitized export data has been introduced.
