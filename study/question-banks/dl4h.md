# Question Bank — DL4H · [OXFORD]
<!-- Appended by tutor sessions. Format: see README.md. Seeded from Day 1 baseline onward. -->

### QB-DL4H-0001 · [OXFORD] · complete the sentence · L2 p.2 · first asked 2026-09-17
Q: "Training a neural network means minimising a loss over the data. The formal name for this principle is ______."
A: **Empirical risk minimisation** — minimising expected loss under the empirical data distribution, standing in for the true risk. (Maximum likelihood is related but narrower: it is what ERM reduces to for particular loss/noise pairings, e.g. cross-entropy.)
Asked: 2026-09-17 🟡 (answered "maximum likelihood estimation")
Linked flag: FP-7

### QB-DL4H-0002 · [OXFORD] · open · L2 p.15–16 · first asked 2026-09-17
Q: Every loss encodes a noise model. Which noise does L2 assume, which does L1 assume, and why does MSE let outliers dominate?
A: L2 ↔ **Gaussian** noise; L1 ↔ **Laplace** noise; cross-entropy ↔ **categorical uncertainty**. "Choosing a loss is choosing which errors are plausible." MSE squares the residual, so a point 10× further out contributes 100× the loss and dominates the gradient — Gaussian tails are thin, so the loss treats a large residual as near-impossible and strains to fix it.
Asked: 2026-09-17 ❌ ("no idea")
Linked flag: FP-6

### QB-DL4H-0003 · [OXFORD] · structural · L2 p.22 · first asked 2026-09-17
Q: Dice = 2TP / (2TP + FP + FN). For a scan with many false positives, which of precision and recall is damaged, and which is untouched?
A: Precision is damaged (FP is in its denominator: TP/(TP+FP)). Recall is untouched — FP appears nowhere in TP/(TP+FN); only false negatives move recall. Dice is hurt by both, which is why it behaves like a balance of the two.
Asked: 2026-09-17 ❌ (said false positives affect recall)
Linked flag: FP-4, FP-5

### QB-DL4H-0004 · [OXFORD] · open · L2 p.20 · first asked 2026-09-17
Q: Why were overlap-based losses like Dice proposed for segmentation instead of plain pixel-wise cross-entropy?
A: **Class imbalance.** Pixel-wise CE is summed over every pixel, and in a large scan the background vastly outnumbers a small structure — so the total is dominated by the sheer *count* of easy background pixels (each contributing a small loss), and predicting "all background" already scores well. Overlap losses measure agreement on the structure itself, so a small tumour still carries weight.
Asked: 2026-09-17 🟡 (core insight correct — small tumour drowned out — but said CE is "high for all the parts that match"; CE is *low* where prediction matches, it is their number that dominates)
Linked flag: FP-5
