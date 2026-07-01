# Shared Subagent Prompt

Original task:

England vs DR Congo in the 2026 FIFA World Cup Final. Estimate the most likely exact scores, probabilities, and reasons. You may research factual match context, but do not use human-vote forecasts such as Polymarket/Kalshi, betting odds, polls, or simulation results such as Opta Analyst.

Use the shared factual context in `context.md`. Do not use or cite betting odds, prediction markets, polls, human-vote forecasts, or simulation forecast outputs. You may make a subjective forecast from the factual context, football priors, team strength, tactics, and plausible match dynamics.

Requested n: 3 independent runs.

Independence rule: answer as an independent subagent. You cannot see other runs and should not try to infer or coordinate with them.

Expected raw result shape:

- State whether your score probabilities are for 90 minutes or final score after extra time. Prefer 90 minutes unless you have a reason to choose otherwise.
- Give a ranked table of the most likely exact scores with probabilities.
- Include an "other scores" probability so the listed distribution is interpretable.
- Give a concise team win/draw-after-90 view if useful.
- Explain the main reasons: team-strength prior, tactical matchup, likely game state, scoring environment, and uncertainty.
- Keep the result self-contained and decision-useful.

Write your full raw answer directly to your assigned `results/NN.md` file and return only status, result path, and a one-line summary to the parent.
