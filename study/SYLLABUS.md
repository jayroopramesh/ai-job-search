# SYLLABUS — 98-Day Campaign to Three Assessments

> **🎤 HARD DATES** — **[AUS] IntroML: Mon 16 Nov 2026** (D61) · **[OXFORD] DL4H: Fri 20 Nov 2026** (D65) · **[OXFORD] CV: Fri 25 Dec 2026** (D100) *(all three corrected 2026-11-12 — they read D60/D64/D99, an off-by-one from differencing the dates instead of counting inclusively from D1 = 17 Sep. The same error set the dashboard progress bar's denominator to 99.)*
> D1 = 17 Sep 2026. Everything below is built backwards from those three dates.
> This replaces the old 28-day sprint: the dates moved out by ~5 weeks on 2026-09-18, and CV decoupled from the DL4H panel into its own assessment.

**THREE windows/day** (see TUTOR.md §2), set by Jayroop on 2026-10-17: **S1** 07:48 review + flag attack · **S2** 12:41 new material · **S3** 19:52 gauntlet + interview drill, which absorbed the retired W4 clinic. 15 min hard cap each. Copenhagen times; queues, not deadlines. *(Corrected 2026-11-12: this line still described **four** windows at 08:00/12:30/17:00/21:00 — stale for 26 days, on the file that is the schedule.)*

**What the extra time buys.** The old plan force-fed two decks a day and capped the spaced-repetition ladder at 28 days. Now: one deck taught properly per day, the full **1→3→7→14→30** ladder actually runs to term, every problem sheet gets mined (for questions — see RESOURCES.md; they are solutions guides, not his attempts), and there is room for four mocks per course instead of a scramble. Depth, not more speed.

---

## Block 1 — Foundations · **Sat 19 Sep → Fri 16 Oct** (4 weeks)
Goal: the whole [AUS] syllabus taught once, and DL4H through regularisation. Pace: one primary deck per day, second course as interleaved review.

| Week | Dates | [AUS] IntroML | [OXFORD] DL4H | Weekend |
|---|---|---|---|---|
| 1 | Sep 19–25 | 1 Introduction ✅ · 2 Data ✅ · ~~3 KNN~~ → wk 2 | L1 Why DL for healthcare ✅ · ~~L2~~ → wk 2 | Mock #1 deferred, available on demand |
| 2 | Sep 21–27 | **3 KNN taught ✅** (lazy learning, dimensionality, regression) · ~~4 Decision Trees~~ · ~~5 Overfitting~~ → wk 3 | ~~L2 carried~~ partly (losses, ERM re-tested) · ~~L3~~ · ~~L4~~ → wk 3 | ~~Mock #2~~ **deferred** · PS1 mined ✅ (as a question source — see RESOURCES) |
| 3 | Sep 28 – Oct 4 | **4 Decision Trees (carried)** · **5 Overfitting (carried)** | **L3 Backprop (carried)** · **L4 Init & normalisation (carried)** | Sat: **short Mock #1** (10 items, ~8 min — see TUTOR §2) · Sun: retro |
| 4 | Oct 5–11 | 6 Class Imbalance & Evaluation · 7 Naïve Bayes | L5 CNNs · L6 Advanced CNNs | Sat: **Mock #2** + PS2 mining · Sun: retro |
| 5 | Oct 12–18 | 8 Regression I · 9 Regression II | L7-8 Regularisation (both parts) | Sat: **Mock #3** + PS3 mining · Sun: retro |

⚠️ **The week grid above is now REFERENCE, not schedule — changed at the 2026-10-04 retro.**

It slipped once on 09-27 (Week 2 delivered one deck of six) and again on 10-04 (Week 3 delivered **none** of its four carried topics). Two slips in a row prove the model is wrong, not merely behind. A calendar assumes the constraint is how fast material can be taught; it never was. The constraint is **engaged days**, running at **3 in 18**. With 43 days to [AUS] that projects to roughly **seven more engaged days** against a grid wanting ~30 teaching days for IntroML alone — a gap no amount of slipping closes, and "slipped one week" written every Sunday is bookkeeping fiction.

**What replaces it: a priority-ordered queue, served from the top whenever he engages, regardless of the date.** Ordered by nearest deadline first, then by whether an open flag lives in that deck.

| # | Deck | Aud. | Why here |
|---|---|---|---|
| 1 | **4 Decision Trees** | [AUS] | FP-3 (GINI extremes) lives here, at 1/3. Carried twice. |
| 2 | **5 Overfitting** | [AUS] | Carried twice; core oral material. |
| 3 | **L3 Backprop** | [OXFORD] | Carried twice. |
| 4 | **L4 Init & normalisation** | [OXFORD] | Carried twice; adjacent to FP-5/FP-6. |
| 5 | **6 Class Imbalance & Evaluation** | [AUS] | FP-4 (precision ↔ recall) lives here. |
| 6+ | 7 Naïve Bayes · 8–9 Regression · L5–L6 CNNs · L7–8 Regularisation · 13/15 Clustering | both | Deadline order thereafter. |

⚠️ **Weighting changed 2026-10-17, by Jayroop: ~60% [AUS] IntroML / ~40% [OXFORD] DL4H, and CV is PAUSED until 20 Nov.** The queue above already runs 3 AUS to 2 OXFORD, so its order stands — what changes is that **no CV deck is served before 20 Nov**, and when the queue is ambiguous, AUS wins. Rationale, his: the CV interview is 25 Dec, five weeks behind the other two, and spending any of the next 30 days on it costs the two that are close. Resume CV on 20 Nov with the DL4H slot, which frees up the same day.

**On the 25 Dec date:** that is Christmas Day. Flagged once as a possible typo, never confirmed, still unconfirmed. ⚠️ **The escape clause in this line is about to expire — caught 2026-11-12.** It read *"it does not affect anything until 20 Nov, so it is not worth a question now"*, which was true when written and is **8 days from false**: 20 Nov is when CV work starts, and `question-banks/cv.md` is empty, so that date is already carrying load. **Exactly the same shape as the 11-08 finding on which course sits on the 16th** — a mitigating statement, true at the time, never re-read as its own trigger approached. **Queued to go out with the next email rather than burning one today**, alongside the still-open question about the 16th.

The dates below stay for the deadline arithmetic and the fixed events (mocks, T-1 days, the three assessments). They no longer claim to schedule a given deck on a given day.

## Block 2 — Advanced DL + CV overlap · **Sat 17 Oct → Fri 6 Nov** (3 weeks)
Goal: DL4H finished; the eight CV decks that overlap DL4H enter as reinforcement, so CV starts Block 4 already half-warm.

| Week | Dates | [AUS] IntroML | [OXFORD] DL4H | CV overlap injected |
|---|---|---|---|---|
| 5 | Oct 17–23 | 13 Cluster Analysis I · 15 Cluster Analysis III | L9-10 Low-data, transfer learning & domain adaptation | 17 Representation · 18 Unsupervised |
| 6 | Oct 24–30 | *maintenance review only* | L11-12 Generative modelling · L13 Federated learning | 16 Generative · 02 Filtering |
| 7 | Oct 31 – Nov 6 | *maintenance review only* | L14-15 Sequence models · L15-16 Transformers · L16 Explainability | 07 CNNs · 08 Transformers · 09 Visualization · 06 Classification |

Sat 24 Oct **Mock #5** + **PS4 mining** · Sat 31 Oct **Mock #6** · Sun retros throughout.
If IntroML decks 10–12/14 appear in Drive, serve them at the next **S2** and shift clustering right. *(Was "week 5–6 W2" — both the week numbers and the window name are from retired schemes.)*

## Block 3 — Consolidation & mocks · **Sat 7 Nov → Sun 15 Nov** (9 days)
No new material. Everything now points at the two interviews.

| Day | Date | Focus |
|---|---|---|
| Sat 7 | full [AUS] syllabus sweep — every deck, cold | |
| Sun 8 | full [OXFORD] DL4H sweep — every lecture, cold | |
| Mon 9 | flag clinic: every open flag, all four windows | |
| Tue 10 | weakest-quartile re-teach, both courses | |
| Wed 11 | **🎤 AUS ORAL MOCK** — full panel simulation, follow-up chains | |
| Thu 12 | AUS re-attack on everything the mock exposed — **all [AUS] flags close today** | |
| Fri 13 | **🎤 OXFORD ORAL MOCK** — Namburete framing, clinical-deployment pressure | |
| Sat 14 | Oxford re-attack — **all [OXFORD] DL4H flags close today** | |
| Sun 15 | **T-1 AUS:** light confidence pass, **`study/ANCHORS.md`** only, stop early | |

## 🎤 **Mon 16 Nov — AUS INTERVIEW (D61)**
**S1** short warm-up (read from `ANCHORS.md`, nothing new, no new flags) · **S2** skipped · **S3** **debrief** — what was asked, what felt shaky, what surprised you. The debrief reshapes 17–19 Nov.

## Block 4 — Oxford final push · **Tue 17 Nov → Thu 19 Nov**
IntroML drops to maintenance. Three days of DL4H only, steered by the AUS debrief (the panels probe similarly; whatever caught you out on Monday gets hunted here). Thu 19 is **T-1**: light pass, stop early.

## 🎤 **Fri 20 Nov — OXFORD DL4H INTERVIEW (D65)**
**S1** warm-up (`ANCHORS-DL4H.md`) · **S2** skipped · **S3** **debrief** → then the campaign turns entirely to CV.

## Block 5 — Computer Vision · **Sat 21 Nov → Thu 24 Dec** (34 days)
The eight overlap decks (02, 06, 07, 08, 09, 16, 17, 18) are already taught — they enter as review. Twelve genuinely new decks over five weeks, one per ~2.5 days, DL4H and IntroML kept alive by the spaced ladder only.

| Week | Dates | New CV material |
|---|---|---|
| 1 | Nov 21–27 | 01 Introduction · 03 Fourier Transforms · 04 Restoration |
| 2 | Nov 28 – Dec 4 | 05 Matching/Indexing/Search · 10 Object Detection |
| 3 | Dec 5–11 | 11 Segmentation · 12 Videos · 13 Tracking |
| 4 | Dec 12–18 | 14 Camera Models · 15 MVG · 19 Vision-Language |
| 5 | Dec 19–24 | 20 Ethics/Privacy · full-syllabus sweep · **🎤 CV ORAL MOCK Tue 22 Dec** · Thu 24 **T-1 light pass** |

## 🎤 **Fri 25 Dec — CV ASSESSMENT (D100)**
**S1** warm-up · **S2** skipped · **S3** debrief + **full campaign retro → final readiness report → wind-down (TUTOR.md §9)**.
⚠️ *25 Dec is Christmas Day — worth double-checking that date.*
