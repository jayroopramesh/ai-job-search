# Student Progress — Jayroop

Campaign: **2026-09-17 (D1) → 2026-12-25 (D99)** · 🎤 **[AUS] IntroML Mon 16 Nov** · 🎤 **[OXFORD] DL4H Fri 20 Nov** · 🎤 **[OXFORD] CV Fri 25 Dec**
*Rescoped 2026-09-18: dates moved out ~5 weeks, CV decoupled into its own assessment, 4th daily window added.*
State file is authoritative (TUTOR.md §4/§8). Updated at the end of every window; committed and pushed each time.

## Scoreboard
- Windows completed: **6** · missed: **0** · cadence now **4/day** (~385 windows across the campaign)
- **Review pass rate: 75%** (W1) then **50%** (W4 clinic) — D2 overall **2 ✅ / 7 🟡 / 0 ❌ of 9 re-attacked items**. Zero fails all day: every answer contained correct content.
- Overall retention incl. cold pre-tests: **40%** (4 ✅ · 12 🟡 · 8 ❌ of 24)
- Ledger items: 14 · due 09-19: **12** · ladder now uncapped (98 days means 30-day spacing genuinely runs to term)
- 🚩 Flag points — open: **9** (6 concept + 3 pattern) · cleared: 0 · **4 now moving** · **FP-9 fired on 5 of 5 clinic items — the dominant flag**
- Mocks: #0 — · #1 — · #2 — · #3 — · AUS oral — · OXFORD oral — · final —

## 🚩 Flag Points (active attack list)
| # | Concept | Course | Aud. | First missed | Angle history (formats tried) | Consec. passes | Status |
|---|---|---|---|---|---|---|---|
| FP-4 | **Precision ↔ recall.** Swapped twice on D1 from unrelated angles → taught the P/R = Prediction/Real anchor rather than re-testing. **D2: first clean pass** — given a more trigger-happy model he reasoned straight from the denominators ("TP increases but so does FP"), which is exactly the taught move. Minor slip: said FN "stays the same" when it actually falls slightly. | IntroML + DL4H | both | 2026-09-17 | intuition, structural, clinical case, forced-choice | **1 / 3** | 🟢 moving |
| FP-3 | **GINI impurity extremes.** Inverted on D1 (put the max at a pure node). **D2: clean pass** — 25/25 is maximum impurity, tree moves toward the pure node. | IntroML | [AUS] | 2026-09-17 | open, forced-choice | **1 / 3** | 🟢 moving |
| FP-7 | **PATTERN: adjacent-concept substitution — measured on its own terms now, and passing.** The flag's definition is "reaches for a neighbouring famous name instead of the precise one". That behaviour has not recurred: Occam's Razor named correctly (W1), and **empirical risk minimisation named correctly in the clinic — the exact item he answered "MLE" to on D1.** The missing justifications were being double-counted here and under FP-9; that muddied both signals, so from 2026-09-18 a missing mechanism scores against FP-9 only. | both | both | 2026-09-17 | interview-style, complete-the-sentence, reverse-flashcard ×2 | **1 / 3** | 🟢 moving |
| FP-1 | **Why an unscaled attribute dominates KNN.** Three attempts, no mechanism yet. D1: blamed correlation. D2 W1: said "scaling" and stopped. D2 clinic: handed the label outright and asked only for the mechanism — he correctly described what min-max scaling and standardisation *do* (and that ranges become comparable), but never reached the squaring of raw differences or the domination of the sum. **He answers with the remedy, not the failure.** Also a small slip: min-max normalises per *column*, not per row. Next attempt must be symbolic — read the distance formula term by term. | IntroML | [AUS] | 2026-09-17 | intuition, interview-style, mechanism-only | 0 / 3 | 🔴 open |
| FP-9 | **🔥 PATTERN: stops at the label, omits the mechanism — now the dominant flag.** Fired on **5 of 5** items in the D2 clinic, every one a 🟡 for exactly this reason. Refined diagnosis from Q5: when pressed for a mechanism he describes **the remedy rather than the failure** — asked what goes wrong inside the distance computation, he explained what min-max scaling and standardisation *do*. He reaches for the fix because the fix is procedural and memorable; the failure mode requires reading the formula. **This is why he asked "explain the formula for me also" — and that request is the way in.** Every open flag now needs its mechanism taught *symbolically*, then re-tested by asking him to read the formula aloud, not recite prose. | both | both | 2026-09-18 | mechanism-only prompt (×5) | 0 / 3 | 🔴 open |
| FP-8 | **Attribute-type taxonomy — big move, one error left.** Clinic: sorted all three means correctly (zip meaningless, pain dubious, weight fine) and volunteered that **mode** is the right statistic for zip, which is beyond what was asked. Labels: zip nominal ✅, pain ordinal ✅, **weight called "interval (no absolute zero)" ❌** — weight in kg plainly has a true zero and is ratio. So he now *has* the true-zero rule and misapplies it; on D1 he had no rule at all. Next attempt: hand him the rule and make him apply it to a fresh set. | IntroML | [AUS] | 2026-09-18 | pre-test, applied-means | 0 / 3 | 🟠 moving |
| FP-2 | **Cosine vs Euclidean on text.** Clinic: got the *direction* right unprompted (cosine calls a 2-page and a 20-page report on the same patient similar; Euclidean calls them far apart) then said "I don't know" for the property and **asked to be shown the formula** — the most useful thing he has said all campaign. Magnitude-invariance taught symbolically on D2. | IntroML | [AUS] | 2026-09-17 | compare, applied intuition | 0 / 3 | 🟠 moving |
| FP-6 | **Losses encode noise models.** From "no idea" on D1 to **L2 + Gaussian correct** in the clinic, with the forced-choice direction right (L2 is the one that contorts to chase outliers). Missing: the L1 ↔ Laplace half, and why thin Gaussian tails cause the contortion. Half the pairing table is now in place. | DL4H | [OXFORD] | 2026-09-17 | open, forced-choice | 0 / 3 | 🟠 moving |
| FP-5 | **PATTERN: directional inversion.** Four instances on D1 (GINI max↔min, precision↔recall ×2, CE high↔low). **D2: 4/4 across both windows** — precision/recall, GINI, L1-vs-L2, and the three-way mean sort, all committed correctly. The inversion habit has not recurred since the anchors were taught. Keep 2 items/window until 80% over a rolling week. | both | both | 2026-09-17 | forced-choice ×4 | **2 / 3** | 🟢 moving |

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
| 2026-09-18 | W4 | D2 flag clinic — first run of the new window; 5 flags re-attacked from unused angles | 5 | 2.5/5 (50%) | **Zero fails, five 🟡s, all for the same reason — FP-9 fired on 5/5.** ✅-grade content inside every answer: cosine/Euclidean direction right, L2+Gaussian right, all three means sorted right (+ volunteered mode for nominal), **ERM named correctly — the exact item he answered "MLE" to on D1**, both scaling methods described accurately. What was absent every time: the mechanism. Q5 refined the diagnosis — handed the label and asked only for the mechanism, he described **the remedy, not the failure**. He asked to be shown the formula, which reframes the whole teaching approach (see NOTES). FP-7 de-coupled from FP-9 to stop double-counting. FP-5 now 4/4 on the day. |
| 2026-09-18 | W2 | D2 new material — IntroML 1+2, DL4H L1 · cold pre-test | 3 | 0/3 | ❌ attribute types 1/4 → new FP-8 · ❌ data quality problems · ❌ DL4H challenges ("no idea"). **Pre-test failure is by design — this is the baseline, not a verdict.** Micro-lesson delivered; recall quiz on 09-19. New pattern FP-9 opened from W1's two 🟡s. |

## Misconception journal (Feynman & mining notes)
- **2026-09-17 — "correlation" standing in for "scale" (FP-1).** Correlation between features is not what breaks an unscaled distance metric; raw magnitude is. Deck 3 p.13–17.
- **2026-09-17 — geometry of cosine (FP-2).** With non-negative word-count vectors the angle never exceeds 90°; orthogonal is cos 0, and cos = −1 is unreachable. Deck 3 p.18.
- **2026-09-17 — the annotation paradox (drives FP-5).** His own margin notes on GINI and precision/recall contain the correct answers; he wrote them correctly months ago and retrieved them backwards. Annotating is recognition, not retrieval — re-reading will not fix these, only retrieval will.
- **2026-09-18 — the anchor worked, and the evidence is the *reasoning*, not the answer (FP-4).** Asked which metric moves when the model turns trigger-happy, he did not recall a fact — he walked the denominators: "TP increases but so does FP." That is the taught procedure running under its own power, which is what storage strength looks like. Generalise the tactic: for any two-pole concept, give him a *procedure* to re-derive the direction rather than a fact to remember.
- **2026-09-18 — label without mechanism (FP-9).** Two answers today were the right word and nothing else. In a written exam that scores; in an oral it invites "why?" and the silence afterwards is the whole impression. From now on a bare-label answer is graded 🟡 even when the label is perfect.
- **2026-09-18 — "ordinal" as a catch-all (FP-8).** Star rating → ratio, °C → ordinal, kg → ordinal. The label is being assigned by feel rather than by the deck's four-property test. Note the same annotation paradox again: his margin note on the interval slide reads "I can't say Ali is twice Ahmed cause my ref point is not 0" — he had the true-zero insight in his own handwriting.

- **2026-09-18 — "explain the formula for me also" (the most useful thing he has said).** Asked why cosine and Euclidean disagree, he produced the right direction, then asked to be shown the formula. Read together with Q5 — where, pressed for a mechanism, he described the *fix* rather than the *failure* — the picture is clear: **prose mechanisms are not landing, and he knows it.** He reaches for procedures because procedures are memorable; the failure mode lives in the formula and he has not been shown it symbolically. The no-arithmetic rule was read as no-formulas, which is not what it meant. Correction to the approach: **teach every mechanism symbolically** — write the expression, name each term, point at the term that does the damage — then test by asking him to *read a formula aloud and say which term dominates*. No computing; reading. This is the single biggest change to how this student should be taught.

## Format-level weaknesses
| Format | Rolling pass rate | Drill active? |
|---|---|---|
| forced-choice direction (FP-5 drill) | **4/4** ✅ | continue — clearly his best format |
| name-the-principle (FP-7 drill) | 2/2 on naming | ✅ working — the reason now scores under FP-9 |
| mechanism / "why" follow-ups (FP-9) | **0/7** | 🔥 top priority — switch to symbolic teaching |
| intuition | 0/2 | ⚠️ yes |
| open (why/mechanism) | 1/4 | ⚠️ yes |
| compare | 0/1 | watch |
| complete the sentence | 1/2 | watch |
| Feynman / clinical case | 0/1 | watch |
