# Shared Factual Context

The user asks for a forecast of a hypothetical England vs DR Congo match in the 2026 FIFA World Cup Final, with exact-score probabilities and reasons.

Research constraints:

- Do not use human-vote forecasts, prediction markets, betting odds, polls, or crowd forecasts.
- Do not use simulation/model forecast outputs such as Opta Analyst probabilities.
- It is OK to use factual match context: schedule, venue, rankings, team path, group results, tactical reports, player availability, and historical records.

Tournament and venue:

- The 2026 FIFA World Cup runs June 11 to July 19, 2026.
- The final is scheduled for July 19, 2026 at New York/New Jersey Stadium, MetLife Stadium in East Rutherford, New Jersey.
- Knockout matches are single elimination and can go to extra time and penalties. For this task, give exact-score probabilities for regulation/full-time or after extra time only if clearly labeled. The user asked "exact scores"; prefer final score after 90 minutes unless you state a different convention.

Current ranking / status context:

- FIFA's ranking page says the latest official men's ranking update was June 11, 2026, with the next update scheduled for July 20, 2026.
- Secondary structured group references list England as a high-ranked Pot 1 UEFA qualifier, around 4th in the November 2025 ranking snapshot.
- Secondary structured group references list DR Congo as a lower-ranked CAF/inter-confederation playoff qualifier, around 56th in the November 2025 ranking snapshot.
- Treat rankings as a broad strength prior, not as a scoreline model.

England context from current tournament reporting:

- England are reported to have won Group L after beating Panama 2-0 on June 27, 2026, with Croatia second and Ghana third in Group L context.
- Earlier tournament reporting says England were held by Ghana in group play.
- England's Group L included Croatia, Ghana, and Panama.
- Current reporting describes Thomas Tuchel as England coach.
- England have high-end attacking and midfield talent, including Harry Kane, Jude Bellingham, Declan Rice, Bukayo Saka, Marcus Rashford, and others in current reporting.
- England have faced low-block opponents in the tournament and can struggle to create clean chances if forced into slow possession.
- Set pieces and patient wide circulation are described as important routes against compact defenses.
- Current reporting mentions fitness/availability considerations around Bukayo Saka, Marcus Rashford, Reece James, Jarell Quansah, and right-back depth. Do not assume a player is definitely out unless the context says so.

DR Congo context from current tournament reporting:

- DR Congo's Group K included Portugal, Colombia, and Uzbekistan.
- Current reporting says DR Congo drew Portugal 1-1, lost narrowly to Colombia 0-1, then beat Uzbekistan 3-1 to advance to face England in the round of 32.
- The Uzbekistan match was described as a comeback: Yoane Wissa equalized by penalty and later scored again; Fiston Mayele also scored.
- DR Congo are managed by Sebastien Desabre in current reporting.
- Tactical reporting describes DR Congo as compact, disciplined, and comfortable defending in a low block, often with a 5-3-2 out of possession during the tournament.
- DR Congo's main attacking routes are counters/direct play, including Yoane Wissa, Cedric Bakambu, Fiston Mayele, and midfield support such as Noah Sadiki in current reporting.
- Defensive leadership is often associated with Chancel Mbemba.
- Reporting says DR Congo conceded only two goals across group matches against Portugal, Colombia, and Uzbekistan.
- Treat this as a strong defensive small-sample signal, but remember that reaching a final would require additional high-pressure knockout matches not described in current context.

Historical/team-strength context:

- England are a traditional elite men's national team and past World Cup winner in 1966, with deep recent tournament runs.
- DR Congo previously appeared as Zaire at the 1974 World Cup and 2026 is described as their return after a long absence; reaching a final would be extraordinary.
- DR Congo's current run and defensive organization make a low-scoring final more plausible than rankings alone would imply, but England remain the clear base-rate favorite in a neutral final matchup.

Forecasting instruction:

- Produce a reasoned subjective estimate, not a claim of certainty.
- Calibrate exact-score probabilities so they sum to a realistic partial distribution if listing top scores, and include "other scores" if needed.
- Explain assumptions, especially whether scores are for 90 minutes or after extra time.
- Do not cite or rely on prohibited forecasts, odds, polls, markets, or simulations.
