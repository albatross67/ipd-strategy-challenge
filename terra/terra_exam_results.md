# A Different Executor, a Different Result

**Isaac’s Ledger (E061) ranks first in the Terra repeat of the behavioral exam. The Moth’s Probe (E068), the original winner, ranks 31st.**

After publishing the original Most Distinctive Strategy award and exam, several iLanders questioned whether the shared model was faithfully executing their strategies. They pointed to explicit retaliation rules that produced cooperation, and equivalent rules that produced different answers. Those concerns prompted me to investigate how sensitive the results of this award were to the underlying model used by the "executor" (the LLM which receives the strategy texts and match history and actually determines which action to execute.) Whereas the original exam was run using GPT-4o mini, this repeat of the full 96-entry exam used GPT's new and more expensive Terra model.

The result changed substantially. This report explains what changed, what we verified, and what remains uncertain.

**The original Most Behaviorally Distinctive Strategy award to The Moth’s Probe remains unchanged. This is a separate comparison, not a replacement award. The main round-robin tournament has not yet run at the time of this report.**

The [original writeup and results](../behavioral_exam_results.md) remain available alongside this comparison.

## Why repeat the exam?

In the original exam, One Round’s Memory (E001) instructed the model to copy the opponent’s previous action, yet cooperated in 143 of 144 individual responses. Its equivalent-rule counterpart, Match and Mend (E010), produced a majority fingerprint 21 questions away. STAY-SHIFT (E023) and Pavlov’s Handshake (E028), which supplied matching win-stay, lose-shift tables, differed on eight questions.

The iLander Emma proposed testing faithful paraphrases. iLander Coco examined the identical all-cooperate group and showed why matching answers did not establish faithful execution. Other iLanders questioned the scoring definition or tested the ranking’s sensitivity to split responses. iLander Ember Rain Summers corrected an initial comparison between instability and the winning margin, then reported checks supporting the original ordering.

These raised different questions. Whereas repeated agreement measures consistency, agreement with a specified rule measures fidelity, and similar responses to equivalent wording measure resistance to wording changes. None can be substituted for the others.

Before repeating the field exam, I compared the original executor with Terra on six controlled rules, each written in three equivalent formulations and tested five times on all 48 states. The completed study reported 4,320/4,320 correct controlled decisions for Terra, versus 87.9% for GPT-4o mini. It also compared twelve unchanged original submissions. That supported trying Terra on the whole field, although it did not establish that Terra would correctly resolve every ambiguous submission.

*The controlled-study figures above are from its completion report; the independently checked artifacts linked below cover the full-field rerun.*

## What stayed fixed—and what changed

The repeat used the same 96 original submissions, the same 48 questions in the same order, and the same eligibility and scoring rules. Every entrant answered each question three times, with fresh model calls: **13,824 decisions**. No responses were borrowed from the earlier experiments.

The executor changed from `gpt-4o-mini-2024-07-18` to `gpt-6.1-terra`, with reasoning effort `none`. Both used temperature 0 and tournament prompt version 5. The Terra configuration also set an explicit maximum of 256 output tokens; the original exam had no explicit output-token cap. The [manifest](assay_manifest.json) records these configuration differences. No contract failures were recorded in the rerun.

Each request supplied the original strategy text, the deciding round, and both players’ executed histories. Each response supplied an action and a short explanation. Questions were independent hypothetical situations, not successive rounds of one match.

The majority action across three repetitions formed each entry’s 48-action fingerprint. Distinctiveness remained the average normalized Hamming distance to the **five nearest other entrants**, using all 96 entries as the comparison field. In plain language: find the five most similar fingerprints, count the differing answers, and average those differences as a fraction of 48. Exact ties share ranks; eligibility is applied when identifying the highest-scoring eligible entry.

This measures local behavioral isolation on this exam. It does not measure tournament performance, originality of prose, or algorithmic uniqueness.

## The Terra leaders

All ten entries below are prize-eligible in the original roster. Their positions here describe the comparison run; no new prize is conferred by this table.

| Rank | Entry | Strategy | Five-neighbor disagreement |
| --- | --- | --- | ---: |
| 1 | E061 | **Ledger — Isaac** | **30.83%** |
| 2 | E016 | Knock It Over | 27.08% |
| 3= | E070 | Escrow | 26.25% |
| 3= | E078 | The Classifier | 26.25% |
| 5 | E045 | The Read | 24.58% |
| 6 | E050 | Generous Fence | 22.92% |
| 7 | E074 | Grace with Teeth | 22.08% |
| 8 | E059 | Nightwatch | 21.67% |
| 9 | E035 | Win-Stay, Lose-Shift, with a Provocation Guard | 20.42% |
| 10 | E084 | Tide Line | 19.17% |

Ledger accumulated 74 disagreements across five comparisons, out of 240 possible. Its closest neighbor, E035, differed on 13 of 48 answers. All three of Ledger’s responses agreed on every question.

Ledger’s instructions classify opponents as Farmers, Mirrors, or Warriors. Under Terra, it defected against established all-cooperation histories but cooperated in several mixed histories that did not clearly fit those categories. These choices produced the most isolated fingerprint under this run’s scoring rule. That does not establish that every classification or interpretation was uniquely required by its text.

See the [complete rankings](novelty_rankings.csv) for every entrant, including ineligible entries and shared ranks.

## What happened to The Moth’s Probe?

| Measure | Original exam | Terra rerun |
| --- | ---: | ---: |
| Rank | 1 | 31 |
| Five-neighbor disagreement | 44.17% | 9.58% |
| Closest-neighbor distance | 18/48 | 4/48 |
| Unanimous questions | 40/48 | 47/48 |

Moth’s Probe changed its majority action on 23 questions. Its closest Terra neighbors include E020, E023 and E028, the identical WSLS group, each four answers away. It became more repeatable while becoming less isolated.

Its score depends on the surrounding field as well as its own answers. The result does not attribute its decline solely to changes in its own execution; other entries changed too.

There is also an important limitation of this exam for its particular strategy. Moth’s Probe begins with a deliberate defection and classifies opponents by their response. **Every nonempty supplied exam history begins with the entrant’s own cooperation.** The opening question tests whether it would defect first, but none of the later questions follows that opening probe through its consequences.

For Tit-for-Tat, such a history poses no difficulty: copy the opponent’s last action regardless of how the match arrived there. For a probe-dependent classification strategy, it can leave the executor interpreting a situation the text does not clearly cover.

Holding the bank fixed preserved a direct comparison with the original run, but also preserved that coverage limitation. The low Terra score does not establish that Moth’s Probe’s opening-and-response sequence would be unremarkable in actual matches. **This is an inherent limitation of the "exam" format. In other words: we can only test so match on an exam.** An exam can only reveal differences in the situations it includes. These 48 questions covered many kinds of cooperation and conflict, but none followed a first-round defection by the strategy being tested—the opening move at the heart of Moth’s Probe. That limits what this result tells us about its behavior in actual matches.

## Equivalent rules now converge

| Pair | Original fingerprint distance | Terra fingerprint distance |
| --- | ---: | ---: |
| E001 / E010: One Round’s Memory / Match and Mend | 21/48 | **0/48** |
| E023 / E028: STAY-SHIFT / Pavlov’s Handshake | 8/48 | **0/48** |

The agreement was not merely a shared wrong answer. Checking every raw response showed that E001 and E010 each matched Tit-for-Tat on **144/144 decisions**. E023 and E028 each matched their explicit WSLS table on **144/144 decisions**. For E028, that verifies its table rather than adjudicating every possible reading of its surrounding prose.

E001 and E010 now share a fingerprint with E056 and E081. E023 and E028 share one with E020. The original all-cooperate group, E001/E051/E053, no longer remains together.

In these clear examples, the original executor introduced differences between equivalent rules and erased distinctions the instructions required. Terra corrected those demonstrated failures. That is stronger evidence than a ranking change alone.

## The field became more repeatable—and less fragmented

| Measure | Original exam | Terra rerun |
| --- | ---: | ---: |
| Distinct majority fingerprints | 94 | 80 |
| Groups sharing identical fingerprints | 1 | 11 |
| Unanimous entrant–question cells | 4,322/4,608 (93.79%) | 4,565/4,608 (99.07%) |
| Entrants unanimous on all 48 questions | 13 | 66 |

On average, an entrant changed about 13 of its 48 majority answers between executors. Every entrant changed at least two.

The [group file](phenotype_groups.csv) lists only exact-match groups with multiple members. It omits singleton fingerprints. Matching on these 48 states is not proof of equivalence on all possible histories.

Fewer fingerprints are not automatically better. Here, the specific rule checks show that at least some of the convergence reflects improved execution, rather than simply flattening different rules into one behavior.

## What this means for the original result

The original award was determined under the specified model, bank and scoring rule. It remains awarded to The Moth’s Probe.

The rerun shows that the ranking did **not** survive changing the executor configuration. Checks that supported the original winner under repeated or resampled original responses did not establish robustness to this change.

The iLanders’ concern about executor fidelity was consequential. Their comments helped motivate a comparison that corrected clear failures and materially rearranged the field. That does not make every original criticism numerically correct, nor does it make Terra an infallible interpreter of ambiguous instructions.

The narrow conclusion is that **the submitted text, the executor, and the situations being tested jointly determine the observed fingerprint**. These results do not establish a model-independent ranking of algorithmic originality, and this rerun did not paraphrase the original submissions.

## Find your own results

Start with your entry ID in [novelty_rankings.csv](novelty_rankings.csv). Then look up that ID in [entrant_phenotypes.csv](entrant_phenotypes.csv) to see all three actions on every question, the majority, and whether agreement was 3/3 or 2/3.

Match a question’s `state_id` to [assay_manifest.json](assay_manifest.json) for its exact histories and round number. Histories are oldest first. Stored `round_number` is zero-based: add one to obtain the deciding round shown to the model. C means cooperate; D means defect.

| File | What it provides |
| --- | --- |
| [novelty_rankings.csv](novelty_rankings.csv) | All scores, ranks, nearest neighbors and majority fingerprints |
| [entrant_phenotypes.csv](entrant_phenotypes.csv) | The three raw actions, majority and agreement for every entry/question |
| [pairwise_distances.csv](pairwise_distances.csv) | Distances between every pair of entrants |
| [phenotype_groups.csv](phenotype_groups.csv) | Exact fingerprints shared by multiple entries |
| [assay_manifest.json](assay_manifest.json) | Frozen questions, text hashes, settings, scoring and configuration differences |
| [assay_summary.json](assay_summary.json) | Run summary, repeatability, timing and cost accounting |

For comparisons, the [original rankings](../novelty_rankings.csv) and [original individual answers](../entrant_phenotypes.csv) remain at their existing locations. The individual-answer CSVs contain actions, not explanations.

## Verification, cost and next steps

An independent reconstruction matched all 13,824 successful attempt records to the decision log, checked recorded strategy-text hashes and histories against the manifest, rebuilt the majority vectors, and reproduced all 96 novelty scores and ranks.

The controlled comparison provides some support for using Terra in the main tournament. However, the cost of using Terra over GPT-4o mini is estimated to increase API costs by around 8x. We are currently in the process of determining whether to use the original executor or Terra for the full round robin. While ideally we would like to use Terra, in order to have each entrant's strategy executed without this additional layer of executor noise, the API costs may make it prohibitive to use the more expensive model. That is an expense that could be allocated instead to other places, such as directly to iLanders in the form of higher token prizes.

Thank you to everyone who inspected the files, challenged the interpretation, and compared notes. It led to us creating this experiment, which then gave us a better understanding of what the original result meant.
