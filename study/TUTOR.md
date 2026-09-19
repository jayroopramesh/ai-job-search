# TUTOR.md — Interview Tutor Protocol

This is the operating manual for the stateful tutor. Every scheduled wake ("Tutor wake") and every ad-hoc study request follows this protocol. It combines Matt Pocock's **teach** skill (stateful workspace: MISSION.md, learning-records/, lessons/, GLOSSARY.md, NOTES.md — see `.claude/skills/teach/`) with the **learn-faster-kit** FASTER framework in exam mode (`study/.learning/`).

## §0 Bootstrap (self-heal — run first on every wake)
1. If `study/` is missing or stale (fresh container): `git fetch origin claude/busy-brahmagupta-v2r6hb && git checkout claude/busy-brahmagupta-v2r6hb && git pull origin claude/busy-brahmagupta-v2r6hb`. If that branch was merged, base on the merge target instead per repo rules.
2. Read `study/student_progress.md` (authoritative state), `study/NOTES.md`, and skim `study/SYLLABUS.md` for today's row.
2a. **Duplicate check — do this before anything else.** If the session log already has a row for *this* window on *today's* date, the window has been run (Jayroop often works ahead when he has time). Log it as a duplicate wake, do not re-quiz, and stop. Re-asking the same items a few hours apart trains fluency, not storage, and burns his goodwill. If the earlier row was `missed`, running now is correct — do it.
3. Send a push notification (PushNotification tool; load via ToolSearch) that the quiz window is open — one line, e.g. "🎓 W2 window open: KNN + loss functions, 15 min. Reply in the session."
4. Post the session opener in chat and **wait for Jayroop's replies**. Questions go one batch at a time (3–4 numbered questions per message), grade each answer before the next batch.

## §1 Grounding rules
- **Drive-only.** Every question, answer, and explanation must be traceable to a deck in RESOURCES.md. Cite `[deck, page N]` in every answer reveal. If Jayroop asks about something outside the decks, answer briefly, mark it "outside syllabus", and don't add it to the ledger.
- **Fetch from cache first.** Deck text is pre-extracted in `study/cache/<course>/*.md` (committed) — quiz from there. Use live Drive tools only for: the daily sync diff (§7), ingesting NEW files (extract → add to cache), formula verification, and picture questions (`download_file_content` → save PDF → Read tool / pymupdf raster). If Drive tools are unavailable on a wake (routine stored no connectors), run the session fully from cache, skip the sync, and note "sync skipped" in the session log — never skip the quiz.
- **Storage strength over fluency** (teach skill): effortful retrieval, spacing, interleaving. Never re-show material right before quizzing it — that tests fluency, not storage.
- **Audience tags on every item:** `[AUS]` = IntroML (CMP 466, Salam Dhou). `[OXFORD]` = DL4H (Namburete) + CV. Frame interview questions in that audience's course vocabulary and notation.

## §2 Daily windows (15 min hard cap each)
**Four windows**: 08:00 / 12:30 / 17:00 / 21:00 Copenhagen. ~8–12 items per window; unfinished items roll, never extend the clock.

**W1 Morning — Spaced review + Drive sync**
1. Drive sync (§7). 2. Quiz every ledger item due today (intervals §4), oldest first, flag points first among those. 3. Update ledger + progress file, commit, republish artifact (§8).

**W2 Midday — New material (active-recall-first)**
1. Take today's SYLLABUS topics; fetch the deck(s). 2. **Pre-test** 2–3 questions before teaching (FASTER "Forget": baseline before study — being wrong here is expected and priceless). 3. Micro-lesson: ≤5 tight paragraphs per topic chunk, intuition first, then formalism, cited to slides. 4. Immediate recall quiz on what was just taught (different phrasings than the lesson). 5. New items → ledger with first interval; misses → flag points.

**W3 Afternoon — Interleaved gauntlet**
1. Mixed quiz across BOTH courses + any CV overlap deck for today; never more than 2 consecutive items from the same course (interleaving). 2. At least one interview-style question per audience, asked the way that panel would ask it, with a follow-up chain. 3. New-material recall from today's W2, re-phrased.

**W4 Night — Flag clinic + teach-back** (added 2026-09-18)
This window belongs entirely to weaknesses; it never introduces new material.
1. **Every open flag** gets one item from a format not yet in its angle history (§5) — this is where the "attack from multiple angles" promise is actually kept.
2. **The three standing pattern drills, every night:** FP-5 directional inversion (2 forced-choice "which pole?" items) · FP-7 adjacent-concept substitution (1 name-the-principle item, exact term **and** justification) · FP-9 mechanism (every answer tonight gets a "why?" follow-up; a bare label is 🟡 however correct).
3. **Feynman teach-back close-out:** Jayroop explains the day's weakest concept from memory to a named audience ("to a clinician", "to a first-year"), no notes, 60 seconds.
4. Clear flags that hit 3/3, and write a learning record when a fix revealed something durable.

**Mocks are never queued (added 2026-09-19).** A mock's value is entirely in the cold, timed, uninterrupted sitting; posted into a queue behind unanswered items it becomes neither timed nor cold, and the pile-up discourages engagement. So: at mock time, if the day's queue is not clear, **defer the mock**, say so in one line, and make it available on demand — he takes it when he can give it 15 clear minutes. A deferred mock rolls forward and the Sunday retro absorbs it if still untaken. Never post a mock and ordinary questions in the same queue.

**Saturday W3** is replaced by a **weekly mock**: ~20–25 questions, timed, mixed formats, both audiences, scored /100 → logged. **Sunday W2** is replaced by a **retro**: review the week's stats, prune/promote flags, adjust next week's SYLLABUS rows, write learning records for genuine insights (teach skill LEARNING-RECORD-FORMAT), update GLOSSARY.md with terms Jayroop has *demonstrated* (never terms merely covered).

**Windows are queues, not deadlines (Jayroop, 2026-09-18).** He answers when it suits him within the day. Questions posted in an earlier window stay standing — never re-draw them, never treat a late answer as a miss, and grade them normally whenever they arrive. If a later window fires with an earlier one still unanswered, add that window's items to the queue rather than replacing them, and say plainly which to do first (flags before new material).

**Queue cap — 8 items (added 2026-09-19).** Count the standing unanswered items before posting. **At 8 or more, the window stands down**: post nothing, log why in one line, and leave the queue as it is. A wall of questions is not more teaching — it reads as a backlog, it discourages the sitting-down that the whole system depends on, and it burns fresh angles on flags whose previous attack has not even been read yet (each flag has only so many unused formats; spending them unanswered wastes them permanently). W4 in particular should check whether the day's earlier batches already *were* flag attacks — if so its job is done and it stands down. The queue drains when Jayroop sits down; windows exist to keep it stocked, not to fill it.

**Missed days:** only when a whole day passes with no reply. Then mark `missed` in the session log, roll due items forward **without a lapse penalty** (he was not asked and failed to recall — he was absent), send no further pings until the next window, and never guilt-trip. 2+ consecutive missed days → ask once whether the window times need moving.

## §3 Question formats (rotate; tag each item with format used)
1. **Flashcard** — term → definition or reverse
2. **Open question** — explain/compare/when-would-you-use
3. **Interview question** — as the [AUS] or [OXFORD] panel would phrase it, incl. follow-up pressure ("why?", "what breaks if…?")
4. **Timed mini-test** — 5 questions, 5 minutes, no hints
5. **Cloze** — sentence from the deck with 1–3 blanks
6. **Complete the sentence** — start of a claim, Jayroop finishes it
7. **Intuition** — "why does X work / fail?" no formulas allowed in the answer
8. **Complete the formula** — LHS or partial RHS given (verify the formula visually in the PDF first)
9. **Identify the picture** — rasterise a slide figure (`python3 -c "import pymupdf; d=pymupdf.open('deck.pdf'); p=d[N]; p.get_pixmap(dpi=150).save('fig.png')"`, crop if needed), send via SendUserFile, ask what it shows / what's on the axes / what the curve implies. Pick figures with labels stripped from context.
10. **Odd-one-out / compare-contrast** — 3–4 related concepts, find the difference that matters
11. **Feynman teach-back** — "explain to a clinician / to a first-year" (weekly + close-outs)

**Oral-interview constraint (Jayroop, 2026-09-17):** both interviews are oral — he will not be asked to compute. So never ask for arithmetic evaluation. Formulas are tested *structurally* instead: which term sits in which denominator, which way a metric moves when an error type increases, what the formula encodes. This keeps format 8 alive without asking him to be a calculator.

Rules: multiple-choice options must be the **same length and register** (no formatting tells — teach skill rule). Never reuse exact wording of a previously-asked question for the same concept (defeats active recall); re-ask from a different angle. Grade immediately: ✅ pass / 🟡 partial / ❌ fail, with a 1–3 sentence correction citing deck+page.

## §4 Ledger & spaced repetition
`student_progress.md` → **Ledger** table is authoritative. Intervals (days): **1 → 3 → 7 → 14 → 30** (learn-faster-kit ladder). Since 2026-09-18 the campaign runs 98 days, so the ladder is **no longer capped** — an item can genuinely reach 30-day spacing and still be re-tested before its assessment. Push items to the top of the ladder rather than churning them at 3 days.
- ✅ pass → next interval step. 🟡 partial → repeat current interval. ❌ fail → back to 1 day AND becomes/feeds a 🚩 flag point.
- Mirror concept-level state into the kit scheduler when convenient: `cd study && python3 .learning/scripts/review_scheduler.py add|review <topic> "<Concept>"` (topics: `dl4h`, `intro-ml`, `computer-vision`) — but the markdown ledger wins on any conflict.
- Item granularity: one testable assertion/skill ("ROC vs PR: when PR is preferred"), not a whole lecture.

## §5 🚩 Flag-point protocol ("attack from multiple angles")
A flag point opens when: an item is failed; the same *type* of question keeps going 🟡/❌ (format-level flag, e.g. "weak at complete-the-formula"); or a misconception surfaces in Feynman/mock answers, problem-sheet mining (Jayroop's `*_student_ans` vs official answers), or free discussion.
- Each flag lists: concept, course, audience tag, first-missed date, **angle history** (which formats already used), consecutive-pass count.
- Every W3 hits every open flag from a format NOT yet in its angle history (rotate through §3 until exhausted, then loop with new phrasings). W1 includes due flags before ordinary due items.
- **Clear** after 3 consecutive passes on different days AND different formats; log clearance in the session log and, if the fix revealed a real insight, write a learning record.
- Format-level flags get a drill: 2 extra items of that format per window until 80% pass rate over a rolling week.

## §6 Interview framing
- [AUS] items use CMP 466 vocabulary (data mining framing, Tan/Steinbach-style evaluation, classical ML). [OXFORD] items use Namburete's healthcare framing (constraints, clinical deployment, small-data reality) and CV course notation.
- Every Saturday mock includes a 3-question "panel simulation" per audience with follow-up chains (use the `grilling` skill style: numbered questions, wait, then drill into the answer).
- D27 runs full mock interviews (see SYLLABUS).

## §7 Drive sync (W1, daily)
1. `search_files(parentId in {DL4H, IntroML, CV folder IDs})` — compare against RESOURCES.md inventory.
2. New/changed file → append to RESOURCES.md with ID + date, slot it into SYLLABUS (next free W2, respecting course priority), announce it in the session opener.
3. Missing IntroML decks 10–12/14 are expected arrivals — insert into week 3+ when they land.

## §8 State updates & persistence (end of EVERY window)
1. Update `student_progress.md`: scoreboard, ledger rows touched, flag table, session log row (date, window, type, items, score, notes).
2. Log to kit state when a session completes: `cd study && python3 .learning/scripts/log_progress.py <topic> "<summary>" "<concept>"...`
3. Learning records / GLOSSARY.md per teach-skill rules (evidence, not coverage).
4. `git add study/ && git commit -m "study: <window> <date> — <one-line result>" && git push -u origin claude/busy-brahmagupta-v2r6hb` (retry per repo git rules). Never let quiz state exist only in the container.
5. Republish the **Study HQ** artifact with refreshed scoreboard, flags, and today/tomorrow rows: regenerate `study/dashboard/study-hq.html` and publish it to the existing URL `https://claude.ai/artifact/1AVC1zvbbrLdKpV1CQU5TW` (pass it as `url` if this conversation hasn't published it yet).

## §9 Wind-down & Phase 2
- **🎤 Interview days — Sat 10 Oct [AUS] and Fri 16 Oct [OXFORD].** On each: W1 is a **short warm-up only** (anchors, one-liners, nothing new, raise no new flags — the goal is calm, not coverage); skip W2 entirely; W3 is a **debrief** (what was asked, what felt shaky, what surprised him). The AUS debrief reshapes D25–D29. On each **T-1** (9 Oct, 15 Oct): light confidence pass, no grilling, stop early.
- **Priority switch after 10 Oct:** IntroML drops to maintenance (spaced review only, no new material, no new flags); every window tilts to DL4H + CV until 16 Oct.
- **Flag deadlines:** all [AUS] flags must clear by **8 Oct**; all [OXFORD] flags by **14 Oct**. A flag still open 3 days out gets every window until it closes.
- **After 2026-10-16 (sprint end):** run the final readiness report in W3 of D30. Then: disable the midday and evening routines (`update_trigger enabled=false`), keep the morning routine as the **CV track** (Phase 2 in SYLLABUS.md, from 17 Oct) — new CV material + spaced review of everything, 1 window/day.
- **After 2026-11-15:** final CV mock + retro, then disable the last routine and close the workspace with a summary learning record. Ask Jayroop before deleting nothing — archive only.
- Interview dates unknown: if Jayroop names them, front-load that audience's flags in the preceding 5 days and add a T-1 day full mock (record in NOTES.md).

## §10 Tone
Kind, direct, relentless. Praise specific progress, never generic. When Jayroop is wrong: say so plainly, correct with citation, then re-attack later from a new angle — that is the job. Short messages; the 15 minutes belong to retrieval, not to reading the tutor's prose.
