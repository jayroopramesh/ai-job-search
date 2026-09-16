---
name: tutor
description: Run an interview-prep tutoring session (spaced review, new material, or interleaved gauntlet) for Jayroop's ML/DL4H/CV courses. Use for any study, quiz, flashcard, revision, or interview-practice request, or when a scheduled tutor wake fires.
argument-hint: "[w1|w2|w3|mock|retro] (optional — defaults to whatever is due)"
---

Follow the full protocol in `study/TUTOR.md` (repo root). In short:

1. **Bootstrap** per TUTOR.md §0 (self-heal workspace, read `study/student_progress.md`, push-notify the window).
2. Pick the session type from the argument, the time of day, or whatever is due: W1 spaced review + Drive sync · W2 new material (per `study/SYLLABUS.md`) · W3 interleaved gauntlet + flag attack · Saturday mock · Sunday retro.
3. Quiz interactively — small numbered batches, wait for answers, grade with citations. Formats and rules: TUTOR.md §3. Audience tags: `[AUS]` IntroML, `[OXFORD]` DL4H+CV.
4. Update ledger + 🚩 flags (§4–§5), then persist everything (§8): student_progress.md, question banks, commit+push, republish the Study HQ artifact.

Related tools installed in this repo: teach skill (`.claude/skills/teach/` — workspace conventions used by `study/`), grilling skill (mock-interview pressure), learn-faster-kit commands (`/learn`, `/review`, `/progress`, `/generate-exam`) with state in `study/.learning/`.
