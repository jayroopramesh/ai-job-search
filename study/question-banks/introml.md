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

### QB-INTROML-0017 · [AUS] · pre-test (lazy learning) · deck 3 KNN p.24 · asked 2026-09-22
Q: KNN is called a **lazy learner**. Where does the computational work happen, and name one practical cost that follows from that.
A: There is **no explicit learning step** — building the model is fast because nothing is built; all the work is deferred to **prediction time**, where distances to every training record must be computed. Costs the deck lists: computationally expensive at prediction, scaling with dataset size *and* feature count; sensitive to the proximity measure and to unscaled data; redundant/irrelevant attributes cause problems; missing attributes are hard to handle. Contrast: eager learners do the work once during training. (His own margin note here: *"Prediction you do work → lazy learner → Don't prepare ahead of time. Other Alg, Prepare model during training"*.)
Asked: 2026-09-22 → answered 2026-09-23 ❌ (described what KNN computes and drifted to dimensionality; never reached "prediction time / no training step". **His own margin note on this slide has the answer** — annotation paradox, 4th instance)

### QB-INTROML-0018 · [AUS] · structural reading (curse of dimensionality) · deck 3 KNN p.22 · asked 2026-09-22
Q: The deck plots the ratio **(distance to the farthest point) / (distance to the nearest point)** as the number of features grows. Low dimensions: the ratio is large. High dimensions: it approaches **1**. Say what a ratio of 1 means for KNN's ability to do its job — no arithmetic, just read the quantity.
A: A ratio of 1 means the nearest and farthest points are **the same distance away** — every point is roughly equidistant, so "nearest" stops picking anything out. KNN's entire mechanism is ranking neighbours by distance, and at ratio 1 there is no ranking left to read: the distances no longer distinguish, so the k it selects are arbitrary rather than similar. Cause per the deck: volume grows exponentially with dimension, data becomes sparse, and "closeness" degrades. Deck's remedy: feature selection / dimensionality reduction (his margin note: *"with kNN feature Selection"*, *"samples become equidistant"*).
Asked: 2026-09-22 → answered 2026-09-23 🟡 (*"no difference between the neighbors close or far"* — the reading is right; the consequence for KNN's job, that the ranking then carries no information and the k chosen are arbitrary, was not stated)
Linked: pairs with FP-1 — both are the distance metric failing, once through **scale** and once through **dimension**.

### QB-INTROML-0019 · [AUS] · **formula-reading (the format that worked)** · deck 3 p.13–17 · asked 2026-09-23
Q: Given $d^2=(\text{age}_a-\text{age}_b)^2+(\text{income}_a-\text{income}_b)^2$ — point at the term that decides the neighbour ranking, and say why the other cannot compete.
A: The **income** term. Income differences run to tens of thousands while age differences run to tens, so the income term is orders of magnitude larger and dominates the sum; age contributes a rounding error to the ranking and is effectively invisible. Squaring widens the gap further but is not the cause — even Manhattan distance would be dominated. Fix: min-max scaling, or standardise to mean 0 / sd 1.
Asked: 2026-09-23 ✅ (*"Income decides, it's several magnitudes higher. Age is too small and will get drowned out without scaling."* — **first complete mechanism after four attempts**)
Linked flag: FP-1 (1/3) · note: this is the format to reuse for every mechanism from now on

### QB-INTROML-0020 · [AUS] · pre-test · deck 3 KNN p.19 · asked 2026-09-23
Q: KNN for **regression**: which steps are identical to classification, and which one changes?
A: **Identical:** compute the distance to every training record, then identify the k nearest neighbours. **Changed:** the aggregation step — instead of a majority vote over neighbour *labels*, take the **mean (or median)** of the neighbours' *target values*, and that average is the prediction. Everything upstream of the aggregation is the same algorithm; only how the neighbours are combined differs.
Asked: 2026-09-23 — standing (third of the three pre-tests withdrawn 09-21; the other two returned 09-22)

### QB-INTROML-0021 · [AUS] · contrast (lazy-learner re-frame) · deck 3 KNN p.24 · asked 2026-09-24
Q: A decision tree and a KNN classifier are both given the same 100,000-row training set. One takes a long time to *train* and is then fast at *prediction*; the other is the reverse. Which is which, and what is each one actually doing during its slow phase?
A: **Decision tree = eager.** Slow to train: it searches splits over the whole dataset up front and compiles a model. Prediction is then a handful of comparisons down the tree — near-instant. **KNN = lazy.** Training is instant because **there is no training step at all** — it just stores the data. The cost lands entirely at prediction, where it must compute the distance from the query point to every stored record and then rank them, which scales with both n and d. Deck's framing: "no explicit learning step; the work is done during the prediction phase."
Asked: 2026-09-24 — standing (re-frame after 09-23 ❌, where "where does the work happen" drew a description of what KNN computes)
Linked flag: FP-9


### QB-INTROML-0022 · [AUS] · **formula-reading** · deck 4 Decision Trees — "Measure of Impurity: GINI" · asked 2026-10-17
Q: $\text{Gini}(t) = 1 - \sum_j [p(j\mid t)]^2$, two-class form $2p(1-p)$. Without computing: which $p$ maximises it, which drives it to zero? Then — when the tree searches for a split, is it pushing this number up or down in the children, and why is that a good split?
A: **Max at $p=0.5$** (classes equally distributed — the deck's "least beneficial situation for classification"); **zero at $p=0$ or $p=1$** (all records one class — "most beneficial"). The tree pushes it **down**: it scores candidate splits by the weighted Gini of the children and picks the lowest. Low child impurity means each child is closer to a single class, so the path to a leaf resolves the label in fewer questions — the split has bought information.
Asked: 2026-10-17 — standing
Linked flag: FP-3 (1/3) · deliberately a different angle from the D2 pass: that one asked where the max sits, this one asks what the tree *does* with it

### QB-INTROML-0023 · [AUS] · **formula-reading + forced choice** · deck 6 Class Imbalance — "Alternative Measures" · asked 2026-10-17
Q: $P = \frac{TP}{TP+FP}$, $R = \frac{TP}{TP+FN}$. Same numerator. (a) Which denominator is "everything I flagged" and which is "everything that was actually there"? (b) Sepsis screen: a miss is catastrophic, a false alarm costs ten minutes. Which do you protect?
A: **(a)** $TP+FP$ = everything the model **flagged** (precision — of what I caught, how much was right). $TP+FN$ = everything that **was** positive (recall — of what was there, how much did I catch). The deck's pond: precision is how many of the fish caught are red; recall is how many of the red fish you caught. **(b) Protect recall.** $FN$ is the dead patient; $FP$ is ten minutes. You accept precision falling — more blue fish in the net — because the loss function is wildly asymmetric.
Asked: 2026-10-17 — standing
Linked flag: FP-4 (1/3)

### QB-INTROML-0024 · [AUS] · complete the sentence + mechanism · deck 5 Model Overfitting — "Reasons for Model Overfitting" · asked 2026-10-17
Q: "A model is overfitting when its training error is ______ and its test error is ______." Then: the deck gives **two** reasons. One is about the model. What is the other?
A: Training error **small**, test error **large** (model too complex). Underfitting is the mirror: too simple, **both** errors large. The two reasons: **high model complexity** and **not enough training data**. The second is the one that gets forgotten — if the training set is under-representative, test error rises while training error falls as you add nodes; doubling the data narrows the train/test gap at the same node count. So "overfitting" is not purely a property of the model, it is a relation between model capacity and how much data you have.
Asked: 2026-10-17 — standing

### QB-INTROML-0025 · [AUS] · contrast · deck 4 Decision Trees — "ID3 / CART" · first asked 2026-10-18 (banked, unasked)
Q: ID3 and CART both build trees but score candidate splits differently, and one of them can only build a particular shape of tree. Which is which?
A: **ID3** uses **information gain** (entropy-based) and allows **multi-way** splits. **CART** uses the **GINI index** and constructs **binary trees only** — every split is two-way. Both sit on Hunt's algorithm; what differs is the impurity measure and the branching factor.

### QB-INTROML-0026 · [AUS] · complete the sentence · deck 4 Decision Trees — "Stopping Criteria of Hunt's Algorithm" · first asked 2026-10-18 (banked, unasked)
Q: Hunt's algorithm stops splitting a node in two situations. One is obvious. The other is the awkward one — records that are **identical in every attribute** but **differ in class label**. What does the algorithm do there, and why can it not just keep splitting?
A: It **declares the node a leaf** and labels it with the **majority class** of the records at that node. It cannot split further because splitting requires an attribute test that separates the records, and by assumption no attribute distinguishes them — there is no question left to ask. This is irreducible error: the data itself cannot resolve the label, so the tree stops and accepts the majority.

### QB-INTROML-0027 · [AUS] · forced choice (direction) · deck 4 Decision Trees — "How should training records be split?" · first asked 2026-10-18 (banked, unasked)
Q: A continuous attribute can be split **binary** ($A < v$ vs $A \ge v$) or **multi-way** by discretising into ranges. Which is the more compute-intensive at training time, and what is the compensating advantage?
A: **Binary is the more compute-intensive** — the deck's point: it considers **all possible cut points** $v$ and finds the best one, so cost scales with the number of distinct values. The compensation is that the cut is chosen by the data rather than fixed in advance. Multi-way needs ranges decided up front (equal-interval bucketing, equal-frequency/percentiles, or clustering), which is cheap but bakes in a choice the data never got to make.

### QB-INTROML-0028 · [AUS] · **mechanism, interview-style** · deck 5 Model Overfitting — "Notes on Overfitting" · first asked 2026-10-18 (banked, unasked)
Q: The deck states flatly that "training error does not provide a good estimate of how well the tree will perform on previously unseen records." An interviewer asks: *why not — what exactly is training error measuring instead?*
A: Training error measures how well the tree has **memorised the records it was fitted on**, and the tree was built by searching splits **chosen to minimise exactly that number**. So it is scored on its own answer key: drive complexity up and training error can be pushed arbitrarily toward zero while the tree fits noise specific to that sample. What you actually need is **generalization error**, estimated either with a **validation set** held out of fitting, or by **incorporating model complexity** into the score so that extra nodes have to pay for themselves.

### QB-INTROML-0029 · [AUS] · forced choice (direction) · deck 5 Model Overfitting · first asked 2026-10-18 (banked, unasked)
Q: Two failing models. Model A: training error 2%, test error 30%. Model B: training error 28%, test error 31%. Which is overfitting, which is underfitting, and which one would **more training data** help most?
A: **A overfits** (small training error, large test error — too complex). **B underfits** (both errors large — too simple). **More data helps A**: the deck's experiment shows that doubling the instances narrows the train/test gap at a given number of nodes. More data does **little for B** — its problem is capacity, not sample size; a model too simple to capture the structure stays too simple with twice as much of it.

### QB-INTROML-0030 · [AUS] · **formula-reading** · deck 6 Class Imbalance — "F-measure" · first asked 2026-10-18 (banked, unasked)
Q: $F = \frac{2rp}{r+p}$, the harmonic mean of recall and precision. Why the **harmonic** mean rather than the ordinary average $\frac{r+p}{2}$? Read it off the expression.
A: The numerator carries the **product** $rp$, so if either term goes to zero the whole F goes to zero — the arithmetic mean would still read 0.5. That is the point: a model that flags **every** patient has recall 1 and precision near 0, and the ordinary average would reward it handsomely. The harmonic mean refuses to average away a disaster in one component; it sits close to the **smaller** of the two, so a good F requires both to be decent at once.

### QB-INTROML-0031 · [AUS] · **the trap** · deck 6 Class Imbalance — the 990/1000 worked example · first asked 2026-10-18 (banked, unasked)
Q: 1000 patients, 10 have the disease. A model predicts "healthy" for every single one. Its accuracy is **99%**. Without computing anything further: what are its recall and precision **on the disease class**, and what does this say about accuracy as a metric?
A: **Recall on the disease class = 0** (it caught none of the 10). **Precision is undefined** — it never made a positive prediction, so the denominator $TP+FP$ is zero. Accuracy is 99% because it is dominated by the 990 negatives it got right for free. Under class imbalance, **accuracy measures the majority class and little else** — which is precisely why the deck introduces precision, recall, F-measure and ROC as "alternative measures".

### QB-INTROML-0032 · [AUS] · identify-the-point · deck 6 Class Imbalance — "ROC Curve" · first asked 2026-10-18 (banked, unasked)
Q: The ROC plane plots **TPR against FPR**. Name what sits at each of these: **(0,0)**, **(1,1)**, **(1,0)**, and the **diagonal**.
A: **(0,0)** — declare everything **negative** (catch nothing, raise no alarms). **(1,1)** — declare everything **positive** (catch everything, alarm on everyone). **(1,0)** — the **ideal**: every positive caught, no false alarms. **The diagonal** — **random guessing**; a model on that line carries no information, and anything below it is worse than a coin.

### QB-INTROML-0033 · [AUS] · mechanism · deck 6 Class Imbalance — "ROC Curve" · first asked 2026-10-18 (banked, unasked)
Q: The deck says a classifier that returns **only the predicted class** gives a **single point** in ROC space, and that to draw a *curve* the classifier must produce **continuous-valued output**. Why — where does the curve actually come from?
A: The curve is swept out by **varying the decision threshold**. A continuous score (a probability, a distance) can be cut at any threshold, and each threshold yields a different (FPR, TPR) pair — lower the bar and both rise together. A hard class label has already had the threshold applied and thrown the score away, so there is nothing left to vary: one model, one operating point. **The ROC curve is a picture of one model at every threshold**, not of many models.

### QB-INTROML-0034 · [AUS] · say-it-precisely · deck 6 Class Imbalance — "AUC" · first asked 2026-10-18 (banked, unasked)
Q: AUC = 0.7. Complete the deck's own sentence: "there is a 70% chance that the model will ______". The precise wording matters here — it is a very easy one to say loosely in an oral.
A: "...a 70% chance that the model will be able to **distinguish between the positive class and the negative class**." Said properly: given one random positive and one random negative, there is a 70% chance the model **scores the positive higher**. It is **not** "70% accurate" and **not** "70% of predictions are right" — AUC is about **ranking**, and it is threshold-free, which is exactly why it survives class imbalance where accuracy does not.

### QB-INTROML-0035 · [AUS] · odd-one-out · decks 4–6 · first asked 2026-10-18 (banked, unasked)
Q: Four things a tree-builder might do: **(1)** pick the split with the lowest weighted child Gini · **(2)** stop splitting when a node is pure · **(3)** keep splitting until every leaf holds one record · **(4)** hold out a validation set to estimate generalization error. Which is the odd one out, and why?
A: **(3).** The other three are the algorithm working as intended; (3) is the definition of **overfitting** — a tree grown until it has memorised each record individually has driven training error to zero and learned the noise. It is also what **early stopping criteria** and **model selection** exist to prevent.

### QB-INTROML-0036 · [AUS] · **interview-style, follow-up chain** · decks 5–6 · first asked 2026-10-18 (banked, unasked)
Q: *"You've built a classifier for a rare condition and it reports 97% accuracy. Walk me through what you'd check before believing it."* Then the follow-up you should expect: *"Suppose precision is high and recall is poor — what do you change?"*
A: **First:** the base rate. If the condition occurs in 3% of cases, 97% accuracy is exactly what predicting "no" every time achieves — so look at the **confusion matrix**, not the headline, and read **precision and recall on the minority class**. Then **F-measure** for a single number that cannot be gamed by one component, and **ROC/AUC** for threshold-free ranking quality. **Follow-up:** high precision, poor recall means the model is **too conservative** — when it flags, it is right, but it is flagging too little. **Lower the decision threshold** (move up the ROC curve, accepting more FP), and address the imbalance itself in training. Say the direction out loud: you are trading precision away to buy recall, and that trade is only correct because a miss costs more than a false alarm.
