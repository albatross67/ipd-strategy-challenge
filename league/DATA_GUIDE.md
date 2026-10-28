# Using the tournament files

[Results](README.md) · [Find your entry](entrants.md)

## Start with your entry

1. Search the [directory](entrants.md) for your name, strategy, or entry ID.
2. Open your entry page. It lists all 95 opponents, scores, and full move histories.
3. Open the linked personal CSV and use GitHub's **Download raw file** control. Filter `opponent_id` in a spreadsheet to see one game's 25 rounds. If giving the file to an assistant, ask it to distinguish recorded actions from the model's stated reasons.

Every participant page and personal CSV is oriented to that participant: “own” means the entry named in the filename. An entry's own move is simultaneous with the opponent's move in the same row; neither had access to the other's current action when deciding.

## File inventory

| File | Contents |
|---|---|
| `participants/E###.md` | One entrant's summary, verbatim submitted strategy, and all 95 match histories |
| `games/E###.csv` | 2,375 rounds from that entrant's perspective, with both players' actions, points, cumulative points, reasons, and fingerprints |
| `data/standings.csv` | Original full standings; ranking, names, eligibility, scores, cooperation, wins/draws/losses |
| `data/matches.csv` | Original match file, renamed only; 4,560 pairings and both 25-action sequences |
| `data/matchup_matrix.csv` | Original matrix: row entrant's score against column entrant; diagonal is not a match |
| `data/rounds.csv` | Original 114,000 rounds, one row per pair per round, including both decision fingerprints |
| `data/round_summary.csv` | Derived cooperation counts and rates for rounds 1–25 across all games |
| `data/endgame_points.csv` | Derived per-entrant points for rounds 1–23, round 24, and round 25 |
| `data/league_manifest.json` | Original frozen league configuration, rules, strategy hashes, and source provenance |
| `data/PRE_RESULT_NOTE.md` | Original questions and rationale written before results |
| `data/system_prompt.txt` | Common executor instructions reconstructed directly from the attempt log |
| `data/review_summary.json` | Derived audit counts, cost reconciliation, and endgame totals |
| `data/SHA256SUMS.txt` | Checksums of the public files, excluding this checksum file itself |

Entry IDs are the authoritative lookup keys. There are 96 entries; E048 is absent, so IDs run through E097. Strategy names can be similar or duplicated. `Ledger` (E061) and `The Ledger` (E051), for example, are different entries.

## Personal round CSV columns

| Column | Meaning |
|---|---|
| `entry_id`, `opponent_id`, `opponent_strategy` | The participant whose file this is, and their opponent |
| `match_id` | Stable pair ID, such as `E060__E085` |
| `round` | Human-readable round number, 1–25 |
| `own_action`, `opponent_action` | Executed C (cooperate) or D (defect); no added action noise |
| `own_payoff`, `opponent_payoff` | Points earned in this round |
| `own_cumulative_points`, `opponent_cumulative_points` | Points through and including this round; reset for each match |
| `own_reason`, `opponent_reason` | One-sentence explanations returned with the saved decisions |
| `own_fingerprint`, `opponent_fingerprint` | References linking the row to the saved decision and the original round records |

The personal CSVs duplicate each game's data from both participants' perspectives. **Do not combine all 96 personal files and count their rows as distinct rounds:** doing so counts each round twice. Use `data/rounds.csv` for league-wide round totals.

Reasons are generated text, not ground truth about internal reasoning. They may be incomplete, inconsistent with the strategy, or mistaken about the history. Judge rule-following against the actual submission and supplied history. A repeated fingerprint identifies reuse of one saved decision, not an independent agreement by the model.

## Scores and ranks

Each entrant played 95 matches of 25 rounds, making 2,375 individual actions. Total points determine rank; exact ties share competition rank (for example 1, 2, 2, 2, 5). Match W/D/L compares the two scores in each match. A player can win many matches with low absolute scores.

Cooperation rates are fractions in the CSVs and percentages in the Markdown pages. Historical points are stored as decimal strings in some original files even though the game's payoffs are integers. The derived personal files use integer points.

## Provenance and limits

The original CSVs, manifest, and pre-result note are copied without altering their bytes. Participant pages, personal CSVs, summaries, and the results report are derived views. Submitted strategy text was recovered from the saved execution requests and verified against the manifest's SHA-256 hashes. Each personal reason was joined by fingerprint to the saved response supporting that action.

This package publishes results and data, not implementation code. Raw provider payload logs, response IDs, and operational error logs are retained for review rather than included here. The manifest references a source snapshot that is not part of this public package. The public checksums detect changes to these files; they do not independently authenticate provider execution.

This is one completed league under the recorded configuration, with saved-response reuse across matching requests. The reports do not claim that all submissions are unambiguous, that every choice was faithful, or that standings would be unchanged in a fresh run. The earlier behavioral-exam award remains a separate result.
