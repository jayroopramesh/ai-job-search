# Question Bank — IntroML (CMP 466) · [AUS]
<!-- Appended by tutor sessions. Format: see README.md. -->

### QB-INTROML-0001 · [AUS] · intuition · deck 3 KNN p.13–17 · first asked 2026-09-17
Q: KNN on raw `age` (20–60) and `loan amount` ($18k–$220k), no preprocessing. Which feature decides every neighbour, and why does the other barely matter?
A: Loan amount. Euclidean distance squares raw differences, so a loan gap of tens of thousands utterly swamps an age gap of tens — age contributes ~nothing to the ranking. Fix: scale features (deck uses min-max; time series standardised to mean 0, sd 1). Nothing to do with correlation between the features.
Asked: 2026-09-17 🟡 (right answer "loan amount", wrong mechanism: said the features aren't correlated)
Linked flag: FP-1

### QB-INTROML-0002 · [AUS] · complete the sentence · deck 3 KNN p.9 · first asked 2026-09-17
Q: "In KNN, if k is too small the classifier becomes ______; if k is too large, ______."
A: Sensitive to noise points (overfits); the neighbourhood starts including points from other classes (over-smooths/underfits). Deck also notes k should not exceed double the smaller class's size, or the majority vote is decided before you look at the features.
Asked: 2026-09-17 ✅ ("overfit, underfit" — correct mapping)

### QB-INTROML-0003 · [AUS] · compare · deck 3 KNN p.18 · first asked 2026-09-17
Q: Two pairs of 12-word document vectors — Pair 1 shares 10 of 12 words, Pair 2 shares none — yet Euclidean distance returns the same value for both. Why, and what does cosine measure instead?
A: Both pairs differ in exactly two positions, and Euclidean only counts *how many* coordinates mismatch (√2 either way); it is blind to how much the documents overlap. Cosine measures the angle between the vectors, i.e. shared components relative to length: ≈0.91 for Pair 1, 0 for Pair 2. With non-negative counts the angle range is 0°–90°, so "no shared words" = orthogonal = cos 0, never 180°.
Asked: 2026-09-17 ❌ (no account of the Euclidean tie; said cosine "takes 180 degree")
Linked flag: FP-2

### QB-INTROML-0004 · [AUS] · open · deck 5 Overfitting p.15 · first asked 2026-09-17
Q: Validation set vs test set — what is each for, and what goes wrong if you tune on the test set?
A: Validation is carved out of the *training* data to estimate generalization error while building the model (choosing hyperparameters, early-stopping thresholds); its drawback is less data left to train on. The test set is touched once, for the final estimate. Tune on test and that estimate is optimistically biased — it no longer measures unseen performance.
Asked: 2026-09-17 ✅ (correct, framed as data leakage)

### QB-INTROML-0005 · [AUS] · open · deck 4 Decision Trees p.35–36 · first asked 2026-09-17
Q: What does the GINI index measure at a node, and at what class distribution does it hit its maximum?
A: Node impurity. **Maximum** when records are equally distributed across classes (least beneficial for classification); **minimum of 0** when all records belong to one class (most beneficial — a pure node). Used by CART, SLIQ, SPRINT. Distinct from entropy, though both measure impurity.
Asked: 2026-09-17 ❌ (said "entropy?" and placed the maximum at a 0/100 split — that is the minimum)
Linked flag: FP-3, FP-5

### QB-INTROML-0006 · [AUS] · intuition · deck 6 Class Imbalance & Evaluation p.10 · first asked 2026-09-17
Q: Pond of fish, model catches red fish. Describe high-precision/low-recall and high-recall/low-precision in terms of what is in the net.
A: High precision, low recall = everything you caught IS red, but you missed many red fish (small, clean catch). High recall, low precision = you caught most of the red fish, but hauled in a lot of blue ones too (big, dirty catch). Precision is exactness/quality of the catch; recall is quantity/completeness of red fish found.
Asked: 2026-09-17 ❌ (answers swapped — described low precision as high precision)
Linked flag: FP-4, FP-5

### QB-INTROML-0007 · [AUS] · interview-style · deck 5 Overfitting p.16 · first asked 2026-09-17
Q: Two models generalize about equally well but one is far more complex. Which do you ship, and what principle backs it?
A: The simpler one — **Occam's Razor** (law of parsimony): "given two models of similar generalization errors, prefer the simpler model." Reason: a complex model has a greater chance of having been fitted accidentally, so its apparent performance is likelier to be an artefact of this particular data. Hence complexity belongs in the evaluation: Gen.Error(Model) = Train.Error + α × Complexity(Model).
Asked: 2026-09-17 🟡 (answered "bias-variance trade-off" — adjacent family, not the named principle, and no reason given)
