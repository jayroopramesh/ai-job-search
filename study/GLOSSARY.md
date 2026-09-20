# Glossary — terms Jayroop has *demonstrated*

Per the teach skill's rule: a term enters here only when he has **used it correctly under retrieval**, not when it has merely been covered. This is a record of compressed knowledge, not a dictionary to read. Terms still being fought over live in the flag table instead.

Opened 2026-09-20 (Week 1 retro). 8 entries.

## Evaluation

**Precision**:
Of everything the model predicted positive, the fraction that was right. False positives are the only error term in its denominator.
*Anchor that worked*: **P → Prediction set.** *Avoid*: "accuracy of the positives"

**Recall**:
Of everything that is actually positive, the fraction the model found. False negatives are the only error term in its denominator — false positives cannot move it.
*Anchor that worked*: **R → Real set.** *Avoid*: "sensitivity" in [AUS] answers (Dhou's decks use recall)

**Validation set**:
Data carved out of the *training* data to estimate generalization error while the model is still being built. Distinct from the test set, which is touched once at the end.
*Avoid*: using "validation" and "test" interchangeably — the deck is emphatic

## Trees and impurity

**GINI index**:
A measure of node impurity. **Maximum** when classes are equally distributed at the node, **zero** when the node is pure. A tree splits *towards* low GINI.
*Avoid*: treating it as interchangeable with entropy — both measure impurity, they are different formulas

## Instance-based learning

**k (in KNN)**:
The number of nearest neighbours whose labels decide the prediction. Too small → sensitive to noise points; too large → the neighbourhood pulls in other classes.
*Avoid*: "the k parameter" without saying which direction each failure lies in

## Data types

**Nominal**:
A categorical attribute with distinctness only — no order. Mode is its summary statistic; a mean is meaningless.
*Demonstrated*: volunteered "mode is useful" for ZIP codes unprompted, 2026-09-18

**Ordinal**:
A categorical attribute with order but no meaningful differences between levels. A mean is *dubious* rather than impossible, because "4 → 5" need not be the same step as "8 → 9".

## Learning principles

**Occam's Razor**:
Given two models with similar generalization error, prefer the simpler one.
*Avoid*: "bias-variance trade-off" — related family, different principle (this substitution cost him a mark on D1)

**Empirical risk minimisation**:
Minimising average loss over the training sample as a stand-in for the true risk, which is unavailable because the data distribution is never observed.
*Avoid*: "maximum likelihood estimation" — MLE is what ERM reduces to for particular loss/noise pairings, not the frame itself

## Not yet admitted
Being fought over in the flag table, and deliberately excluded until demonstrated: **interval vs ratio** (the true-zero discriminator is held but misapplied) · **cosine similarity** (direction right, magnitude-invariance not yet produced) · **L1/Laplace** (half the pairing still missing) · **the curse of dimensionality** (not yet asked).
