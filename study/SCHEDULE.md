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
| **Sun 13 Dec (BUILD BY)** | **CV oral mock — written and verified by this date.** *A concrete date, because "before 22 Dec, not on it" is the same under-specified instruction that nearly sent the anchor sheet a month early on 25 Nov.* | **does not exist yet** |
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
| QB-CV-0019 (`ℱ{f ∗ g} = ℱ{f}·ℱ{g}`) | **not yet** | standard identity, low risk, but **unverified** |
| QB-CV-0007 (`f : ℝ^(H×W×3) → ℝ²`) | **not yet** | written as a derivation (*"so…"*), not a quotation, so lower risk |
| QB-CV-0036 (`for t = T … 1`) | **not yet** | prose claim verified earlier; the loop body is not quoted |

**Standing rule: an item may not quote a formula as the deck's until it carries a ✅ VERIFIED marker.** Clearing the three rows above is background work, never urgent.

## Artefact states

| Artefact | State |
|---|---|
| `ANCHORS.md` | [AUS] IntroML · delivered in-body 12 Nov · **assessment past — source material only, never T-1 content for the CV oral** |
| `ANCHORS-DL4H.md` | [OXFORD] DL4H · delivered in-body 19 Nov · **assessment past — source material only** |
| `ANCHORS-CV.md` | **live.** Coverage is an explicit list on its face: covered FP-9/1/2/4/5/6/7 · omitted on purpose FP-3, FP-8 (IntroML-only, assessment past). **Not delivered — see the date above.** |
| `mocks/mock-01-aus-oral.md` | **WITHDRAWN UNRUN 17 Nov** (assessment had passed). Available on request, **not owed, not to be re-offered.** |
| `mocks/mock-02-dl4h-oral.md` | **WITHDRAWN UNRUN 24 Nov** (same reasoning, applied four days late, during which it was the whole live queue and blocked all CV serving). Same terms. |
| CV mock | **does not exist.** Build before 22 Dec. |

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
