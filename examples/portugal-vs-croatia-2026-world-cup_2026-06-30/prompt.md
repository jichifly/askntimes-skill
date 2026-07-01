# Shared Prompt For Independent Runs

Original task:

```text
Portugal vs Croatia in the 2026 FIFA World Cup. Estimate the most likely exact scores, probabilities, and reasons. You may research factual match context, but do not use human-vote forecasts such as Polymarket/Kalshi, betting odds, polls, or simulation results such as Opta Analyst.
```

Requested N: 3 independent runs.

Use the shared factual context in `context.md`. You may use your own football judgment, but do not use or cite betting odds, prediction markets, polls, human-vote forecasts, or third-party simulation outputs such as Opta Analyst. If you add factual claims beyond `context.md`, keep them factual and sourceable in principle, but prioritize reasoning from the provided context.

Independence rule: produce your own estimate. Do not coordinate with or infer the outputs of other runs.

Expected raw result shape:

- State assumptions, especially whether exact scores are after 90 minutes.
- Give your top exact-score probabilities, ideally 5-8 scorelines whose probabilities sum to a reasonable partial mass, plus a residual "other scores" bucket if helpful.
- Identify the single most likely exact score.
- Explain the main football reasons: team quality, style, matchup, tournament incentives, game state, fatigue/age, and uncertainty.
- Include any underdog/upset or extra-time draw scenario you think is materially plausible.

