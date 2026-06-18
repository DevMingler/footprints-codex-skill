# Add report QA rubric

## Skills required

- Prompting
- QA
- Evaluation design
- Privacy and safety review

## Skill level

Mid

## Ownership

- Owns the human review rubric for Footprints reports.
- Depends on no other issue.
- Does not own adding new example exports, changing the report prompt, or
  building automated model evaluation.

## Summary

Turn the report design principles into a checklist for reviewers: evidence
anchors, no assistant-only claims, no sensitive inference, no recency bias, no
hidden IDs/raw JSON, and clear incomplete-input disclosure.

## Motivation

The project already has strong report-design principles, but contributors need
a practical review surface for generated reports. A QA rubric should help
reviewers catch unsupported claims, overconfident synthesis, privacy leaks, and
format drift without turning Footprints into a scoring or ranking system.

The rubric should support human review of sample outputs and prompt changes,
especially when contributors do not have access to the same private exports.

## Requirements

- Add a report QA document, such as `docs/report-qa-rubric.md`.
- Base the rubric on:
  - `prompts/001-generate-reflective-report.md`;
  - `docs/report-design-v1.md`;
  - the current example report in `examples/`.
- Include checklist sections for:
  - input scope and date range;
  - active-path and evidence handling;
  - user-first claims;
  - assistant contamination;
  - evidence anchors;
  - report structure;
  - recency bias and over-repetition;
  - sensitive inference and diagnosis avoidance;
  - privacy, raw JSON, IDs, and hidden implementation details;
  - tone, restraint, and usefulness.
- Use pass/fail or review-note language rather than numeric scoring.
- Include examples of common failure modes.
- Add guidance for reviewing reports generated from synthetic or sanitized
  exports.

## Acceptance criteria

- A contributor can use the rubric to review a Footprints report without extra
  project context.
- The rubric does not introduce productivity scores, personality labels, or
  diagnostic categories.
- The rubric distinguishes critical failures from ordinary revision notes.
- The rubric covers the guardrails in `SKILL.md` and the writing rules in the
  report prompt.
- The README or relevant docs link to the rubric if it becomes part of normal
  contributor workflow.

## Out of scope

- Building an automated model evaluator.
- Assigning numeric quality scores to reports.
- Reviewing private exports committed outside the repository.
- Changing the report structure unless a separate prompt issue is opened.
