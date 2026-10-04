# SYLLABUS — 98-Day Campaign to Three Assessments

> **🎤 HARD DATES** — **[AUS] IntroML: Mon 16 Nov 2026** (D60) · **[OXFORD] DL4H: Fri 20 Nov 2026** (D64) · **[OXFORD] CV: Fri 25 Dec 2026** (D99)
> D1 = 17 Sep 2026. Everything below is built backwards from those three dates.
> This replaces the old 28-day sprint: the dates moved out by ~5 weeks on 2026-09-18, and CV decoupled from the DL4H panel into its own assessment.

**Four windows/day** (see TUTOR.md §2): **W1** 08:00 review · **W2** 12:30 new material · **W3** 17:00 interleaved gauntlet · **W4** 21:00 flag clinic + teach-back. Copenhagen times; queues, not deadlines.

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

The dates below stay for the deadline arithmetic and the fixed events (mocks, T-1 days, the three assessments). They no longer claim to schedule a given deck on a given day.

## Block 2 — Advanced DL + CV overlap · **Sat 17 Oct → Fri 6 Nov** (3 weeks)
Goal: DL4H finished; the eight CV decks that overlap DL4H enter as reinforcement, so CV starts Block 4 already half-warm.

| Week | Dates | [AUS] IntroML | [OXFORD] DL4H | CV overlap injected |
|---|---|---|---|---|
| 5 | Oct 17–23 | 13 Cluster Analysis I · 15 Cluster Analysis III | L9-10 Low-data, transfer learning & domain adaptation | 17 Representation · 18 Unsupervised |
| 6 | Oct 24–30 | *maintenance review only* | L11-12 Generative modelling · L13 Federated learning | 16 Generative · 02 Filtering |
| 7 | Oct 31 – Nov 6 | *maintenance review only* | L14-15 Sequence models · L15-16 Transformers · L16 Explainability | 07 CNNs · 08 Transformers · 09 Visualization · 06 Classification |

Sat 24 Oct **Mock #5** + **PS4 mining** · Sat 31 Oct **Mock #6** · Sun retros throughout.
If IntroML decks 10–12/14 appear in Drive, slot them into week 5–6 W2 and shift clustering right.

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
| Sun 15 | **T-1 AUS:** light confidence pass, anchors only, stop early | |

## 🎤 **Mon 16 Nov — AUS INTERVIEW (D60)**
W1 short warm-up (anchors and one-liners, nothing new, no new flags) · W2 skipped · W3 **debrief** — what was asked, what felt shaky, what surprised you. The debrief reshapes 17–19 Nov.

## Block 4 — Oxford final push · **Tue 17 Nov → Thu 19 Nov**
IntroML drops to maintenance. Three days of DL4H only, steered by the AUS debrief (the panels probe similarly; whatever caught you out on Monday gets hunted here). Thu 19 is **T-1**: light pass, stop early.

## 🎤 **Fri 20 Nov — OXFORD DL4H INTERVIEW (D64)**
W1 warm-up · W3 **debrief** → then the campaign turns entirely to CV.

## Block 5 — Computer Vision · **Sat 21 Nov → Thu 24 Dec** (34 days)
The eight overlap decks (02, 06, 07, 08, 09, 16, 17, 18) are already taught — they enter as review. Twelve genuinely new decks over five weeks, one per ~2.5 days, DL4H and IntroML kept alive by the spaced ladder only.

| Week | Dates | New CV material |
|---|---|---|
| 1 | Nov 21–27 | 01 Introduction · 03 Fourier Transforms · 04 Restoration |
| 2 | Nov 28 – Dec 4 | 05 Matching/Indexing/Search · 10 Object Detection |
| 3 | Dec 5–11 | 11 Segmentation · 12 Videos · 13 Tracking |
| 4 | Dec 12–18 | 14 Camera Models · 15 MVG · 19 Vision-Language |
| 5 | Dec 19–24 | 20 Ethics/Privacy · full-syllabus sweep · **🎤 CV ORAL MOCK Tue 22 Dec** · Thu 24 **T-1 light pass** |

## 🎤 **Fri 25 Dec — CV ASSESSMENT (D99)**
W1 warm-up · W3 debrief + **full campaign retro → final readiness report → wind-down (TUTOR.md §9)**.
⚠️ *25 Dec is Christmas Day — worth double-checking that date.*
