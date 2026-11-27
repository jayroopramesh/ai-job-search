# SCHEDULE — the single source of truth for what is due when

**Why this file exists.** Nine times this month a correction landed in some artefacts and not its siblings, because the same instruction existed as three copies inside three trigger prompts. *"Store the pointer, not the value"* was written for **numbers**; this file extends it to **dates and decisions**. The prompts now point here. **Edit this file, not the prompts.**

**And the ordering lesson that produced it:** on 25 Nov the delivery-timing decision was written into `TUTOR.md`, `student_progress.md` and the dashboard — and *not* into the three prompts, which is where it would have acted. **The trigger prompt is the only artefact that starts a window's reasoning. A fix that reaches the documentation and not the prompt has reached the places where it matters least.**

---

## Dates

| What | When | Status |
|---|---|---|
| D1 — campaign start | **2026-09-17** | given |
| [AUS] IntroML assessment | **Mon 16 Nov** | **done · no debrief ever received** |
| [OXFORD] DL4H assessment | **Fri 20 Nov** | **done · no debrief ever received** |
| **[OXFORD] CV assessment** | **Fri 25 Dec** | **given in September · UNCONFIRMED — it is Christmas Day. Asked 16 and 20 Nov, no reply.** |

Day numbers are computed against D1, never stored. **The 25 Dec date is the one load-bearing unconfirmed fact in the campaign**: the mock date, the T-1 date and the delivery date all hang off it. If it moves, every row below moves.

---

## What is due, and when it is due

| Date | Item | State |
|---|---|---|
| ~~Sun 13 Dec (BUILD BY)~~ | **CV oral mock — BUILT 27 Nov, 16 days early.** `study/mocks/mock-03-cv-oral.md` — 10 items, 8 minutes, every formula ✅ verified, avoids all six served items. | **DONE** |
| **~Tue 22 Dec** | CV oral mock **POSTED** self-timed (honour system; say plainly that unsupervised means softer evidence) | — |
| **~Mon 21 – Tue 22 Dec** | **Deliver `ANCHORS-CV.md`** in the **email body** (no link, no attachment) | **written 24 Nov · verified 24 Nov · HELD on purpose** |
| **Thu 24 Dec** | **T-1** — light confidence pass, no grilling, stop early, read **only** from `ANCHORS-CV.md` | — |
| **Fri 25 Dec** | Assessment · then debrief ask | — |
| **After 25 Dec** | Final campaign retro, then **disable all three tutor tasks** | — |

### Build early, deliver near — these are two different decisions
- **Building late** means the artefact does not exist when it is needed. The mock was discussed across nine Saturdays and never written. **Fix: build early.** This is where *"before 22 Dec, not on it"* belongs.
- **Delivering early** means it exists but is not at hand when it is needed. **Fix: deliver near.** The two anchor sheets that landed went out **4 days** (`ANCHORS.md`) and **1 day** (`ANCHORS-DL4H.md`) before their assessments. A 2,245-word T-1 sheet mailed a month out sinks down the thread.
- **So: `ANCHORS-CV.md` is finished and must NOT be sent before ~21 Dec.** Sending it early is not keenness, it is burying it.

---

## Bank integrity — audited 2026-11-25, first time

`study/question-banks/cv.md`: **IDs contiguous and unique** (no gaps, no duplicates, monotonic) · **every item has an answer block** · **audience tags all `[OXFORD]`**, correct for a CV course. Re-run with the ID/answer checks in the log row for D70 S3.

**One real defect found, and it needed reading rather than a script:** QB-CV-0010 and QB-CV-0012 ask different questions but **share an answer** — the quadratic-cost-is-why-ViT-patches sentence serves 0010(a) and 0012(b). Both are now cross-annotated. **Two items that share an answer are one measurement, not two**, which matters because flag closure needs *independent* passes.

## Formula verification — the cache is NOT the source of truth

Every file in `study/cache/` carries this header, from September: *"lossy text extraction — math glyphs may be mangled; **verify formulas visually in the PDF before quizzing them**."* **It was never acted on until 2026-11-26, and three of the four formula attributions then checked were wrong.** The extraction collapses every superscript and many symbols to one glyph (`ð`), and each gap had been filled from standard convention and then written as the deck's own.

**The method, which costs about a minute per deck and beats the cache outright:**
1. deck's Drive id: `head -2 study/cache/cv/<deck>.md | tail -1`
2. `mcp__Google_Drive__download_file_content` with `exportMimeType: application/pdf`
3. `pdftotext -f <page> -l <page> <file> -` — **it preserves the maths the cache destroys** (`pymupdf` is not importable here; `pdftotext` and `pdfinfo` are)
4. for superscripts, print codepoints: a mathematical-italic `d` is U+1D451

| item | checked | result |
|---|---|---|
| QB-CV-0011 | 2026-11-26 | **was wrong, and its whole premise did not exist in the deck.** Deck writes all three as `ℝ^d → ℝ^d`; `ℝ^d→ℝ^k`/`ℝ^v` was invented. Rewritten, and the new version is a better question. |
| QB-CV-0025 / 0026 | 2026-11-26 | **wrong symbol** — the kernel is `d`, not `h`. Maths unaffected (convolution commutes). Fixed. |
| QB-CV-0034 | 2026-11-26 | **verified exactly** — `p(x) = ∏ p(xᵢ \| x₁ … xᵢ₋₁)`, wording and all. |
| QB-CV-0035 | 2026-11-26 | **wrong symbol** — the deck's network is `f`, not `ε_θ`. Substance unaffected. Fixed. |
| QB-CV-0019 | 2026-11-27 | **verified exactly** — the deck states the theorem in words and gives both directions. |
| QB-CV-0007 | 2026-11-27 | **wrong symbol** — the deck writes **`φ`**, not `f`, and the signature `ℝ^(H×W×3) → ℝ²` is verbatim its own. Also: nearest-neighbour is taught on slides 8–11 and the embedding on 12; **pairing them was my construction** and is now flagged as such. Fixed. |
| QB-CV-0036 | 2026-11-27 | **verified** — `for t = T, …, 1` with `x_T ~ N(0,I)`, and the update uses `f(x_t,t)`, consistent with the deck naming the network `f`. |

**Status: every item that quotes a deck formula, signature or numeric structure now carries a ✅ marker.** **Tally: nine such items; four carried a wrong symbol** (0007 `φ`→`f`, 0011 the invented `ℝ^k`/`ℝ^v`, 0025/0026 `d`→`h`, 0035 `f`→`ε_θ`), **five were exact** (0008, 0019, 0034, 0036, 0040).

**And a third false completion claim, made the same hour as the rule against them.** Twenty minutes after writing *"verification is exhaustive over a bounded set, never sampled by judgement"*, this section said **"all formula rows are now closed"** — built from the three items I had *flagged* rather than from a sweep. A grep for formula characters then found **0008, already served to him, never checked** (it verified clean). *The curated list is the same instrument as the felt-risk rating: both are memory standing in for a scan.* The sweep that caught it was also over-broad, flagging five items whose only "formula" was an arrow in prose — and **an over-broad sweep you then dismiss by hand is triage-by-judgement wearing a script.** So the rule is now precise about its own scope, which is what makes the grep and the rule agree:

> **A ✅ marker is required on any item that quotes a formula, a function signature, or a numeric structure (like `4×4×8 = 128`) and attributes it to the deck.** Arrows or `×` inside ordinary prose do not need one. And the triage was wrong too — 0007 was rated *"lower risk, written as a derivation"* on 26 Nov and turned out to hold the deck's verbatim signature under a substituted letter. **Do not rank items by how risky they feel: that estimate comes from the same memory that produced the error.**

**Standing rule: an item may not quote a formula as the deck's until it carries a ✅ VERIFIED marker.** Every formula-bearing CV item now carries one.

## Picture questions — the first one has shipped

**QB-CV-0042 was sent 2026-11-27 (D72), inline in the email body.** Figure: `study/figures/qb-cv-0042-horse-heatmap.png` — send with `SendUserFile` **and** in the email body. Prepared at D71 S3 and held one window because that day's email was spent. *Built early, delivered near: "near" meant the next window that could ring the bell, not a month out.* **Make more of these** — it is the cheapest instrument in the campaign for a student who has gone quiet, and the only format where the figure carries the question.

**Gmail gotcha, two failed sends:** attaching a file *by reference* requires **`replyToMessageId` + an explicit `to`**, never `replyThreadId`, or the call refuses and sends nothing. It still threads correctly. The reference is `sha256:<64 hex>:<absolute path>` with the digest actually computed (`sha256sum`).

It is the horse-watermark slide from `09`, **cropped above the deck's own answer line** so the question is not given away. The figure was rendered and **looked at** before use. **Why this one first:** it attacks FP-9, the dominant flag, and it is the one item where the picture is load-bearing rather than decorative — the accuracy number cannot show the failure and the average heatmap can. It is also a **ten-second look rather than a paragraph**, which is the best shape to offer someone who has been silent a long time.

**How to make more:** `pdftoppm -f N -l N -r 150 -png -x X -y Y -W W -H H <pdf> <out>` crops at render time, which is how the answer line was removed. **Always render the full page, read it yourself, then crop** — the crop box cannot be guessed from the text layer.

## Artefact states

| Artefact | State |
|---|---|
| `ANCHORS.md` | [AUS] IntroML · delivered in-body 12 Nov · **assessment past — source material only, never T-1 content for the CV oral** |
| `ANCHORS-DL4H.md` | [OXFORD] DL4H · delivered in-body 19 Nov · **assessment past — source material only** |
| `ANCHORS-CV.md` | **live.** Coverage is an explicit list on its face: covered FP-9/1/2/4/5/6/7 · omitted on purpose FP-3, FP-8 (IntroML-only, assessment past). **Not delivered — see the date above.** |
| `mocks/mock-01-aus-oral.md` | **WITHDRAWN UNRUN 17 Nov** (assessment had passed). Available on request, **not owed, not to be re-offered.** |
| `mocks/mock-02-dl4h-oral.md` | **WITHDRAWN UNRUN 24 Nov** (same reasoning, applied four days late, during which it was the whole live queue and blocked all CV serving). Same terms. |
| `mocks/mock-03-cv-oral.md` | **BUILT 27 Nov (D72), unrun, held.** Post self-timed ~22 Dec on the honour system. Cold-set verified against the served list; item 9 shares the COMPAS case with served QB-CV-0029 and is flagged on its face as weaker evidence. |

---

## Standing decisions

- **Scope.** A question went to him on **20 Nov**: (a) keep as is · (b) lighter · (c) pause. **No reply.** The campaign runs on **(a) as a stated default** — call it a default, **never "his choice"**.
- **Cadence.** Three windows a day, 15 min hard cap each. Set by Jayroop 2026-10-17 — *given, not derived.*
- **Course.** **CV only** from 20 Nov. IntroML and DL4H appear only as cross-course links into CV.
- **Flag closure is not attempted.** It needs 3 consecutive passes on 3 different days and formats; no remaining calendar holds that. The anchor sheets replaced it on 11 Nov.
- **Email.** One per day that has something in it, none otherwise. Alternate asks with deliveries and say which in the first line.

---

## Open questions to him, oldest first

| Asked | Question | Status |
|---|---|---|
| 8 Nov, re-asked 16 Nov | Which course was 16 Nov? | **closed by events** — both assessments have happened, so the inference can no longer mis-aim anything |
| 16 + 20 Nov | **Is the CV assessment really Fri 25 Dec?** It is Christmas Day. | **open — and everything above hangs on it** |
| 16 + 20 Nov | Debrief from either assessment: what was asked, where did you trail off, anything surprising | **open · never received for either** |
| 20 Nov | Scope: keep / lighter / pause | **open · running on (a) as a default** |
