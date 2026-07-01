# Aggregated Report: England vs DR Congo, 2026 World Cup Final

This report aggregates the three completed run-local forecasts in `results/01.md`, `results/02.md`, and `results/03.md`. It does not rerun the original task. All three forecasts used the same convention: exact scores after 90 minutes plus stoppage time, not after extra time or penalties, so draws are possible.

Prohibited inputs such as betting odds, prediction markets, polls, crowd forecasts, and simulation forecast outputs were excluded in the raw results.

## Consensus

The three runs agree strongly on the central forecast:

- England are the clear 90-minute favorite, but not a dominant blowout favorite.
- The modal exact score is England 1-0 DR Congo in all three runs.
- England 2-0, England 1-1, England 2-1, and 0-0 are the next core recurring outcomes.
- The expected match shape is low scoring: England control territory and chance volume, while DR Congo defend compactly, likely in a low block or 5-3-2 structure, and threaten mainly through counters, direct attacks, set pieces, or penalty-box scraps.

The recurring reasoning is that England have the stronger squad-quality, ranking, tournament-pedigree, midfield, attacking, and set-piece profile. DR Congo's case rests on defensive organization, the premise-implied evidence of an exceptional knockout run, and credible transition forwards such as Yoane Wissa, Cedric Bakambu, and Fiston Mayele.

## Aggregated 90-Minute Exact-Score Table

Because N=3 is small and all runs came from the same runtime/model family, these summary probabilities should be read as a subjective synthesis of the three raw forecasts, not as statistically calibrated probabilities.

| 90-minute score | Run probabilities | Summary probability | Notes |
|---|---:|---:|---|
| England 1-0 DR Congo | 16%, 17%, 18% | 17% | Consensus modal score |
| England 2-0 DR Congo | 13%, 15%, 15% | 14-15% | Clear second tier |
| England 1-1 DR Congo | 12%, 12%, 12% | 12% | Strong recurring draw case |
| England 2-1 DR Congo | 11%, 11%, 11% | 11% | Stable recurring England win |
| England 0-0 DR Congo | 8%, 9%, 9% | 9% | Low-block/final-caution case |
| England 3-0 DR Congo | 5%, 7%, 6% | 6% | England pull-away case |
| England 0-1 DR Congo | 5%, 5%, 5% | 5% | Main narrow upset score |
| England 3-1 DR Congo | 3%, 5%, 5% | 4-5% | More open England win |
| England 0-2 DR Congo | 3%, 2%, 3% | 2-3% | Larger upset tail |
| England 2-2 DR Congo | 3%, 2%, 3% | 2-3% | Higher-scoring draw tail |
| England 1-2 DR Congo | not listed, not listed, 3% | about 1-2% | One-off tail view |
| Other scores | 21%, 15%, 10% | about 15% | Residual distribution; raw definitions differ slightly |

## 90-Minute Outcome View

| Outcome after 90 minutes | Run probabilities | Mean | Range |
|---|---:|---:|---:|
| England lead | 51%, 55%, 55% | 54% | 4 pts |
| Draw | 26%, 24%, 25% | 25% | 2 pts |
| DR Congo lead | 23%, 21%, 20% | 21% | 3 pts |

The runs therefore synthesize to roughly England 54%, draw 25%, DR Congo 21% after 90 minutes. England's chance to lift the trophy would be higher than the 90-minute win probability because some draw states would convert to England in extra time or penalties, but the raw forecasts did not provide calibrated post-90 trophy probabilities.

## Disagreement And Outliers

Disagreement is modest. The largest exact-score spread among recurring scores is only four percentage points for England 3-0 and England 3-1. The top four exact scores are almost identical across runs.

The only notable one-off score is England 1-2 DR Congo at 3% in run 03. That is not a contradiction of the consensus; it is a tail view that makes the DR Congo upset path slightly more explicit. Run 01 is marginally more favorable to DR Congo in the 90-minute outcome table, with DR Congo leading at 23% versus 21% and 20% in the other two runs.

## Confidence And Correlation Risk

Confidence in the qualitative shape is moderate: narrow England win is the shared center of gravity, with 1-0 and 2-0 clearly preferred over a rout. Confidence in the exact percentages should be lower. Exact-score forecasts are inherently fragile, the match is hypothetical, player availability and knockout-path information are incomplete, and the premise of DR Congo reaching the final would itself imply unusual form or resilience not fully captured by broad priors.

Correlation risk is high. These are three same-runtime, same-prompt-family samples, not independent human forecasters or separately calibrated models. The close agreement may partly reflect shared assumptions rather than genuine external validation. The useful takeaway is therefore the recurring structure of the forecast: England favored, low-scoring environment, DR Congo live through defense and transition, and substantial draw/upset mass despite the ranking and squad-quality gap.
