---
name: askntimes
description: "Explicit slash-command skill for native subagent runtimes. Tested with Codex; Claude Code support is best-effort until verified. Use only when the user's message begins with /askntimes, optionally followed by flags such as --n 3. Do not trigger for natural-language requests to spawn agents, run multiple reviewers, or get independent attempts."
---

# Ask N Times

Trigger this skill only for explicit slash-command invocations:

- `/askntimes TASK`
- `/askntimes --n 3 TASK`
- `/askntimes --output-dir PATH TASK`
- `/askntimes --n 3 TASK --report highlight differences`
- `/askntimes --n 3 --report "highlight differences" -- TASK`

Do not use this skill for ordinary natural language, even if the user asks to
spawn N agents, run multiple reviewers, or collect independent attempts. Handle
those requests with the runtime's normal tools and behavior.

`/askntimes TASK` means:

```text
Spawn N independent subagents to TASK, then generate a report from their results.
```

## Invocation

- N defaults to 3. Parse it from `--n 5`, `--n=5`, `n=10`, etc.
- Batch size defaults to 5. Parse it from `--batch-size 4`,
  `--batch-size=4`, `batch-size=4`, etc. It must be positive.
- Output home defaults to `~/Documents/AskNTimes`. Parse overrides from
  `--output-dir PATH` or `--output-dir=PATH`.
- Optional report instructions can appear as `TASK --report TEXT`,
  `--report "TEXT" TASK`, `--report=TEXT TASK`, or `report="TEXT"`. They are
  report-only instructions for `report_prompt.md`, not instructions for the
  independent subagents.
- When `--` appears, treat everything after it as task text and stop parsing
  flags.
- If requested `n > 5` or batch size `> 5`, warn that the run may be slower,
  costlier, and correlated because samples come from the same runtime and
  prompt family. If `n > 20` or batch size `> 20`, ask for explicit
  confirmation before launching.

## Core Rules

- Give every subagent the same task. This samples one judgment; it does not
  divide work.
- Do not answer the task yourself first. Create `prompt.md`, launch subagents
  from it, wait for results, then create `report_prompt.md`.
- Keep sampling and reporting isolated. Report rubrics, aggregation methods,
  and user-provided `--report` instructions must not affect `prompt.md` or any
  independent subagent run.
- Use supervisor pre-research in auto mode. Before creating `prompt.md`, decide
  whether the task depends on current, local, market, legal, medical, product,
  schedule, price, odds, roster, injury, or other unstable external facts. If it
  does and the user has not forbidden research, research first and write
  sanitized facts and sources to `context.md`.
- Do not perform hidden supervisor research after subagents have started. Any
  research that informs the run must happen before `prompt.md` is finalized and
  must be visible through `context.md`.
- If the runtime cannot launch independent native subagents, stop and say the
  runtime is unsupported rather than simulating independence in one
  conversation.

## Run Bundle

Before launching subagents, create a run bundle when file access is available:

```text
~/Documents/AskNTimes/runs/YYYYMMDD-HHMMSS-slug/
```

If the user passes `--output-dir PATH`, create the bundle at:

```text
PATH/runs/YYYYMMDD-HHMMSS-slug/
```

If the selected home is outside the writable sandbox, fall back to
`.askntimes/runs/YYYYMMDD-HHMMSS-slug/` and tell the user which path was used.
Do not ask for elevated filesystem permissions just to use the default output
home. Do not support environment-variable overrides or config files in this
version.

After creating the bundle, send a brief progress update with a clickable link
to the run directory when supported. Use an absolute Markdown file link, and
wrap paths with spaces in angle brackets.

The run bundle should contain:

- `request.md` - audit record of the raw invocation, parsed fields, warnings,
  supervisor decisions, and light source audit when pre-research used external
  sources. It is not an execution input and must not be shown to subagents.
- `context.md` - subagent-visible source material: background, long documents,
  code snippets, evidence, constraints, and allowed pre-research facts.
- `prompt.md` - the exact shared prompt every subagent receives.
- `results/NN.md` - one raw result per subagent, numbered from `01`.
- `manifest.jsonl` - authoritative index, one JSON object per result.
- `references/reporting.md` - run-local snapshot of the reporting reference.
- `report_prompt.md` - the exact prompt for the report-generation subagent.
- `report.md` - the final report generated from `report_prompt.md`.

Keep `context.md` factual and subagent-visible. Do not include report-only
instructions, `--report` text, aggregation rubrics, statistical analysis
instructions, references to `request.md`, or references to
`references/reporting.md`.

## Prompt And Results

`prompt.md` must include:

- the original user task, preserving relevant context
- a reference to `context.md` when shared context exists
- the requested `n`
- the independence rule
- the expected raw result shape, if useful
- constraints that should be identical across all runs

`prompt.md` must not include report-generation instructions, scoring rubrics,
aggregation methods, statistical analysis instructions, references to
`references/reporting.md`, or any user-provided `--report` instruction.

Spawn every subagent from `prompt.md`. Do not hand-write slightly different
prompts per subagent unless the user explicitly asks for a diversity
experiment. Launch in batches, defaulting to batch size 5 and honoring
user-provided batch size without silently clamping it. If a known runtime limit
is lower than the requested batch size, stop and ask for a smaller value.

When the runtime supports subagent file writes, instruct each subagent to write
its full raw answer directly to its assigned `results/NN.md` and return only
status, result path, and a one-line summary. If subagents cannot write files,
collect their outputs in conversation and write `results/NN.md` as a fallback.
Update `manifest.jsonl` after each batch.

Use these default manifest fields:

```text
{"run_id":"01","context_path":"context.md","prompt_path":"prompt.md","result_path":"results/01.md","status":"complete","one_line_summary":"..."}
```

Optional observed metadata may include `runtime`, `model`, `started_at`,
`completed_at`, `latency_ms`, `input_tokens`, `output_tokens`, `total_tokens`,
`error`, or `tags`. Omit unknown metadata rather than guessing or writing `0`.
Aggregate stats should be derivable from `manifest.jsonl`; do not add a
separate stats file unless a later workflow needs it.

## Report Generation

After all available raw results are written or marked failed in
`manifest.jsonl`, copy the skill's `references/reporting.md` into the run
bundle. Treat it as a reproducibility snapshot. `prompt.md` and
`report_prompt.md` should reference only run-local relative paths, never
absolute paths to the skill installation.

Create `report_prompt.md` only after the manifest is final. It must include:

- the original user task
- the requested `n`
- links to `manifest.jsonl` and every available `results/NN.md`
- a reference to `context.md` when shared context exists
- a reference to `references/reporting.md`
- instructions to aggregate raw results rather than rerun the task
- instructions to report consensus, disagreement, outliers, confidence,
  correlation risk, and recurring versus one-off findings when useful
- any user-provided `--report` instruction, clearly labeled as an additional
  report instruction

Launch one report-generation subagent from `report_prompt.md` and have it write
`report.md`. The report subagent should not see hidden scratch work or prior
conversation beyond the files referenced by `report_prompt.md`.

The final user-facing answer should present `report.md` or a concise relay of
it. If supervisor pre-research used external sources, briefly mention or link
the key sources when useful. If a QA pass finds an issue, do not silently
rewrite the report; fix `report_prompt.md` and regenerate `report.md`, or note
the unresolved issue.

If the runtime cannot write files, still create the shared prompt visibly before
launching subagents. After raw runs complete, create a visible
report-generation prompt and use it to produce the final report.

## Runtime Support

This skill is tested with Codex native subagents. Other native-subagent runtimes
are best-effort until verified with a transcript showing slash-command
triggering, shared `prompt.md`, separate raw results, `report_prompt.md`, and
run bundle paths.
