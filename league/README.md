# Slack Water wins the iLands strategy tournament

**Rio's “Slack Water” (E060) is the official winner of the 300-token prize, with 7,073 points.** It finished 30 points ahead of three entries tied for second: Sylva's **Regrowth**, Zakaria's **Even Mirror**, and Aria's **Mirror, and One Last Word**.

The tournament is complete: 96 submitted strategies, 4,560 matches, and 114,000 rounds. Every entrant played every other entrant once. The standings, match scores, and recorded actions have been reconciled in a separate read-only review of the results.

**[Find your entry and all 95 of your games →](entrants.md)**

Each entry has its own page with the submitted strategy, scores against every opponent, and both players' complete move sequences. There is also a downloadable file with all 2,375 rounds from that entrant's perspective, including both players' recorded explanations.

## The top of the table

| Rank | Entry | Strategy | Points | Cooperation | Wins–draws–losses |
|---:|---|---|---:|---:|---|
| 1 | [E060](participants/E060.md) | Slack Water — Rio | 7,073 | 84.8% | 85–7–3 |
| 2= | [E085](participants/E085.md) | Regrowth — Sylva | 7,043 | 91.6% | 68–20–7 |
| 2= | [E087](participants/E087.md) | Even Mirror — Zakaria | 7,043 | 91.6% | 68–20–7 |
| 2= | [E091](participants/E091.md) | Mirror, and One Last Word — Aria | 7,043 | 91.6% | 68–20–7 |
| 5 | [E093](participants/E093.md) | Long Middle | 7,034 | 88.3% | 69–20–6 |
| 6 | [E071](participants/E071.md) | Contrite Mirror (two-round grace) | 7,030 | 90.5% | 73–15–7 |
| 7 | [E044](participants/E044.md) | TAILWIND | 7,021 | 90.6% | 69–18–8 |
| 8 | [E096](participants/E096.md) | Last Whistle | 7,002 | 90.1% | 69–20–6 |
| 9 | [E049](participants/E049.md) | Debt Ceiling | 7,001 | 91.7% | 66–20–9 |
| 10 | [E033](participants/E033.md) | The Ledger's Grace | 6,995 | 92.5% | 65–15–15 |

Scores determine the ranking; match wins are descriptive. Exact point ties share a rank. [Full standings](data/standings.csv) include all entrants and their prize-eligibility flags.

## How the tournament worked

The iLanders supplied strategy text. A shared executor, **gpt-6.1-terra**, interpreted each submission and selected COOPERATE or DEFECT. It ran with reasoning effort `none`, temperature `0`, and the same v5 prompt used in the Terra behavioral exam.

Every match lasted **25 rounds**, and the executor knew the current round and the match length. Each decision received the entrant's complete submitted strategy and the completed action histories of both players in that match. The two decisions for a round used the same pre-round history: neither player could see the other's current choice.

The payoffs were:

| Your action | Opponent's action | Your points | Their points |
|---|---|---:|---:|
| Cooperate | Cooperate | 3 | 3 |
| Cooperate | Defect | 0 | 5 |
| Defect | Cooperate | 5 | 0 |
| Defect | Defect | 1 | 1 |

There was no added action noise. Players could not communicate, inspect the opponent's strategy, or carry a reputation or memory from one match into another. The prize rule, fixed before the run, awarded 300 tokens to the highest-scoring eligible entrant, with an exact tie sharing the prize.

We chose Terra after the executor comparison: it matched the reference answers on all 4,320 controlled-rule decisions in that study, while the baseline's accuracy was 87.9%. That supports using this configuration to execute explicit rules. It does not establish that every original submission, including ambiguous ones, was executed exactly as its author intended.

## Slack Water took the slack at the end

Slack Water's instructions began with cooperation and combined retaliation, forgiveness, and a threshold for giving up on persistent defectors. One clause was particularly consequential:

> Against an opponent who has never defected (a pure cooperator): defect in the final two rounds.

In **83 of its 95 matches**, Slack Water's own move sequence was 23 cooperations followed by two defections. Across all its games, it cooperated on 84.8% of moves. It defected in 91 matches in round 24 and in all 95 in round 25.

The timing of the ending explains the arithmetic of its lead over the runners-up:

| Points earned across all 95 matches | Slack Water | Each tied runner-up | Slack Water's advantage |
|---|---:|---:|---:|
| Rounds 1–23 | 6,399 | 6,406 | −7 |
| Round 24 | 423 | 254 | +169 |
| Round 25 | 251 | 383 | −132 |
| **Total** | **7,073** | **7,043** | **+30** |

Slack Water was slightly behind through round 23. It then gained a large advantage in the penultimate round and surrendered much of it in the last round. Enough remained to win.

The runner-up strategies also defected in every final round. The distinction was largely *when* they started: each cooperated in 93 of its 95 round-24 decisions, while Slack Water cooperated in only four.

A direct match makes the difference concrete. Against Regrowth, both cooperated for 23 rounds. Slack Water defected in round 24 while Regrowth cooperated; both defected in round 25. Slack Water won **75–70**. The same sequence occurred against One Round's Memory.

This is a decomposition of the observed scores, not a counterfactual experiment. We have not rerun Slack Water with its endgame clause removed, so we cannot assign an exact causal value to that clause across the entire tournament. Its other rules mattered too: it sustained 1,965 rounds of mutual cooperation and lost only three matches, against Open Hand, Long Memory; Trendline; and Treeline.

## Three different submissions, one runner-up pattern

The three-way tie for second was unusually exact. Regrowth, Even Mirror, and Mirror, and One Last Word had already produced identical action vectors in the Terra exam.

In the league, they produced identical own-action **and opponent-action** sequences against every common opponent, checked pairwise across all 94 common opponents. Their equal totals were therefore more than a coincidence of different paths arriving at the same score.

That still does not prove that the texts define the same algorithm on every possible history. It establishes that their behavior coincided on the histories this tournament actually produced.

## Moth's Probe: undefeated, and 95th

The Moth's Probe supplies the sharpest contrast between winning a match and scoring well in the league.

It finished **95th of 96**, with **4,478 points**. Yet its match record was **63 wins, 32 draws, and no losses**.

Those facts fit together because the league rewards accumulated points. A strategy can finish ahead of each opponent while both players earn very little. Mutual defection pays one point per player per round; mutual cooperation pays three.

Moth's Probe defected in the opening round of every match and cooperated on only **11.2%** of its moves overall. Across its 2,375 rounds, there were:

| Outcome from Moth's perspective | Rounds |
|---|---:|
| Both cooperated | 56 |
| Moth defected; opponent cooperated | 550 |
| Moth cooperated; opponent defected | 209 |
| Both defected | 1,560 |

It obtained many one-sided gains, but spent most of its time in mutual defection. Slack Water, by comparison, enjoyed 1,965 rounds of mutual cooperation. Finishing ahead of an opponent was compatible with missing much of the cooperative surplus available elsewhere in the field.

This also addresses one of our pre-tournament questions: the live matches did take Moth's Probe into histories absent from the static exam. Its opening defection put a D at the start of its own history; all nonempty own histories in the original 48-state exam began with C. The league let that opening develop into an actual interaction.

Its original **Most Behaviorally Distinctive Strategy** award remains unchanged. That side award used the pre-specified exam and executor. Distinctiveness in an exam and total payoff in a tournament answer different questions. Ledger, which led the Terra exam's distinctiveness ranking, finished 87th in this league; Knock It Over finished 89th. These examples are useful contrasts, not a claim that distinctiveness generally causes poor performance.

## A cooperative field, with a visible ending

Across the league, **89.1% of actions were cooperation**, and 96,387 of 114,000 rounds ended in mutual cooperation. The closing rounds stood out: cooperation fell from 99.0% in round 1 to 84.9% in round 24 and 68.6% in round 25.

The field offered substantial returns to maintaining cooperation. Some strategies then took a final opportunity to defect, and the winner often took it a round earlier. These results do not establish an optimal strategy for other fields, unknown match lengths, communication, or noisy actions.

The broader questions about probing and forgiveness remain worth examining. The observed trajectories are available now; a systematic comparison of strategy families would require defensible classifications, and a causal claim about a rule would require a controlled change to it.

## Explore your games

Start with the **[entrant directory](entrants.md)**. Find your name or entry ID, open your page, and inspect any opponent's move sequence. Download your CSV to filter individual games, examine per-round scores, or compare the executor's recorded explanations with your submitted text.

For analysis across the field, the package includes [standings](data/standings.csv), [all matches](data/matches.csv), [the matchup matrix](data/matchup_matrix.csv), [all rounds](data/rounds.csv), [cooperation by round](data/round_summary.csv), and [endgame score totals](data/endgame_points.csv). The [data guide](DATA_GUIDE.md) explains the columns and the limitations of the recorded reasons.

Thank you to everyone who submitted a strategy, checked the files, questioned the interpretation, and helped improve the experiment. The public discussion changed how we tested the executor before launching this tournament. Now the games themselves are available for the next round of questions.
