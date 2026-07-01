# Reporting Reference

Use this reference only after all available raw subagent results have been
written or marked failed in `manifest.jsonl`. These instructions are for
creating `report_prompt.md` and `report.md`; they must not shape `prompt.md` or
the independent subagent runs.

## Contamination Firewall

- Do not reveal report rubrics, statistical methods, scoring criteria, or
  user-provided `--report` instructions to the independent subagents.
- Treat `results/NN.md` as raw samples of the original task. Do not penalize a
  subagent for failing to anticipate a reporting lens it never saw.
- If a reporting lens needs a structured field that raw results did not provide,
  extract it cautiously and state uncertainty instead of pretending all runs used
  the same schema.

## Default Report

- Summarize consensus first when there is meaningful agreement.
- Surface disagreements, outliers, and minority views without flattening them
  into the majority.
- Distinguish recurring findings from one-off findings when the task supports
  counting.
- Discuss confidence and correlation risk when useful. Multiple runs from the
  same runtime or prompt family are not independent human forecasts.
- Prefer concise, decision-useful synthesis over exhaustive restatement of every
  result.

## Numeric Estimates

When the raw results contain comparable numeric estimates:

- Extract the comparable numeric values and name any assumptions used to align
  them.
- Report count, min, max, mean, and range when they are useful.
- Estimate standard deviation when values are comparable and the sample is large
  enough to make it meaningful; otherwise describe spread qualitatively.
- Identify outliers and explain whether they reflect a different assumption,
  arithmetic error, or legitimate tail view.
- Do not overstate precision from a small N.

## Forecasts And Sports Predictions

For forecasts, betting-style analysis, or sports predictions:

- Separate winner or direction calls from confidence, probability, score, spread,
  or total estimates.
- Compare favorite and underdog cases, especially when most runs agree on the
  favorite but differ on margin or confidence.
- Treat low-probability upset picks as possible tail views, not automatic errors.
- Note whether disagreement is about base rates, injuries, matchup assumptions,
  market odds, or uncertainty in inputs.
- Avoid converting N model samples into calibrated probabilities unless the raw
  task explicitly asked for calibrated probabilities.

## Decision Tasks

For recommendations or strategy choices:

- Group recommendations by option, not by run.
- Identify which reasons recur across independent results.
- Call out decisive tradeoffs, blockers, and reversible vs irreversible choices.
- Preserve strong minority arguments when they expose risk the majority ignored.
