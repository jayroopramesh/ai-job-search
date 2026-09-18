# Student Progress — Jayroop

Sprint: **2026-09-17 (D1) → 2026-10-16 (D30)** · 🎤 **[AUS] Sat 10 Oct** · 🎤 **[OXFORD] Fri 16 Oct** · CV long track → 2026-11-15
State file is authoritative (TUTOR.md §4/§8). Updated at the end of every window; committed and pushed each time.

## Scoreboard
- Sessions completed: **5 / 88** sprint windows · missed: **0**
- **Review pass rate (the number that matters): 75%** on D2 — 2 ✅ / 2 🟡 / 0 ❌ of 4 re-attacked flags
- Overall retention incl. cold pre-tests: **39%** (4 ✅ · 7 🟡 · 8 ❌ of 19)
- Ledger items: 14 · due 09-19: **12**
- 🚩 Flag points — open: **9** (6 concept + 3 pattern) · cleared: 0 · **2 now moving (1/3 passes)**
- Mocks: #0 — · #1 — · #2 — · #3 — · AUS oral — · OXFORD oral — · final —

## 🚩 Flag Points (active attack list)
| # | Concept | Course | Aud. | First missed | Angle history (formats tried) | Consec. passes | Status |
|---|---|---|---|---|---|---|---|
| FP-4 | **Precision ↔ recall.** Swapped twice on D1 from unrelated angles → taught the P/R = Prediction/Real anchor rather than re-testing. **D2: first clean pass** — given a more trigger-happy model he reasoned straight from the denominators ("TP increases but so does FP"), which is exactly the taught move. Minor slip: said FN "stays the same" when it actually falls slightly. | IntroML + DL4H | both | 2026-09-17 | intuition, structural, clinical case, forced-choice | **1 / 3** | 🟢 moving |
| FP-3 | **GINI impurity extremes.** Inverted on D1 (put the max at a pure node). **D2: clean pass** — 25/25 is maximum impurity, tree moves toward the pure node. | IntroML | [AUS] | 2026-09-17 | open, forced-choice | **1 / 3** | 🟢 moving |
| FP-7 | **PATTERN: adjacent-concept substitution.** D1: "bias-variance" for Occam's Razor, "MLE" for empirical risk minimisation. **D2: named Occam's Razor correctly** — the substitution behaviour itself is corrected — but supplied no justification when asked, so the drill spec (exact term + one line) is not yet met. | both | both | 2026-09-17 | interview-style, complete-the-sentence, reverse-flashcard | 0 / 3 | 🟠 half-fixed |
| FP-1 | **Why an unscaled attribute dominates KNN.** D1: blamed correlation. D2: answered "scaling" and stopped — the *mechanism* (large-magnitude feature dominates the squared distance) is still not produced, and the question asked for it explicitly. Two attempts, zero mechanisms. | IntroML | [AUS] | 2026-09-17 | intuition, interview-style | 0 / 3 | 🔴 open |
| FP-9 | **PATTERN: stops at the label, omits the mechanism.** New on D2, and the highest-leverage pattern for an *oral* format: Q3 ("scaling") and Q4 ("Occam's Razor") were both correct labels with the requested "why" simply absent. A panel's next word is always "why?" — a label-only answer reads as recognition, not understanding. Drill: every flag re-attack must demand label **and** mechanism; grade 🟡 whenever the mechanism is missing, however right the label. | both | both | 2026-09-18 | — | 0 / 3 | 🔴 open |
| FP-8 | **Attribute-type taxonomy.** Pre-test: 1/4 (zip nominal ✅; star rating called ratio, °C called ordinal, kg called ordinal). "Ordinal" is being used as a catch-all for anything numeric. The deck's discriminator is the four properties — distinctness, order, meaningful differences, meaningful ratios — and whether there is a true zero. | IntroML | [AUS] | 2026-09-18 | pre-test | 0 / 3 | 🔴 open |
| FP-2 | **Cosine vs Euclidean on text** — could not say why Euclidean ties the two document pairs; angle detail wrong (said 180°, orthogonal is 90° / cos = 0). Not yet re-attacked. | IntroML | [AUS] | 2026-09-17 | compare | 0 / 3 | 🔴 open |
| FP-6 | **Losses encode noise models** — total gap: L2 ↔ Gaussian, L1 ↔ Laplace, CE ↔ categorical; and why squaring lets outliers dominate. Core Namburete framing, likely [OXFORD] opener. Not yet re-attacked. | DL4H | [OXFORD] | 2026-09-17 | open | 0 / 3 | 🔴 open |
| FP-5 | **PATTERN: directional inversion.** Four instances on D1 (GINI max↔min, precision↔recall ×2, CE high↔low). **D2 drill: 2/2 — both poles committed correctly and for the right reason.** Best evidence yet that the anchors are landing. Keep 2 items/window until 80% over a rolling week. | both | both | 2026-09-17 | forced-choice ×2 | **1 / 3** | 🟢 moving |

## Ledger (spaced repetition)
Intervals 1→3→7→14→30 days. ✅ advance · 🟡 repeat · ❌ reset to 1d + flag.
| Item (one testable assertion/skill) | Course | Aud. | Interval | Last seen | Next due | Lapses |
|---|---|---|---|---|---|---|
| FP sits in precision's denominator only; FN sits in recall's only — so FP cannot move recall | both | both | 3d ✅ | 2026-09-18 | 2026-09-21 | 2 |
| GINI measures node impurity: max at equal class distribution, min (0) at a pure node | IntroML | [AUS] | 3d ✅ | 2026-09-18 | 2026-09-21 | 1 |
| Unscaled features let the large-magnitude attribute dominate the distance metric (KNN) | IntroML | [AUS] | 1d 🟡 | 2026-09-18 | 2026-09-19 | 2 |
| Occam's Razor: given equal generalization error prefer the simpler model (complex models fit accidentally) | IntroML | [AUS] | 1d 🟡 | 2026-09-18 | 2026-09-19 | 2 |
| Effect of k: too small → noise-sensitive; too large → neighbourhood pulls in other classes | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |
| Validation set estimates generalization error during model building; test set stays untouched | IntroML | [AUS] | 3d ✅ | 2026-09-17 | 2026-09-20 | 0 |
| Euclidean counts mismatched positions and ties unrelated doc pairs; cosine measures angle/overlap | IntroML | [AUS] | 1d ❌ | 2026-09-17 | 2026-09-19 | 1 |
| Training a NN = minimising loss over data = **empirical risk minimisation** (the named principle) | DL4H | [OXFORD] | 1d 🟡 | 2026-09-17 | 2026-09-19 | 1 |
| Every loss is a noise model: L2 ↔ Gaussian, L1 ↔ Laplace, CE ↔ categorical; squaring makes outliers dominate | DL4H | [OXFORD] | 1d ❌ | 2026-09-17 | 2026-09-19 | 1 |
| Overlap losses (Dice) address class imbalance: background pixel count dominates pixel-wise CE | DL4H | [OXFORD] | 1d 🟡 | 2026-09-17 | 2026-09-19 | 1 |
| The two error types are NOT interchangeable — summing FP and FN is accuracy thinking | both | both | 1d 🟡 | 2026-09-17 | 2026-09-19 | 1 |
| Attribute types: the four properties, and true zero as the interval↔ratio discriminator | IntroML | [AUS] | 1d ❌ | 2026-09-18 | 2026-09-19 | 1 |
| Data quality problems: noise/outliers, wrong data, fake data, missing values, duplicates | IntroML | [AUS] | 1d ❌ | 2026-09-18 | 2026-09-19 | 1 |
| DL4H open challenges: bias & fair representation, explainability, privacy/security (GDPR) | DL4H | [OXFORD] | 1d ❌ | 2026-09-18 | 2026-09-19 | 1 |

## Session log
| Date | Window | Type | Items | Score | Notes |
|---|---|---|---|---|---|
| 2026-09-16 | setup | Day 0 — system built, routines armed | – | – | Baseline diagnostic scheduled for D1 (Sep 17) |
| 2026-09-17 | W1 | D1 morning — Drive sync only | 0 | – | Fired 06:10Z, processed 11:08Z (session idle). Sync clean. Ledger empty on D1 so nothing was due. |
| 2026-09-17 | W2 | D1 baseline pt 1 — [AUS] IntroML | 7 | 3/7 (43%) | ✅ k trade-off, validation vs test · 🟡 KNN scaling mechanism, Occam's Razor · ❌ cosine/Euclidean, GINI extremes, precision/recall. **Vocabulary present, mechanisms and directions absent.** Two failures were concepts he annotated CORRECTLY in his own margin notes. |
| 2026-09-17 | W3 | D1 baseline pt 2 — [OXFORD] DL4H + FP-4 re-attack | 5 | 1.5/5 (30%) | 🟡 ERM named as MLE, 🟡 Dice/imbalance · ❌ noise models, ❌ FP-4 again. Recorded oral-interview preference (no arithmetic). Taught the P/R anchor instead of re-testing. Wrote LR-0001. |
| 2026-09-17 | W3 (wake) | Duplicate wake | 0 | – | Closed as duplicate — window already run live. Added TUTOR.md §0 same-day duplicate check. |
| 2026-09-18 | W1 | D2 review — 4 flag re-attacks from fresh angles | 4 | **3/4 (75%)** | ✅ **FP-4 first clean pass** (reasoned from the denominators — the taught anchor held) · ✅ **FP-3 first clean pass** (inversion corrected) · 🟡 FP-1 (said "scaling", no mechanism) · 🟡 FP-7 (named Occam's Razor correctly — substitution fixed — but no justification). **FP-5 drill 2/2.** Answered in the afternoon, which is fine: windows are queues, not deadlines (see NOTES.md). |
| 2026-09-18 | W2 | D2 new material — IntroML 1+2, DL4H L1 · cold pre-test | 3 | 0/3 | ❌ attribute types 1/4 → new FP-8 · ❌ data quality problems · ❌ DL4H challenges ("no idea"). **Pre-test failure is by design — this is the baseline, not a verdict.** Micro-lesson delivered; recall quiz on 09-19. New pattern FP-9 opened from W1's two 🟡s. |

## Misconception journal (Feynman & mining notes)
- **2026-09-17 — "correlation" standing in for "scale" (FP-1).** Correlation between features is not what breaks an unscaled distance metric; raw magnitude is. Deck 3 p.13–17.
- **2026-09-17 — geometry of cosine (FP-2).** With non-negative word-count vectors the angle never exceeds 90°; orthogonal is cos 0, and cos = −1 is unreachable. Deck 3 p.18.
- **2026-09-17 — the annotation paradox (drives FP-5).** His own margin notes on GINI and precision/recall contain the correct answers; he wrote them correctly months ago and retrieved them backwards. Annotating is recognition, not retrieval — re-reading will not fix these, only retrieval will.
- **2026-09-18 — the anchor worked, and the evidence is the *reasoning*, not the answer (FP-4).** Asked which metric moves when the model turns trigger-happy, he did not recall a fact — he walked the denominators: "TP increases but so does FP." That is the taught procedure running under its own power, which is what storage strength looks like. Generalise the tactic: for any two-pole concept, give him a *procedure* to re-derive the direction rather than a fact to remember.
- **2026-09-18 — label without mechanism (FP-9).** Two answers today were the right word and nothing else. In a written exam that scores; in an oral it invites "why?" and the silence afterwards is the whole impression. From now on a bare-label answer is graded 🟡 even when the label is perfect.
- **2026-09-18 — "ordinal" as a catch-all (FP-8).** Star rating → ratio, °C → ordinal, kg → ordinal. The label is being assigned by feel rather than by the deck's four-property test. Note the same annotation paradox again: his margin note on the interval slide reads "I can't say Ali is twice Ahmed cause my ref point is not 0" — he had the true-zero insight in his own handwriting.

## Format-level weaknesses
| Format | Rolling pass rate | Drill active? |
|---|---|---|
| forced-choice direction (FP-5 drill) | **2/2** ✅ | continue — best-performing format |
| name-the-principle (FP-7 drill) | 0/3 (label right on the last one) | ⚠️ yes — now demand the reason too |
| mechanism / "why" follow-ups (FP-9) | 0/2 | ⚠️ yes — highest priority for an oral panel |
| intuition | 0/2 | ⚠️ yes |
| open (why/mechanism) | 1/4 | ⚠️ yes |
| compare | 0/1 | watch |
| complete the sentence | 1/2 | watch |
| Feynman / clinical case | 0/1 | watch |
