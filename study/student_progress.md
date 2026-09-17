# Student Progress — Jayroop

Sprint: **2026-09-17 (D1) → 2026-10-16 (D30)** · 🎤 **[AUS] Sat 10 Oct** · 🎤 **[OXFORD] Fri 16 Oct** · CV long track → 2026-11-15
State file is authoritative (TUTOR.md §4/§8). Updated at the end of every window; committed and pushed each time.

## Scoreboard
- Sessions completed: **3 / 88** sprint windows (3/day × 30, less the 2 skipped midday windows on interview days) · missed: 0
- Retention (7-day rolling pass rate): **38%** (2 ✅ · 5 🟡 · 5 ❌ of 12, full D1 baseline + close-out)
- Ledger items: 11 · due tomorrow (D2, 09-18): **9**
- 🚩 Flag points — open: **7** (5 concept + 2 pattern) · cleared: 0
- Mocks: #0 — · #1 — · #2 — · #3 — · AUS oral — · OXFORD oral — · final —

## 🚩 Flag Points (active attack list)
| # | Concept | Course | Aud. | First missed | Angle history (formats tried) | Consec. passes | Status |
|---|---|---|---|---|---|---|---|
| FP-1 | **Why an unscaled attribute dominates KNN** — answered "age and loan aren't correlated"; the real cause is *magnitude/scale*, not correlation. Right answer, wrong mechanism. | IntroML | [AUS] | 2026-09-17 | intuition | 0 / 3 | 🔴 open |
| FP-2 | **Cosine vs Euclidean on text** — could not say why Euclidean ties the two document pairs; angle detail wrong (said 180°, orthogonal is 90° / cos = 0). | IntroML | [AUS] | 2026-09-17 | compare | 0 / 3 | 🔴 open |
| FP-3 | **GINI impurity extremes inverted** — said GINI is maximal at a 0/100 split; that is the *minimum* (pure node). Max is at equal class distribution. Also conflated GINI with entropy. | IntroML | [AUS] | 2026-09-17 | open | 0 / 3 | 🔴 open |
| FP-4 | **🔥 CRITICAL — precision and recall swapped.** Missed TWICE on D1 from two unrelated angles: fish analogy (said high precision = big mixed catch) and Dice/segmentation (said false positives hurt recall; they hurt precision — FP does not appear in recall's denominator at all). Encoding is wrong, not just weakly stored → taught the P/R = Prediction/Real anchor on D1 W3; retrieval practice resumes D2. **D1 close-out showed the anchor beginning to bite**: he classified 460 FP / 5 FN correctly for the first time, then failed to draw the conclusion and summed the two error types instead. | IntroML + DL4H | both | 2026-09-17 | intuition, structural, clinical case | 0 / 3 | 🟠 moving |
| FP-6 | **Losses encode noise models** — total gap ("no idea"): L2 ↔ Gaussian, L1 ↔ Laplace, cross-entropy ↔ categorical uncertainty; and why squaring lets outliers dominate. Core Namburete framing, likely [OXFORD] opener. | DL4H | [OXFORD] | 2026-09-17 | open | 0 / 3 | 🔴 open |
| FP-7 | **PATTERN: adjacent-concept substitution.** Asked to *name* a principle, reaches for a neighbouring famous name instead of the precise one — "bias-variance trade-off" for Occam's Razor, "maximum likelihood estimation" for empirical risk minimisation. 0/2 on name-the-principle items. Drill: name-the-principle item every window; require the exact term plus one line of justification. | both | both | 2026-09-17 | interview-style, complete-the-sentence | 0 / 3 | 🔴 open |
| FP-5 | **PATTERN: directional inversion.** When a concept has two poles, the wrong pole gets picked (GINI max↔min, precision↔recall twice, cross-entropy high↔low on matching pixels). Four instances on D1 — the dominant failure mode of this student. Drill: 2 "which pole, and what does the other pole look like?" items per window until 80% over a rolling week. | both | both | 2026-09-17 | — | 0 / 3 | 🔴 open |

## Ledger (spaced repetition)
Intervals 1→3→7→14→30 days. ✅ advance · 🟡 repeat · ❌ reset to 1d + flag.
| Item (one testable assertion/skill) | Course | Aud. | Interval | Last seen | Next due | Lapses |
|---|---|---|---|---|---|---|
| Unscaled features let the large-magnitude attribute dominate the distance metric (KNN) | IntroML | [AUS] | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |
| Effect of k: too small → noise-sensitive; too large → neighbourhood pulls in other classes | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |
| Euclidean counts mismatched positions and ties unrelated doc pairs; cosine measures angle/overlap | IntroML | [AUS] | 1d ❌ | 2026-09-17 | 2026-09-18 | 1 |
| Validation set estimates generalization error during model building; test set stays untouched | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |
| GINI measures node impurity: max at equal class distribution, min (0) at a pure node | IntroML | [AUS] | 1d ❌ | 2026-09-17 | 2026-09-18 | 1 |
| Occam's Razor: given equal generalization error prefer the simpler model (complex models fit accidentally) | IntroML | [AUS] | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |
| Training a NN = minimising loss over data = **empirical risk minimisation** (the named principle) | DL4H | [OXFORD] | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |
| Every loss is a noise model: L2 ↔ Gaussian, L1 ↔ Laplace, CE ↔ categorical; squaring makes outliers dominate | DL4H | [OXFORD] | 1d ❌ | 2026-09-17 | 2026-09-18 | 1 |
| FP sits in precision's denominator only; FN sits in recall's only — so FP cannot move recall | both | both | 1d ❌ | 2026-09-17 | 2026-09-18 | **2** |
| Overlap losses (Dice) address class imbalance: background pixel count dominates pixel-wise CE | DL4H | [OXFORD] | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |
| The two error types are NOT interchangeable — summing FP and FN is accuracy thinking, which is what P/R exist to prevent | both | both | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |

## Session log
| Date | Window | Type | Items | Score | Notes |
|---|---|---|---|---|---|
| 2026-09-16 | setup | Day 0 — system built, routines armed | – | – | Baseline diagnostic scheduled for D1 (Sep 17) |
| 2026-09-17 | W1 | D1 morning — Drive sync only | 0 | – | Fired 06:10Z, processed 11:08Z (session was idle). Sync clean: all 3 folders match inventory, no new files. Ledger empty on D1 so nothing was due — no quiz owed. |
| 2026-09-17 | W2 | D1 baseline pt 1 — [AUS] IntroML (KNN, overfitting, trees, evaluation) | 7 | 3/7 (43%) | ✅ k trade-off, validation vs test · 🟡 KNN scaling mechanism, Occam's Razor · ❌ cosine/Euclidean, GINI extremes, precision/recall. Seeded 7 ledger items, 5 flags. **Diagnosis: vocabulary is present, mechanisms and directions are not.** Two of the three failures are concepts he annotated CORRECTLY in his own margin notes — fluency decayed, storage strength never formed. |
| 2026-09-17 | W3 | D1 baseline pt 2 — [OXFORD] DL4H (L2 losses/metrics) + FP-4 re-attack | 5 | 1.5/5 (30%) | 🟡 ERM named as MLE, 🟡 Dice/imbalance (core insight right, CE high↔low inverted) · ❌ noise models (no idea), ❌ **FP-4 missed again** from the structural angle. Recorded oral-interview format preference: no arithmetic questions — TUTOR.md §3 updated. Taught the P/R anchor rather than only re-testing. Close-out (rare-disease screening case) 🟡: error types finally classified correctly, conclusion not drawn — called 460 FP and 5 FN "about the same". Wrote LR-0001. |
| 2026-09-17 | W3 (wake) | Duplicate — scheduled 18:01Z wake arrived after the window had already been run live earlier in the evening | 0 | – | Closed as duplicate, no re-quiz (re-asking the same items hours apart would test fluency, not storage). Exposed a protocol gap → TUTOR.md §0 now requires a same-day duplicate check. |

## Misconception journal (Feynman & mining notes)
- **2026-09-17 — "correlation" standing in for "scale" (FP-1).** Asked why loan amount dominates KNN, answered that age and loan aren't correlated. Correlation between features is not what breaks an unscaled distance metric; raw magnitude is ($-differences in the tens of thousands swamp year-differences in the tens, both squared). Watch for the general pattern: reaching for a statistical-relationship explanation where the cause is arithmetic. Deck 3 p.13–17.
- **2026-09-17 — geometry of cosine (FP-2).** "180 degrees" for dissimilar documents. With non-negative word-count vectors the angle never exceeds 90°; orthogonal (no shared words) is cos = 0 = 90°, and cos = −1 is unreachable. Also missing: *why* Euclidean ties the pairs — it counts mismatched positions and is blind to overlap. Deck 3 p.18.
- **2026-09-17 — the annotation paradox (drives FP-5).** On BOTH GINI and precision/recall his own handwritten margin notes on the Tagged PDFs contain the correct answer ("Maximum GINI when we have the sample more equally distributed across the classes"; "Precision → out of those red, how many"). He wrote it correctly months ago and retrieved it backwards today. This is the teach-skill fluency-vs-storage distinction in its purest form: annotating is recognition, not retrieval. Implication for the sprint: **re-reading slides will not fix these; only repeated retrieval will.** Bias every window further toward cold recall, away from review.

- **2026-09-17 — FP-4 survived a second, unrelated angle.** The fish analogy and the Dice/TP-FP-FN route both produced the same swap, which rules out "bad analogy" and means the *encoding* is reversed rather than weakly stored. Two more retrievals would just have re-practised the error, so W3 switched from testing to teaching: **P → Prediction set** (of what I predicted positive, how much was right — FP hurts it), **R → Real set** (of what is actually positive, how much I found — FN hurts it). Structural rule to lean on in an oral: read the denominator, and whichever error term is missing from it cannot move that metric. Re-test from cold on D2.

- **2026-09-17 — summing error types (close-out).** Given 460 false positives against 5 false negatives he judged the two "about the same", i.e. added them into a single error count. That is accuracy thinking, and separating precision from recall exists precisely to stop it: the two error types carry different costs and are not exchangeable. The asymmetry *is* the diagnosis — 460 vs 5 means recall is fine (89%) and precision has collapsed (8%). Teach next: why screening deliberately buys recall with precision, then confirms downstream. Ties to DL4H's clinical-deployment framing.

## Format-level weaknesses
| Format | Rolling pass rate | Drill active? |
|---|---|---|
| name-the-principle (interview-style / complete-the-sentence) | 0/2 🟡🟡 | ⚠️ yes — FP-7 drill |
| intuition | 0/2 (🟡, ❌) | ⚠️ yes — weakest format |
| open (why/mechanism) | 1/4 | ⚠️ yes |
| compare | 0/1 (❌) | watch |
| structural / formula-reading | 0/1 (❌) | watch — no arithmetic per preference |
| complete the sentence | 1/2 | watch |
| Feynman / clinical case | 0/1 (🟡) | watch |
