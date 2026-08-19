# GCA Intuition Curriculum — recognize the problem before you write a line

Goal: walk into the exam able to classify any of the four questions within 60
seconds of reading it, know the approach family, and know the time it deserves.
Syntax is the one thing the exam lets you look up (one reference tab allowed);
**intuition is the thing it doesn't.** That is what we train.

---

## 0. The three meta-skills (these transfer to every question)

### Meta-skill 1: Constraints are the complexity budget
Read the constraints **before** choosing an approach. They tell you what the
setter expects:

| Constraint on n | Allowed complexity | Signal |
|---|---|---|
| n ≤ ~500–1,000 | O(n²)–O(n³) fine | Brute force is *intended* (typical Q2/Q3) |
| n ≤ ~10⁴ | O(n²) borderline-OK | Simple nested loop usually passes |
| n ≥ 10⁵ | O(n log n) or O(n) | An idea is required: hashmap / sort / window (this is the Q4 tell) |

If n ≤ 10³ and you're inventing something clever, stop — you're burning time
the setter didn't ask for. If n = 10⁵ and you're writing two nested loops,
stop — you're walking into a TLE.

### Meta-skill 2: Read in this order — examples → constraints → prose
The worked examples show you the transformation in seconds; the prose then
confirms edge rules. On Q3 (long spec) this order saves minutes and prevents
the classic failure of half-understanding the task before coding.

### Meta-skill 3: State your loop invariant in one sentence
Before typing, say to yourself what one pass maintains: "as I scan, `counts`
holds the frequency of every element seen so far", "the window [l, r] always
satisfies the condition", "the stack holds indices of bars not yet closed".
If you can't say the sentence, you don't have the approach yet — and writing
code won't produce it.

---

## 1. Q1 — Basic Coding (target ≤ 8 min, 5–10 lines)

**What it is:** one loop, 2–3 basic operations combined, boundary conditions.
The setter's spec explicitly excludes patterns, algorithms, optimization.

| Recognition cue in the statement | Think |
|---|---|
| "given an array/string, return the array/string where each element …" | one pass, build output list |
| "count how many …" | counter += condition |
| digits / year / century / splitting a number | `divmod`, `str(n)`, `% 10` |
| "is X a palindrome / valid" (single string, no nesting) | direct check, `s == s[::-1]` |
| edges named in examples ("if it doesn't exist, use 0") | boundary guards `if i > 0`, `if i < n-1` |

**Official example, walked as reasoning:** `b[i] = a[i-1] + a[i] + a[i+1]`,
missing neighbors count 0.
- *Classify:* one-pass transform + boundary condition. No trick.
- *Invariant sentence:* "each b[i] is the sum of the up-to-3 real neighbors."
- *Approach:* start `b[i] = a[i]`, add left if `i > 0`, add right if
  `i < n-1`. Done. The only way to lose points here is rushing into an index
  error — so run the sample before submitting.

**The Q1 discipline:** it is a *gimme* designed to be beaten in half the
budgeted 10 minutes. Bank the time; you are pre-paying for Q4.

## 2. Q2 — Data Manipulation (target ≤ 15 min, 10–20 lines)

**What it is:** 3–5 basic concepts chained; 1–2 nested loops; the statement
gives step-by-step instructions. Constraints small (≈10³) → **brute force is
the intended solution**. Do not optimize Q2.

| Recognition cue | Think |
|---|---|
| "group by / most frequent / appears more than once" | `Counter` / `defaultdict(list)` |
| substring windows checked against a rule | slide a start index, helper checks one window |
| "sort by X, ties broken by Y" | `sorted(key=lambda t: (x, y))` |
| messy text to clean/reassemble | `split` → transform pieces → `join` |
| compare/merge two collections | sets, or walk both with indices |

**Official example, walked:** count substrings of `source` matching a 0/1
`pattern` where 0=vowel, 1=consonant (vowels include `y`!).
- *Classify:* fixed-length window check. n, m ≤ 10³ → O(n·m) = 10⁶ → nested
  loop is fine by design.
- *Invariant:* "for each start index, the helper decides that one window."
- *Structure:* write `check(start)` as a helper; outer loop sums it. A helper
  per rule keeps the edge case (the vowel list!) in exactly one place.
- *Lesson:* Q2 punishes misread details, not weak algorithms. Re-read the
  definitions ("y is a vowel") before submitting.

## 3. Q3 — Implementation Efficiency (target ≤ 20 min, 25–40 lines)

**What it is:** a long, rule-heavy spec — usually a **2D matrix** — where the
skill is *translating instructions into code without dropping a clause*.
Official exclusions: no graphs, no DP, no number theory. Community name for
it: "bashing-friendly". O(n²)–O(n³) over the grid is expected and fine.

| Recognition cue | Think |
|---|---|
| grid + unusual visiting order (spiral, diagonal, zig-zag) | direction vectors + boundary bookkeeping |
| "rotate / transpose / reflect the matrix" | `zip(*m)` transposes; rotate = transpose + reverse rows |
| a physical process described step by step (falling, filling, moving) | simulate literally; one helper per rule |
| formatting output with padding/wrapping | greedy line packing, `str` methods |
| "compare/merge according to this custom rule" | write the comparator as its own function |

**Official example ("Tetris drop"), walked:** drop a 3×3 figure down a column
of a 0/1 field; find a column producing a full row.
- *Classify:* pure simulation. Nothing clever exists to find — the spec IS
  the algorithm.
- *Decompose before coding:* (1) `can_place(row, col)` — does the figure
  overlap occupied cells? (2) for each column, slide down until `can_place`
  fails, back up one; (3) `row_full(r)` — is row r full counting the figure's
  cells? Three tiny functions, each testable in your head.
- *Lesson:* the monolith version of this is a 4-deep nested loop where one
  off-by-one hides for 15 minutes. The decomposed version localizes every
  bug. **Helpers are not style — they are your debugger.**

**The Q3 trap (strategic):** it is the *longest* question but the *least
valuable* (old-scale: Q1+Q2+Q4 ≈ 810 vs Q1+Q2+Q3 ≈ 760). Never let Q3 eat
Q4's time. Read Q4 before committing to Q3; if Q4 clicks, take it first.

## 4. Q4 — Problem Solving (target 20–30 min, 20–35 lines)

**What it is:** the only question where complexity is graded. n ≥ 10⁵ →
O(n²) will TLE. The official spec names: hashmaps/sets for query
optimization, greedy, divide & conquer, two pointers. **Not** DP, not graphs,
not Dijkstra.

**The single master pattern (internalize this):**
> Write the brute force in your head. Look at its inner loop. Ask: "what is
> the inner loop *searching for*, and can I look that up in O(1) from a
> hashmap/set I build as I go — or is the space of relevant candidates
> bounded and tiny?"

| Recognition cue | Think |
|---|---|
| "count/find pairs (i, j) such that a[i] + a[j] …" | one pass; for each element, look up its *complement* in a running count-map |
| "sum/condition is a power of 2 / multiple of k / equals target" | the candidate set is bounded (≈21 powers of 2; k residues) — loop candidates × lookup |
| "longest run of consecutive values" | put all in a set; only start counting where `v-1` is absent |
| "longest/shortest contiguous subarray/substring with property" | sliding window; the invariant sentence is mandatory |
| "(start, end) intervals, overlap/merge/rooms" | sort by start; sweep with running state |
| "maximize/minimize by choosing an order" | sort + greedy exchange argument |
| "next greater / largest rectangle" | monotonic stack of indices |
| "minimize the maximum …" + monotonic feasibility | binary search on the answer (rare) |

**Official example, walked:** count pairs with `a[i] + a[j]` a power of 2
(n ≤ 10⁵, values ≤ 10⁶).
- *Brute force:* all pairs, O(n²) = 10¹⁰ → dead. Its inner loop asks: "how
  many previous elements equal `P - a[j]` for some power P?"
- *The two moves:* (1) a running `Counter` answers "how many previous
  elements equal x" in O(1); (2) the relevant powers of 2 are bounded — sums
  can't exceed 2×10⁶, so only ~21 powers matter. Result: O(21·n).
- *Invariant:* "when I process a[j], `counts` holds frequencies of a[0..j]
  (including j itself → counts the i = j pair exactly once)."
- *Lesson:* Q4 is never an exotic algorithm. It is **noticing the bounded
  candidate set and replacing the inner loop with a lookup.**

**The Q4 insurance rule:** if the idea won't come, write the clean brute
force and **submit it** with ~10 minutes left. Partial credit is real
(post-2023), the highest submission is kept, and a blank Q4 is the single
most expensive mistake the scoring model allows.

## 5. Python idioms — the 12 you should not have to think about

The allowed reference tab covers exact signatures; these must be reflexes:

```python
from collections import Counter, defaultdict
counts = Counter(arr)               # frequency table in one line
d = defaultdict(int); d[k] += 1     # counting without key checks
d = defaultdict(list); d[k].append(v)  # grouping
sorted(items, key=lambda t: (t[1], -t[0]))  # composite sort keys
for i, x in enumerate(arr): ...     # index + value
for a, b in zip(xs, ys): ...        # parallel walk
list(zip(*matrix))                  # transpose
s[::-1]; s[i:j]                     # reverse / slice
" ".join(parts); s.split(",")       # reassemble / parse
q, r = divmod(n, 10)                # digit peeling
[f(x) for x in arr if cond(x)]      # transform+filter
seen = set(); x in seen             # O(1) membership
```

Plus two memorized skeletons:

```python
# sliding window
l = 0
for r, x in enumerate(arr):
    add(x)                      # extend window to include r
    while broken():             # shrink until invariant holds
        remove(arr[l]); l += 1
    best = max(best, r - l + 1)

# running-hashmap pair count
counts = defaultdict(int)
ans = 0
for x in arr:
    counts[x] += 1              # include x first if (i == j) pairs count
    for cand in bounded_candidates:
        ans += counts[cand - x]
```

## 6. Drill lists (the "repetitions", made concrete)

**The four official examples** (drill until each is a 1-minute classification):
neighbor-sum array; vowel/consonant pattern count; Tetris drop; pairs summing
to a power of 2.

**Q3 family — 12 LeetCode analogues** (aim 15–20 min each):
Spiral Matrix (54) · Spiral Matrix II (59) · Rotate Image (48) · Diagonal
Traverse (498) · Reshape the Matrix (566) · Toeplitz Matrix (766) · Image
Overlap (835) · Largest Local Values in a Matrix (2373) · Transpose Matrix
(867) · Count Square Submatrices with All Ones (1277) · Sort the Matrix
Diagonally (1329) · Text Justification (68 — the string-based outlier).

**Q4 family — 13 LeetCode analogues** (aim 20–30 min each):
Longest Consecutive Sequence (128) · 4Sum II (454) · Pairs of Songs With
Total Durations Divisible by 60 (1010) · Longest Palindrome by Concatenating
Two Letter Words (2131) · Array of Doubled Pairs (954) · 3Sum With
Multiplicity (923) · Count Number of Nice Subarrays (1248) · K-diff Pairs in
an Array (532) · Diagonal Traverse II (1424) · Find Occurrences of an Element
in an Array (3159) · Find the Number of Distinct Colors Among the Balls
(3160) · Max Sum of a Pair With Equal Sum of Digits (2342) · Minimum Absolute
Difference-style mirror pairs.

**How to drill for intuition (not syntax):** for each problem, before any
code — (1) classify the archetype out loud, (2) say the invariant sentence,
(3) state the complexity budget from the constraints. Only then implement.
If classification took > 3 minutes, that problem goes on the re-drill pile;
a wrong-but-fast classification is progress, a slow-correct one is not (the
exam pays for recognition speed).

## 7. Top mistakes (each one is a drill check-item)

1. Off-by-one on Q3 specs → always run empty / single-element / duplicate
   custom tests before submitting (edge cases ≈ 20–30% of hidden tests).
2. TLE on Q4 from an un-analyzed brute force → constraints first, always.
3. Perfecting one question while another sits blank → the ±12 rule: solved
   questions dominate; polish is worth almost nothing.
4. Leaving Q4 blank → submit the brute force, always.
5. Wasting exam time refactoring/renaming → style is effectively unmeasured.
6. Skipping the final 90-second re-read of the spec against your code.
