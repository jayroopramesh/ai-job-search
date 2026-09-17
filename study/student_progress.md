# Student Progress — Jayroop

Sprint: **2026-09-17 → 2026-10-14** (DL4H [OXFORD] + IntroML [AUS]) · CV long track [OXFORD] → 2026-11-15
State file is authoritative (TUTOR.md §4/§8). Updated at the end of every window; committed and pushed each time.

## Scoreboard
- Sessions completed: **2 / 84** sprint windows (3/day × 28) · missed: 0
- Retention (7-day rolling pass rate): **43%** (2 ✅ · 2 🟡 · 3 ❌ of 7, D1 baseline pt 1)
- Ledger items: 7 · due tomorrow (D2, 09-18): **5**
- 🚩 Flag points — open: **5** (4 concept + 1 pattern) · cleared: 0
- Mocks: #0 — · #1 — · #2 — · #3 — · AUS oral — · OXFORD oral — · final —

## 🚩 Flag Points (active attack list)
| # | Concept | Course | Aud. | First missed | Angle history (formats tried) | Consec. passes | Status |
|---|---|---|---|---|---|---|---|
| FP-1 | **Why an unscaled attribute dominates KNN** — answered "age and loan aren't correlated"; the real cause is *magnitude/scale*, not correlation. Right answer, wrong mechanism. | IntroML | [AUS] | 2026-09-17 | intuition | 0 / 3 | 🔴 open |
| FP-2 | **Cosine vs Euclidean on text** — could not say why Euclidean ties the two document pairs; angle detail wrong (said 180°, orthogonal is 90° / cos = 0). | IntroML | [AUS] | 2026-09-17 | compare | 0 / 3 | 🔴 open |
| FP-3 | **GINI impurity extremes inverted** — said GINI is maximal at a 0/100 split; that is the *minimum* (pure node). Max is at equal class distribution. Also conflated GINI with entropy. | IntroML | [AUS] | 2026-09-17 | open | 0 / 3 | 🔴 open |
| FP-4 | **Precision and recall swapped** — described high-precision/low-recall as "catch lots of fish but few red", which is low precision. Highest-priority flag: this is the most common ML interview killer. | IntroML | [AUS] | 2026-09-17 | intuition | 0 / 3 | 🔴 open |
| FP-5 | **PATTERN: directional inversion.** When a concept has two poles, the wrong pole gets picked (GINI max↔min, precision↔recall). Not a content gap — a retrieval-direction gap. Drill: 2 "which pole, and what does the other pole look like?" items per window until 80% over a rolling week. | both | both | 2026-09-17 | — | 0 / 3 | 🔴 open |

## Ledger (spaced repetition)
Intervals 1→3→7→14→30 days. ✅ advance · 🟡 repeat · ❌ reset to 1d + flag.
| Item (one testable assertion/skill) | Course | Aud. | Interval | Last seen | Next due | Lapses |
|---|---|---|---|---|---|---|
| Unscaled features let the large-magnitude attribute dominate the distance metric (KNN) | IntroML | [AUS] | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |
| Effect of k: too small → noise-sensitive; too large → neighbourhood pulls in other classes | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |
| Euclidean counts mismatched positions and ties unrelated doc pairs; cosine measures angle/overlap | IntroML | [AUS] | 1d ❌ | 2026-09-17 | 2026-09-18 | 1 |
| Validation set estimates generalization error during model building; test set stays untouched | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |
| GINI measures node impurity: max at equal class distribution, min (0) at a pure node | IntroML | [AUS] | 1d ❌ | 2026-09-17 | 2026-09-18 | 1 |
| Precision = of what you caught, how much is red; Recall = of all red, how much you caught | IntroML | [AUS] | 1d ❌ | 2026-09-17 | 2026-09-18 | 1 |
| Occam's Razor: given equal generalization error prefer the simpler model (complex models fit accidentally) | IntroML | [AUS] | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |

## Session log
| Date | Window | Type | Items | Score | Notes |
|---|---|---|---|---|---|
| 2026-09-16 | setup | Day 0 — system built, routines armed | – | – | Baseline diagnostic scheduled for D1 (Sep 17) |
| 2026-09-17 | W1 | D1 morning — Drive sync only | 0 | – | Fired 06:10Z, processed 11:08Z (session was idle). Sync clean: all 3 folders match inventory, no new files. Ledger empty on D1 so nothing was due — no quiz owed. |
| 2026-09-17 | W2 | D1 baseline pt 1 — [AUS] IntroML (KNN, overfitting, trees, evaluation) | 7 | 3/7 (43%) | ✅ k trade-off, validation vs test · 🟡 KNN scaling mechanism, Occam's Razor · ❌ cosine/Euclidean, GINI extremes, precision/recall. Seeded 7 ledger items, 5 flags. **Diagnosis: vocabulary is present, mechanisms and directions are not.** Two of the three failures are concepts he annotated CORRECTLY in his own margin notes — fluency decayed, storage strength never formed. |

## Misconception journal (Feynman & mining notes)
- **2026-09-17 — "correlation" standing in for "scale" (FP-1).** Asked why loan amount dominates KNN, answered that age and loan aren't correlated. Correlation between features is not what breaks an unscaled distance metric; raw magnitude is ($-differences in the tens of thousands swamp year-differences in the tens, both squared). Watch for the general pattern: reaching for a statistical-relationship explanation where the cause is arithmetic. Deck 3 p.13–17.
- **2026-09-17 — geometry of cosine (FP-2).** "180 degrees" for dissimilar documents. With non-negative word-count vectors the angle never exceeds 90°; orthogonal (no shared words) is cos = 0 = 90°, and cos = −1 is unreachable. Also missing: *why* Euclidean ties the pairs — it counts mismatched positions and is blind to overlap. Deck 3 p.18.
- **2026-09-17 — the annotation paradox (drives FP-5).** On BOTH GINI and precision/recall his own handwritten margin notes on the Tagged PDFs contain the correct answer ("Maximum GINI when we have the sample more equally distributed across the classes"; "Precision → out of those red, how many"). He wrote it correctly months ago and retrieved it backwards today. This is the teach-skill fluency-vs-storage distinction in its purest form: annotating is recognition, not retrieval. Implication for the sprint: **re-reading slides will not fix these; only repeated retrieval will.** Bias every window further toward cold recall, away from review.

## Format-level weaknesses
| Format | Rolling pass rate | Drill active? |
|---|---|---|
| intuition | 0/2 (🟡, ❌) | ⚠️ yes — weakest format |
| compare | 0/1 (❌) | watch |
| open (why/mechanism) | 1/2 | watch |
| complete the sentence | 1/1 | no |
| interview-style | 0/1 (🟡) | watch |
