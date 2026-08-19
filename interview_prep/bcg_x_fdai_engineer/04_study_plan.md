# 6-Day Study Plan + Exam-Day Runbook

Invite received Aug 19; link expires **Aug 26, 1:54 AM PDT = 08:54 UTC**
(≈ 12:54 PM in the UAE). Plan assumes sitting the test **Aug 24 or 25** —
never on the expiry day itself (a technical hiccup then is unrecoverable).

Daily load: ~2.5–4 focused hours. Every drill follows the intuition protocol
from `03_intuition_curriculum.md` §6: classify out loud → invariant sentence
→ complexity budget → only then code. Python for everything, including drills.

## Day 0 — today, Aug 19: platform + meta-skills (~2h)
- Log into CodeSignal via the invite, **do not press "Let's Go"** (that
  starts the real, proctored, one-shot run). Press **Practice** instead —
  unscored, invisible to BCG X.
- Configure the IDE before anything else: Python 3 in the language selector
  (top right), theme/font in Settings (bottom left). Type a few functions to
  feel the editor, run custom test cases.
- Work through the per-type practice questions once, untimed.
- Read curriculum §0 (meta-skills) and §5 (idioms). Hand-write the two
  skeletons (sliding window, running-hashmap) from memory twice.

## Day 1 — Aug 20: Q1/Q2 fluency + official examples (~3h)
- The four official example problems: classify + invariant + implement.
- 4–5 Q1/Q2-grade warm-ups (LC Easy: two-sum, valid anagram, merge sorted
  arrays, longest common prefix, plus one string-cleanup of your choice).
  Target: ≤ 10 min each including a custom edge test.
- CodeSignal Learn (premium): the **hashing/dicts/sets** and **sorting &
  complexity** modules of "Mastering Algorithms and Data Structures in
  Python". **Skip the linked-list, graph, and DP modules — out of scope.**

## Day 2 — Aug 21: Q3 day — matrix bashing (~3.5h)
- 5 problems from the Q3 list: Spiral Matrix, Rotate Image, Diagonal
  Traverse, Reshape the Matrix, Count Square Submatrices with All Ones.
- Practice the decomposition ritual on each: name the helpers before coding
  (`in_bounds`, `next_cell`, `can_place`…), then implement.
- Re-do the Tetris-drop official example cold, from the blank page.
- Log every off-by-one you commit; each becomes a personal check-item.

## Day 3 — Aug 22: Q4 day — the hashmap eye (~3.5h)
- 6 problems from the Q4 list, in this order: Longest Consecutive Sequence,
  4Sum II, Pairs of Songs Divisible by 60, K-diff Pairs, Count Nice
  Subarrays, Max Sum of Pair With Equal Digit Sum.
- For each: write the brute force *in comments first*, name what its inner
  loop searches for, then replace it with the lookup. That replacement move
  is the entire skill.
- Finish with 15 minutes of pure classification: read 8–10 unseen problem
  statements (any source), classify + invariant only, no code.

## Day 4 — Aug 23: Mock #1 under real conditions (~3h)
- Build a 70-minute mock: 1 unseen easy + 1 unseen easy-medium + 1 unseen
  matrix problem + 1 unseen hashmap problem. Webcam on, single monitor,
  phone away, one documentation tab only, scratch paper on the desk.
- Enforce the exam time gates (below) with an actual timer.
- Afterwards: score honestly (hidden-test mindset — did you test edges?),
  then patch the two weakest archetypes with 2 targeted drills each.

## Day 5 — Aug 24: Mock #2 + dress rehearsal (~3h) — or test day
- Mock #2, same recipe, new problems. If both mocks land "3 solved + Q4
  brute-force submitted" or better, you are ready — consider sitting the
  real test today while sharp.
- Proctoring dress rehearsal (15 min): ID physically on the desk, disconnect
  any second monitor, close every app, check webcam framing and lighting,
  stable network (wired or best Wi-Fi spot), power plugged in.
- Light review only after the mock. No new material.

## Day 6 — Aug 25: test day (latest safe day)
- Morning: 30-minute warm-up — one easy problem + re-read curriculum §7
  (mistakes) and the runbook below. Nothing new.
- Sit the test at your sharpest hour. Buffer day left before the Aug 26
  expiry in case of technical failure needing CodeSignal support.

---

# Exam-Day Runbook

## Setup (T-30 min)
- Single monitor (external ones physically unplugged), power connected,
  strongest network. Chrome/Firefox/Edge, fully updated.
- Government photo ID on the desk. Alone in the room, face well-lit.
- Close everything except: the assessment tab + ONE documentation tab
  (docs.python.org). Web searches for syntax only — never for approaches.
- No AI tools, no phone, no second device, no dev console. Scratch paper +
  pen ready. Water within reach.
- Expect: consent screen → ID photo + selfie → camera/mic/screen share.
  If the connection drops you're sent back to proctoring setup and the clock
  keeps running — this is why the network check matters.

## Order of attack and time gates
```
0:00–0:03   Open all four. Classify each (archetype + budget). 30s per question.
0:03–0:11   Q1. Submit by 0:11 at the latest.
0:11–0:25   Q2. Brute force is intended. Submit.
0:25–0:27   READ Q4 properly. Decide:
            → Q4 idea clicks?  do Q4 now (it is worth more than Q3).
            → No idea yet?     do Q3 now; the idea often surfaces meanwhile.
Path A (Q4 first):   Q4 → submit by 0:48. Q3 → submit by 1:05.
Path B (Q3 first):   Q3 → hard stop 0:45 even if unfinished — SUBMIT partial.
                     Q4 → brute force submitted by 0:55, then optimize.
1:05–1:10   Final pass: re-read each spec against your code; run edge tests
            (empty, single element, duplicates); make sure ALL FOUR have a
            submission recorded.
```

## Standing rules (from the scoring model)
1. **Every question gets a submission.** Highest submission per question is
   kept; a blank scores zero; partial credit is generous.
2. **Submit the moment something works**, then improve. Early submissions
   are free insurance.
3. **Never polish.** Style moves the score by rounding error; a solved
   question moves it by ~40 points.
4. **Q3 never eats Q4's time.** If forced to choose, Q1+Q2+Q4 > Q1+Q2+Q3.
5. Stuck 10+ minutes on the Q4 insight → write and submit the brute force,
   move on, come back.
6. Panic protocol: 20 seconds, breathe, re-read the constraint line — it
   names the intended complexity, which names the approach family.

## After submitting
- Expect status silence for 1–2 weeks; a stale "Assessment Requested" is not
  a rejection. No thank-you email needed for an automated test.
- Start light prep for round 2 (live coding + technical case) only after
  results: see `02_research_synthesis.md` §7.
