# Anchors — the nine things you've gotten wrong, and exactly what to say

**Four minutes to read. Built 2026-11-11 (D56).**
For the night before, and for the ten minutes before you walk in. Not a test — these are the answers.

---

## The one that matters most

**🔴 FP-9 — you stop at the label.**
Fired on **5 of 5** clinic items, and still the dominant pattern after eight weeks. Every time, the content inside your answer was right; what was missing was the *because*.

> **The move: after you name the thing, say one more sentence starting with "because".**

That's it. That single habit is worth more than any fact on this page. An examiner who hears "it overfits" has heard a label; one who hears "it overfits **because** the extra nodes are fitting noise in the sample rather than structure in the population" has heard that you understand it. You already know the because — on D7 you produced a complete mechanism unprompted the one time you were shown an expression instead of asked for prose. The knowledge is there. The habit of saying it out loud isn't, yet.

**And a second habit, from the same root:** if you don't know, say "I don't know, but here's how I'd work it out" and then walk the formula. That scores far better than a confident label, and on D7 asking to be shown the formula was the single most useful thing you did all campaign.

---

## Directions — get the arrow right

**🟠 FP-5 — directional inversion.** You had the right pairing and the right vocabulary and still ran the arrow backwards (said L1 penalises outliers *extra*; it penalises them **less**).
> **Anchor: heavy tail = tolerant.** A heavy-tailed noise model expects big residuals, so the loss shrugs at them. Thin tails (Gaussian/L2) treat a big residual as near-impossible, so the fit contorts to kill it. **L1 is the robust one.**

**🟠 FP-6 — losses encode noise models.** L2 ↔ Gaussian is secure; L1 ↔ Laplace is now in place too. The *why* is the tail argument above — same anchor, don't separate them.

**🟢 FP-3 — Gini extremes.** You once put the maximum at a pure node.
> **Anchor: 50/50 is maximum impurity, pure is zero, and the tree drives it DOWN in the children.** Same shape for entropy. Impurity measures how mixed a node is; a split that doesn't reduce it is a split that bought nothing.

---

## Denominators and definitions — say the formula, not the name

**🟢 FP-4 — precision ↔ recall.** You swapped these twice on D1, then fixed it on D2 by *reasoning from the denominators* rather than recalling a fact. That's the method; use it again.
> **Anchor: Precision = of everything I flagged, how much was real. Recall = of everything that was really there, how much did I catch.** Say the denominator out loud and the direction follows. Trigger-happy model → recall up, precision down. Sepsis screen → **protect recall**, because a missed case is dead and a false alarm is a second test.

**🟠 FP-2 — cosine vs Euclidean on text.** You had the direction unprompted and then stalled on the property.
> **Anchor: cosine is magnitude-invariant — it only sees the angle.** So a 2-page and a 20-page report on the same patient look *similar* to cosine and *far apart* to Euclidean, because Euclidean sees length.

**🟠 FP-8 — attribute types.** You now have the true-zero rule and misapplied it (called kg "interval").
> **Anchor: a true zero means zero of the thing. Weight in kg has one — it's RATIO.** Temperature in °C doesn't (0°C isn't no-temperature) — that's interval. Zip code is nominal, pain scale is ordinal. And: **mode** is the right statistic for nominal, which you volunteered unasked, so you have this better than the one error suggests.

**🟢 FP-7 — adjacent-concept substitution.** Not recurring: you named Occam's Razor correctly, then **empirical risk minimisation** correctly — the exact item you answered "MLE" to on D1.
> **Anchor: empirical risk = the error you can measure on your sample. True risk = the error you actually care about, on the population.** Minimising the first hoping it tracks the second *is* the whole game, and the gap between them is overfitting.

---

## The one you've already fixed — keep it

**🟢 FP-1 — why an unscaled attribute dominates KNN.** Four attempts, then on D7 you produced it complete and unprompted: *"Income decides, it's several magnitudes higher. Age is too small and will get drowned out without scaling."*
> That is the full mechanism: the term named, the cause identified as **magnitude** (not correlation), the domination of the sum stated. **Say it exactly like that.** It's the model for how all nine of these should sound.

---

## If you read nothing else

1. **Say the "because".** Every time. It's the single biggest gap between what you know and what you score.
2. **Heavy tail = tolerant.** L1 is robust.
3. **Say the denominator** and precision/recall sorts itself out.
4. **Impurity goes down** in the children.
5. **"I don't know, but here's how I'd work it out"** beats a confident label.

*Flag detail and history: `study/student_progress.md`. Nine open, four moving, none formally cleared — clearing needs three passes on three different days, which the remaining calendar cannot hold, so this sheet exists instead.*
