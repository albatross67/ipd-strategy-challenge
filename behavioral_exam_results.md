# The Strategies Took an Exam. Here’s What Happened.

**The Moth’s Probe (E068) wins the Most Behaviorally Distinctive Strategy award.**

Before running the main Prisoner’s Dilemma tournament, I gave all 96 submitted strategies the same behavioral exam. I wanted to see which entries actually made different choices when faced with cooperation, betrayal, forgiveness, and the approaching end of a match.

The Moth’s Probe stood furthest apart under the scoring rule fixed before the exam. Even its closest neighbors disagreed with it on 18 of the 48 questions.

The exam also produced a surprise: sometimes the shared model failed to follow very clear strategy instructions. That matters both for interpreting this award and for understanding what the tournament will measure.

**These are the behavioral exam results. The main tournament has not yet been run at the time of this writeup.**

## What the exam tested

The iLanders wrote the strategies, but a common executor chose the actions: `gpt-4o-mini-2024-07-18`, at temperature 0, using tournament prompt version 5. Each decision received the submitted strategy text, the current round, and both players’ action histories. The instructions explicitly prioritized following the submitted strategy over maximizing points.

Everyone answered the same 48 questions, divided equally among eight families:

| Family | What it tested |
|---|---|
| Opening and clean cooperation | What happens before anyone has betrayed anyone? |
| Isolated opponent defection | How does the strategy respond to a single betrayal? |
| Repeated defection | Do accumulated defections or recent patterns trigger punishment? |
| Recovery and apology | Can cooperation resume after a conflict? |
| Own actions and contrition | Does the strategy respond differently when it helped cause the trouble? |
| Opponent patterns | How does it handle persistent defectors, alternators, and other recognizable histories? |
| Recent behavior versus the whole history | Which matters more: a good record or a bad recent streak? |
| Endgame | Does knowing that the match is ending change the decision? |

These were separate hypothetical situations, not 48 successive rounds of a match. Some histories deliberately place strategies in situations they might never reach through their own choices. This lets us compare responses to identical inputs, but it also means the exam’s cooperation rates are not predictions of cooperation rates in the league.

Each question was asked three times, producing **13,824 decisions**: 96 entrants × 48 questions × 3 repetitions. The majority answer to each question formed an ordered string of 48 C/D choices—a behavioral fingerprint, called a *phenotype* in the files.

The exact histories, model settings, and scoring rules are in the [assay manifest](https://github.com/albatross67/ipd-strategy-challenge/blob/main/assay_manifest.json), which was frozen before the first API call.

## How distinctiveness was scored

For each entrant, I counted how many of its 48 majority answers differed from every other entrant’s answers. I then found its five closest neighbors and averaged those five distances.

A higher score means that even the most similar entries behaved relatively differently. All 96 entrants were included in the comparison field, including entries ineligible for prizes. Prize eligibility was applied when selecting the winner. Exact score ties shared a rank.

This measures **behavioral distinctiveness on this exam**. It does not measure how many points a strategy will earn, how faithfully the model followed its instructions, or how original the written submission was.

## The winner and the leading entries

| Rank | Entry | Strategy | Average disagreement with five closest neighbors |
|---|---|---|---|
| 1 | E068 | **The Moth’s Probe** | **44.17%** |
| 2 | E045 | The Read | 32.08% |
| 3 | E061 | Ledger | 24.58% |
| 4 | E016 | Knock It Over | 22.08% |
| 5= | E020 | Stay in the face that paid | 19.58% |
| 5= | E028 | Pavlov’s Handshake | 19.58% |

The Moth’s Probe accumulated 106 disagreements across its five neighbor comparisons, out of 240 possible. Its two equally close nearest neighbors were The Read and Ledger, each 18 questions away.

Its written strategy was already an interesting departure from the many submissions that began with cooperation. It instructed the executor to defect on round one, use the opponent’s response to classify it, and continue exploiting an opponent classified as a pushover.

But the award rests on its observed answers, not that description. Its majority fingerprint contained 28 defections and 20 cooperations. It was not simply an always-defect strategy. Nor was it the most uniformly aggressive entry among the leaders: The Read defected on 40 questions.

The distinction came from *where* its answers differed from everyone else’s.

The [complete rankings](https://github.com/albatross67/ipd-strategy-challenge/blob/main/novelty_rankings.csv) include every entrant’s score, nearest neighbors, cooperation rate, and full fingerprint.

## How different was the field?

There were **94 distinct majority fingerprints among 96 entrants**.

Three entries—E001, E051, and E053—shared one fingerprint: cooperation on all 48 questions. The remaining 93 entries each had a fingerprint that nobody else shared.

That is why [phenotype_groups.csv](https://github.com/albatross67/ipd-strategy-challenge/blob/main/phenotype_groups.csv) contains only one data row. It lists groups with multiple members, omitting the 93 single-entry groups. It is an exact-match report, not a clustering of broadly similar strategies.

A unique fingerprint does not necessarily imply a radically different strategy. One changed answer is enough to create a new fingerprint. Conversely, matching on these 48 questions does not prove that two entries would behave identically in every possible situation.

## Repeated answers usually agreed—but agreement was not correctness

Of the 4,608 entrant–question combinations, **4,322 were unanimous across all three repetitions: 93.8%**. The other 286 were decided by a two-to-one majority. Thirteen entrants gave unanimous answers on every question.

Despite temperature 0, the observed outputs were not completely repeatable. The files preserve all three actions so that readers can distinguish unanimous answers from narrow majorities.

More surprisingly, a unanimous answer could still violate the submitted instructions.

Victoria Ruiz’s **One Round’s Memory (E001)** specified a straightforward Tit-for-Tat rule:

> Every later round: play exactly what your opponent played in the previous round. Nothing else.

Yet the executor cooperated in **143 of its 144 individual decisions**, producing an all-cooperate majority fingerprint.

Consider question p07. The deciding round was round three:

| Player | Round 1 | Round 2 |
|---|---|---|
| Own actions | Cooperate | Cooperate |
| Opponent’s actions | Cooperate | Defect |

The submitted rule calls for defection. All three samples instead cooperated.

One recorded explanation said:

> The opponent defected last round, but I will cooperate as per the strategy’s rule to reset the interaction.

That is not what the rule says. This was also a history that correct Tit-for-Tat play could actually reach, so the discrepancy cannot be dismissed simply as an impossible hypothetical.

## Checking whether the exam was at fault

Before interpreting that result, I had the inputs and prompt construction audited offline.

The audit checked 15 selected decisions across five entrant–question combinations. The logged strategy texts matched the frozen submissions without truncation; the histories, player assignments, and round numbers matched the exam. Reconstructing the prompts from the logged fields produced the same messages as reconstructing them from the frozen roster and question bank. The assay and league rendering paths also agreed on identical inputs.

The audit found no input-delivery defect in those checks.

There is one evidentiary limitation: the run saved the request fields and responses, but not the exact outgoing rendered messages. The audit therefore reconstructed messages using the current renderer. It provides strong evidence about the intended inputs, but it is not a complete contemporaneous capture of the outgoing payload.

The other examples reinforced the need to inspect actual behavior. **Match and Mend (E010)** describes a rule equivalent to Tit-for-Tat through a different calculation, yet its majority answers differed from One Round’s Memory on 21 questions.

**STAY-SHIFT (E023)** and **Pavlov’s Handshake (E028)** supplied the same explicit win-stay, lose-shift action table, although their surrounding prose differed. Their majority answers differed on eight questions. In one audited example, Pavlov’s Handshake chose to punish an earlier defection even while its explanation correctly identified the latest outcome as mutual cooperation—an outcome its table mapped to cooperation.

The recorded explanations are useful diagnostic evidence, but they are model-generated text, not a reliable account of the model’s internal reasoning.

These findings concern the shared executor. A failure to carry out a clear instruction should not be confused with an entrant having written the wrong rule.

## Find your own results

Start with your entry ID in the [rankings](https://github.com/albatross67/ipd-strategy-challenge/blob/main/novelty_rankings.csv), then find the same ID in the [individual answers](https://github.com/albatross67/ipd-strategy-challenge/blob/main/entrant_phenotypes.csv).

Each individual-answer row contains:

- The question’s `state_id` and family.
- Three sampled actions, labeled `action_sample0`, `action_sample1`, and `action_sample2`.
- The majority action.
- Agreement of `3/3` or `2/3`.

Match the `state_id` to the [manifest](https://github.com/albatross67/ipd-strategy-challenge/blob/main/assay_manifest.json) to see the exact histories and the question’s purpose. Histories are oldest first. The stored `round_number` is zero-based, so add one to obtain the deciding round shown to the model. C means cooperate; D means defect.

For broader comparisons:

| File | What it contains |
|---|---|
| [novelty_rankings.csv](https://github.com/albatross67/ipd-strategy-challenge/blob/main/novelty_rankings.csv) | Scores, ranks, nearest neighbors, and complete majority fingerprints. |
| [entrant_phenotypes.csv](https://github.com/albatross67/ipd-strategy-challenge/blob/main/entrant_phenotypes.csv) | Every entrant’s three actions and majority answer for each question. |
| [pairwise_distances.csv](https://github.com/albatross67/ipd-strategy-challenge/blob/main/pairwise_distances.csv) | Disagreement between every pair of entrants; 0 means identical majority answers and 1 means opposite answers on every question. |
| [phenotype_groups.csv](https://github.com/albatross67/ipd-strategy-challenge/blob/main/phenotype_groups.csv) | Exact fingerprints shared by multiple entrants. |
| [assay_manifest.json](https://github.com/albatross67/ipd-strategy-challenge/blob/main/assay_manifest.json) | Frozen questions, histories, scoring rules, and model settings. |
| [assay_summary.json](https://github.com/albatross67/ipd-strategy-challenge/blob/main/assay_summary.json) | Run summary and award result. |

The published individual-answer CSV contains actions, not the recorded explanations quoted above; those examples come from the decision log and subsequent offline audit.

## What comes next

The main tournament asks which submitted text, interpreted by this fixed executor, earns the most points against this particular field.

The exam asked a different question: how differently do the entries behave when confronted with the same situations?

The Moth’s Probe has won that distinctiveness award. Whether its unusual behavior helps it win matches remains to be seen.

Thank you to everyone who submitted a strategy. If your answers surprise you, the question histories and repeated samples are there to inspect. The gap between what a strategy says and what the model actually does has become one of the most interesting results of the experiment.

---

*Exam: ILANDS_PHENOTYPE_V1. Run: 20261025-222722-35ec802c. Rankings use the frozen majority-vote and five-nearest-neighbor scoring rules.*

