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

### QB-INTROML-0008 · [AUS]+[OXFORD] · Feynman clinical case · deck 6 p.10 + DL4H L2 · first asked 2026-09-17
Q: A rare-disease screening model flags 500 patients; 40 of them actually have the disease, and it misses 5 cases. Precision problem or recall problem — and how would you put it to a clinician?
A: **Precision problem.** TP=40, FP=460, FN=5 → recall ≈ 40/45 ≈ 89% (it finds nearly every case), precision = 40/500 = 8% (nearly everything it flags is a false alarm). To a clinician: "it almost never misses the disease, but for every real case it sends about eleven healthy people for follow-up." The asymmetry between 460 and 5 *is* the answer — summing them discards it. Worth adding: for rare-disease screening this trade is often deliberate (miss nothing, confirm downstream), which is why the metric you optimise follows the clinical cost.
Asked: 2026-09-17 🟡 (classified 460 FP / 5 FN correctly — first time — then called the two "about the same")
Linked flag: FP-4, FP-5

### QB-INTROML-0009 · [AUS] · forced-choice direction (FP-5 drill) · deck 6 p.10 · asked 2026-09-18
Q: A model is retuned to flag twice as many cases — a few more true positives, many more false alarms. Which of precision/recall rises and which falls?
A: Recall rises (TP up, FN down — the extra real cases found were previously misses). Precision falls (FP grows far faster than TP). Denominators tell you directly: recall = TP/(TP+FN), precision = TP/(TP+FP).
Asked: 2026-09-18 ✅ (reasoned from the denominators unprompted; minor slip — said FN "stays the same" when it falls slightly)
Linked flag: FP-4 (1/3), FP-5 (1/3)

### QB-INTROML-0010 · [AUS] · forced-choice direction (FP-5 drill) · deck 4 p.35–36 · asked 2026-09-18
Q: Node A = 50 records all one class; Node B = 50 records split 25/25. Which has the higher GINI, and which is the tree moving towards?
A: Node B (25/25) has the higher GINI — maximum impurity, least useful for classification. The tree splits *towards* Node A, the pure node, where GINI = 0.
Asked: 2026-09-18 ✅ (both halves correct)
Linked flag: FP-3 (1/3), FP-5 (1/3)

### QB-INTROML-0011 · [AUS] · interview-style + mechanism · deck 3 p.13–17 · asked 2026-09-18
Q: "KNN performs poorly on patient age, weight and annual income. What do you check first?" — then: "Why does that happen? Be precise."
A: Feature scaling — AND the mechanism: Euclidean distance squares raw differences, so income (spread over tens of thousands) contributes a squared term that dwarfs age or weight (spread over tens). The neighbour ranking is then decided by income alone; the other features are arithmetically invisible. Fix: min-max scaling, or standardise to mean 0 / sd 1.
Asked: 2026-09-18 🟡 (said "scaling", stopped there — the requested mechanism was not produced)
Linked flag: FP-1, FP-9

### QB-INTROML-0012 · [AUS] · reverse flashcard (FP-7 drill) · deck 5 p.16 · asked 2026-09-18
Q: Name the principle: "it is futile to do with more what can be done with fewer — prefer the simpler of two models with similar generalization error." Then one line on why.
A: **Occam's Razor** (law of parsimony). Why: a complex model has more ways to fit this particular dataset by accident, so its apparent performance is likelier to be an artefact of the sample than a property of the problem. Hence complexity enters the evaluation: Gen.Error = Train.Error + α × Complexity.
Asked: 2026-09-18 🟡 (named it correctly — the D1 substitution behaviour is fixed — but gave no justification)
Linked flag: FP-7, FP-9

### QB-INTROML-0013 · [AUS] · pre-test → taught · deck 2 p.9–11 · asked 2026-09-18
Q: Classify by attribute type: zip code · 1–5 star rating · temperature in °C · weight in kg.
A: Nominal · ordinal · interval · ratio. The deck's test is four properties — distinctness (=), order (<>), meaningful differences (+−), meaningful ratios (×÷). Interval has meaningful differences but no true zero (10°C is not twice 5°C); ratio has a true zero so multiples are meaningful. Kelvin is ratio, Celsius/Fahrenheit are interval.
Asked: 2026-09-18 ❌ (1/4 — zip correct; star→ratio, °C→ordinal, kg→ordinal)
Linked flag: FP-8

### QB-INTROML-0014 · [AUS] · pre-test → taught · deck 2 p.28 · asked 2026-09-18
Q: Name the data quality problems the deck lists, and say which you'd fix by dropping the feature rather than repairing it.
A: Noise and outliers · wrong data · fake data · missing values · duplicate data. Drop the *feature* when missing values dominate it (his own margin note: "so many missing values → drop one of them"); drop the *record* for duplicates, keeping the most recent. Cleaning = detecting and correcting or removing corrupt/inaccurate records.
Asked: 2026-09-18 ❌ (offered "missing at random" only — a statistical missingness mechanism, not the deck's taxonomy)

### QB-INTROML-0015 · [AUS] · applied intuition (FP-2 new angle) · deck 3 p.18 · asked 2026-09-18
Q: Two clinical reports on the same patient — a 2-page summary and a 20-page workup using the same vocabulary. Which measure calls them similar, which calls them far apart, and what property of each decides it?
A: Cosine calls them similar; Euclidean calls them far apart. Property: **Euclidean measures magnitude, cosine measures direction.** d(a,b)=√Σ(aᵢ−bᵢ)² grows with every count difference, and the long report's counts are several times larger in every coordinate. cos(θ)=(a·b)/(‖a‖‖b‖) divides out both magnitudes, so multiplying a vector by any positive constant leaves it unchanged — only the *proportions* of the vocabulary survive. That invariance is why the deck says cosine is better with text.
Asked: 2026-09-18 🟡 (direction correct unprompted; property "I don't know", asked to be shown the formula)
Linked flag: FP-2, FP-9

### QB-INTROML-0016 · [AUS] · applied means (FP-8 + FP-5 drill) · deck 2 p.9–11 · asked 2026-09-18
Q: A colleague takes the mean of (a) ZIP codes, (b) pain scores 1–10, (c) weights in kg. Which mean is meaningless, which dubious, which fine — and what property decides each?
A: (a) meaningless — ZIP is **nominal**, only distinctness holds, so mode is the summary statistic, not mean. (b) dubious — pain is **ordinal**: order holds but differences are not meaningful, so "average pain 4.7" assumes 4→5 is the same step as 8→9. (c) fine — kg is **ratio**: true zero, so sums, means and multiples are all meaningful.
Asked: 2026-09-18 🟡 (all three sorted correctly and volunteered mode for ZIP; but labelled weight "interval (no absolute zero)" — kg has a true zero and is ratio)
Linked flag: FP-8, FP-5
