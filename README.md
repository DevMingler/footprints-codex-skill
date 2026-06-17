# Footprints Codex Skill

An open-source Codex Skill for exploring the paths people leave behind in their conversations.

Footprints transforms ChatGPT exports into reflective reports that highlight projects, recurring themes, persistent questions, creative seasons, and emerging patterns over time.

The goal is not analytics.

The goal is reflection.

---

## What is Footprints?

Footprints is an experiment in helping people better understand their own conversation history.

Given a ChatGPT export (`chat.json`), Footprints attempts to identify:

* Major projects
* Recurring themes
* Persistent questions
* Creative and reflective seasons
* Emerging interests
* Turning points and shifts in focus
* Long-term patterns that may not be obvious when viewed conversation by conversation

Rather than analysing individual messages in isolation, Footprints seeks to understand the larger story that emerges across months or years of conversations.

---

## What is This Repository?

This repository contains the open-source Codex Skill implementation of
Footprints. The repository root is the installable skill.

Unlike the Custom GPT implementation, the Codex Skill is intended for:

* Contributors
* Prompt engineers
* Researchers
* Experimenters
* Developers
* Curious users

It provides a transparent and extensible environment for improving the Footprints methodology.

---

## Install

Copy or clone this repository to the Codex skills directory as `footprints`:

```bash
git clone https://github.com/DevMingler/footprints-codex-skill.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/footprints"
```

Restart Codex after installation so the skill is discovered.

## Use

Invoke the skill with one or more ChatGPT export JSON files or a directory:

```text
Use $footprints to create a reflective report from /path/to/chat.json.
```

The skill applies the Footprints reflective-report prompt to all supplied
conversation files, reconstructs the active branch of each conversation, and
writes a report with dated evidence anchors. It processes the export locally.

## Skill Structure

* `SKILL.md` defines the workflow and evidence policy.
* `prompts/001-generate-reflective-report.md` is the report methodology and
  runtime source of truth.
* `docs/` contains research and design context for contributors.
* `agents/openai.yaml` provides Codex UI metadata.

---

## Relationship to Other Repositories

### footprints-bts

Source of truth.

Contains:

* Prompt evolution
* Research findings
* JSON structure analysis
* Evaluation criteria
* Sample outputs
* Design decisions
* Experimental notes

Any improvements to the Footprints methodology should begin there.

---

### footprints-custom-gpt

Public-facing implementation.

Designed for users who want a simple upload-and-report experience.

The GPT implementation consumes insights and methodologies developed through the BTS and Codex Skill repositories.

---

## Goals

The Codex Skill should:

* Analyse ChatGPT exports
* Generate meaningful reflection reports
* Surface long-term patterns
* Encourage exploration and experimentation
* Remain transparent and explainable
* Avoid unsupported conclusions

The ideal outcome is:

> "I had forgotten about that, but yes, that was important."

---

## Example Outputs

Current and future outputs may include:

### Reflection Reports

* Major projects
* Recurring themes
* Persistent questions
* Creative seasons
* Notable shifts
* Reflection summaries

### Idea Archaeology

Discover:

* Returning ideas
* Dormant ideas
* Evolving ideas
* Unexpected connections

### Timeline Reports

Identify:

* First appearance of projects
* Long-term interests
* Changes in focus
* Significant periods of activity

### Alternative Formats

Potential outputs include:

* Markdown
* HTML
* PDF
* PowerPoint
* JSON
* CSV

---

## Contributing

Contributions are welcome.

Areas of interest include:

* Prompt improvements
* Export format support
* Better project detection
* Theme extraction
* Timeline generation
* Evaluation methodology
* Output templates
* Documentation

Current implementation issue:

* [Add an optional deterministic ChatGPT export preprocessor](docs/issues/001-add-deterministic-export-preprocessor.md)

When proposing changes:

1. Explain the problem.
2. Explain the reasoning.
3. Provide examples where possible.
4. Prioritise transparency and usefulness.

---

## Design Principles

### Reflection Over Analytics

The objective is insight, not scoring.

### Explainability Over Magic

Outputs should be understandable and defensible.

### Patterns Over Moments

Long-term trends are more valuable than isolated messages.

### Signal Over Volume

Frequency alone does not determine importance.

### Human Recognition

The best report is one where the user says:

> "Yes, that feels like the path I walked."

---

## Status

Current Phase: Usable Skill, Ongoing Validation

The Codex Skill is expected to evolve significantly as:

* More exports are tested
* More evaluation cases are introduced
* More contributors participate
* Better methodologies emerge

This repository intentionally favours experimentation.

---

## License

MIT

---

## Final Thought

A conversation is a moment.

A footprint is a trail.

This repository exists to help people follow the trail.
