# Student Progress — Jayroop

Sprint: **2026-09-17 → 2026-10-14** (DL4H [OXFORD] + IntroML [AUS]) · CV long track [OXFORD] → 2026-11-15
State file is authoritative (TUTOR.md §4/§8). Updated at the end of every window; committed and pushed each time.

## Scoreboard
- Sessions completed: **2 / 84** sprint windows (3/day × 28) · missed: 0
- Retention (7-day rolling pass rate): **63%** (2 ✅ · 1 🟡 · 1 ❌ of 4, D1 baseline pt 1)
- Ledger items: 4 · due tomorrow (D2): 2
- 🚩 Flag points — open: **2** · cleared: 0
- Mocks: #0 — · #1 — · #2 — · #3 — · AUS oral — · OXFORD oral — · final —

## 🚩 Flag Points (active attack list)
| # | Concept | Course | Aud. | First missed | Angle history (formats tried) | Consec. passes | Status |
|---|---|---|---|---|---|---|---|
| FP-1 | **Why an unscaled attribute dominates KNN** — answered "age and loan aren't correlated"; the real cause is *magnitude/scale*, not correlation. Right answer, wrong mechanism — dies on an interview follow-up. | IntroML | [AUS] | 2026-09-17 | intuition | 0 / 3 | 🔴 open |
| FP-2 | **Cosine vs Euclidean on text** — could not say why Euclidean ties the two document pairs; angle detail wrong (said 180°, orthogonal is 90° / cos = 0). | IntroML | [AUS] | 2026-09-17 | compare | 0 / 3 | 🔴 open |

## Ledger (spaced repetition)
Intervals 1→3→7→14→30 days. ✅ advance · 🟡 repeat · ❌ reset to 1d + flag.
| Item (one testable assertion/skill) | Course | Aud. | Interval | Last seen | Next due | Lapses |
|---|---|---|---|---|---|---|
| Unscaled features let the large-magnitude attribute dominate the distance metric (KNN) | IntroML | [AUS] | 1d 🟡 | 2026-09-17 | 2026-09-18 | 1 |
| Effect of k: too small → noise-sensitive; too large → neighbourhood pulls in other classes | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |
| Euclidean counts mismatched positions and ties unrelated doc pairs; cosine measures angle/overlap | IntroML | [AUS] | 1d ❌ | 2026-09-17 | 2026-09-18 | 1 |
| Validation set estimates generalization error during model building; test set stays untouched | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |

## Session log
| Date | Window | Type | Items | Score | Notes |
|---|---|---|---|---|---|
| 2026-09-16 | setup | Day 0 — system built, routines armed | – | – | Baseline diagnostic scheduled for D1 (Sep 17) |
| 2026-09-17 | W1 | D1 morning — Drive sync only | 0 | – | Fired 06:10Z, processed 11:08Z (session was idle). Sync clean: all 3 folders match inventory, no new files. Ledger empty on D1 so nothing was due — no quiz owed. |
| 2026-09-17 | W2 | D1 baseline pt 1 — [AUS] IntroML (KNN, overfitting/model selection) | 4 | 2.5/4 (63%) | ✅ k trade-off, ✅ validation vs test · 🟡 KNN scaling (right answer, wrong mechanism) · ❌ cosine vs Euclidean. Seeded 4 ledger items, 2 flags. Strong on *what*, shaky on *why* — the interview-relevant half. |

## Misconception journal (Feynman & mining notes)
- **2026-09-17 — "correlation" standing in for "scale" (FP-1).** Asked why loan amount dominates KNN, answered that age and loan aren't correlated. Correlation between features is not what breaks an unscaled distance metric; the raw magnitude of the differences is ($-differences in the tens of thousands swamp year-differences in the tens, since both are squared). Watch for this pattern generally: reaching for a statistical-relationship explanation where the real cause is arithmetic/scale. Deck 3 p.13–17.
- **2026-09-17 — geometry of cosine (FP-2).** "180 degrees" for dissimilar documents. With non-negative word-count vectors the angle can never exceed 90°; orthogonal (no shared words) is cos = 0 = 90°, and cos = −1 (180°) is unreachable. Also missing: *why* Euclidean returns the same value for both pairs — it counts the number of mismatched positions and is blind to how much the documents overlap. Deck 3 p.18.

## Format-level weaknesses
| Format | Rolling pass rate | Drill active? |
|---|---|---|
| intuition | 0/1 (🟡) | watch |
| compare | 0/1 (❌) | watch |
| complete the sentence | 1/1 | no |
| open | 1/1 | no |
