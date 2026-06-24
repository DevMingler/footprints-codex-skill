# Footprints Codex Skill

An installable Codex Skill for creating evidence-grounded reflective reports
from ChatGPT conversation exports.

Footprints looks across an export for sustained projects, recurring themes,
persistent questions, shifts in focus, and unfinished ideas. The aim is
reflection, not analytics, scoring, diagnosis, or profiling.

This repository is contributor-facing. The research history and broader
philosophy belong in
[footprints-bts](https://github.com/DevMingler/footprints-bts); the public
upload-and-report experience belongs in
[footprints-custom-gpt](https://github.com/DevMingler/footprints-custom-gpt).

## Quick Start

Clone this repository into the Codex skills directory as `footprints`:

```bash
git clone https://github.com/DevMingler/footprints-codex-skill.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/footprints"
```

Restart Codex so the skill is discovered.

Invoke it with a ChatGPT export file or directory:

```text
Use $footprints to create a reflective report from /path/to/chat.json.
```

Accepted inputs:

* `chat.json`
* `conversations.json`
* numbered `conversations-*.json` chunks
* a directory containing those files

The skill treats supplied conversation files as one export unless the user says
otherwise. It processes the export locally through Codex.

## Repository Map

* `SKILL.md` is the Codex entrypoint and workflow.
* `prompts/001-generate-reflective-report.md` is the runtime methodology and
  report prompt.
* `docs/chatgpt-export-schema.md` documents the ChatGPT export structure.
* `docs/report-design-v1.md` captures report design decisions.
* `docs/issues/` holds scoped implementation notes and proposed improvements.
* `examples/` contains a small sample export and generated report.
* `agents/openai.yaml` provides Codex UI metadata.

There is no build step or dependency install today; the skill is prompt and
documentation driven.

## Contributor Workflow

1. Start with `prompts/001-generate-reflective-report.md` for behavior changes.
2. Update `SKILL.md` when invocation, input handling, or workflow changes.
3. Follow `docs/prompt-numbering.md` when changing prompt behavior or examples.
4. Use `footprints-bts` for deeper methodology, evaluation, and research notes.
5. Test changes against representative exports before updating examples.
6. Keep reports grounded in dated evidence anchors from the user's messages.

## Report Guardrails

Reports should:

* reconstruct the active conversation branch from `current_node`;
* prioritize user-authored messages over assistant text;
* use conversation titles as hints, not standalone evidence;
* identify patterns across the full available date range;
* disclose incomplete input briefly when relevant;
* avoid unsupported conclusions, sensitive inferences, scores, rankings,
  diagnoses, and personality labels.

Do not commit private exports or generated reports unless they are synthetic,
sanitized, or intentionally included as examples.

## Related Repositories

* [footprints-bts](https://github.com/DevMingler/footprints-bts): source of
  truth for research, prompt evolution, evaluation, philosophy, and design
  decisions.
* [footprints-custom-gpt](https://github.com/DevMingler/footprints-custom-gpt):
  user-facing Custom GPT implementation and assets.

## Status

Usable and experimental. Expect the prompt, report structure, export handling,
and evaluation approach to evolve as more exports are tested.

## License

MIT
