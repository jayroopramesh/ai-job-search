# Glossary — terms Jayroop has *demonstrated*

Per the teach skill's rule: a term enters here only when he has **used it correctly under retrieval**, not when it has merely been covered. This is a record of compressed knowledge, not a dictionary to read. Terms still being fought over live in the flag table instead.

Opened 2026-09-20 (Week 1 retro). Updated 2026-09-27 (Week 2 retro). **10 entries.**

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

## Added at the Week 2 retro (2026-09-27)

**Laplace distribution** (as a noise model):
The distribution L1 loss implies, exactly as the Gaussian is the one L2 implies. Its tails are **heavier**, so a large residual is merely unusual rather than near-impossible — which is why L1 is the robust choice.
*Demonstrated*: paired "L1 is Laplacian" unprompted, 2026-09-23, closing the half of the table that was missing on 09-18.
*Admitted on the pairing only* — the tail **reasoning** went the wrong way on the same answer (see FP-5), so the direction is not yet his.

**True risk**:
The expected loss over the real data distribution — the quantity you are actually trying to minimise and **cannot compute**, because the distribution is never observed. What you minimise instead is the empirical risk, the average loss over the finite sample in hand.
*Demonstrated*: named the uncomputable quantity correctly, 2026-09-23.

### Not yet admitted
- **Empirical risk** — he reaches for it correctly *as a concept* but called it "expected risk", which is the name of the thing you cannot compute. The collision is the problem; admit it once the two names come out the right way round.
- **Lazy learner** — failed under retrieval 2026-09-23 despite a correct margin note in his own hand. Re-framed and re-asked 09-24, still standing.
- **Magnitude domination in KNN** — the mechanism was produced cleanly (FP-1, 1/3), but one pass is not a demonstration. Admit at 2/3.

