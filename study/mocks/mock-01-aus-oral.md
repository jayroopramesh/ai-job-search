# Mock #1 — [AUS] IntroML oral dress rehearsal

**Built 2026-11-10 (D55), unattended. Ready to run on "go".**
Target date: Wed 11 Nov · Real interview: Mon 16 Nov (CMP 466, Salam Dhou, AUS)

## Protocol
- **10 items · ~8 minutes · cold · timed · scored /100.**
- **Cold means cold:** no warm-up, no teaching, no hints before the clock starts. Do not post this into a queue (§TUTOR "mocks are never queued"). It is run in one sitting or not at all.
- **AUS only.** This is a dress rehearsal for a specific oral, not the mixed weekly. The DL4H equivalent is `mock-02-dl4h-oral.md`, for 13 Nov.
- **No arithmetic** — oral conditions. Every item is structural, directional, or a mechanism demand.
- Each item is a question **plus one follow-up probe**, because that is how an oral actually runs: the probe is where the grade is decided.
- Ask them **in order**. Do not skip ahead if he stalls — say "park it, moving on" and return at the end if time allows.
- Read the clock aloud at item 5 ("halfway, four minutes"). That pressure is the entire point of the exercise.

## Scoring — 10 points per item
| Score | Meaning |
|---|---|
| **10** | Main answer correct **and** the probe answered with the mechanism, unprompted. |
| **6** | Main answer correct, probe produced a label or a restatement rather than a mechanism. **This is FP-9 and it is the dominant failure — expect it.** |
| **3** | Partially correct, or correct only after the probe did the work for him. |
| **0** | Wrong, inverted, or not answered. |

Log the total, and log **how many 6s** separately: the 6-count is the direct FP-9 reading and the single most useful number this mock produces.

---

## The items

**1. Training error.** Your tree gets steadily better on the training set as you add nodes. Why is that not evidence it is getting better?
*Probe:* What is the training error actually measuring at that point?
<sub>`05_Model_Overfitting` — "Training error does not provide a good estimate of how well the tree will perform on previously unseen records"</sub>

**2. Overfitting, as a direction.** Too complex: training error does what, test error does what? Now the other end — too simple, same two.
*Probe:* Which of the two errors can you actually see while training, and what does that imply about how you'd ever detect the problem?
<sub>`05_Model_Overfitting` — "Overfitting: when model is too complex, training error is small but test error is large"</sub>

**3. Cross-validation.** You have one dataset. Why is k-fold preferred over a single holdout split?
*Probe:* What is the cost of k-fold, and what specifically does averaging over the folds buy you?
<sub>`05_Model_Overfitting` — "Holdout" / "Random subsampling: repeated holdout" / "Cross-validation"</sub>

**4. ROC axes.** What two quantities are on the axes of an ROC curve?
*Probe:* Top-left corner — what kind of classifier sits there? And the diagonal?
<sub>`06_Class_Imbalance_Evaluation` — "ROC (Receiver Operating Characteristic)" / "ROC curve plots TPR against FPR"</sub>

**5. Why a point, not a curve.** A classifier that outputs only a hard label gives you a single point on the ROC plot, not a curve. Why?
*Probe:* What do you need the model to produce instead, and what are you varying to trace the curve out?
<sub>`06_Class_Imbalance_Evaluation` — "To draw ROC curve, classifier must produce continuous-valued output"</sub>

**6. F-measure.** F combines precision and recall as a *harmonic* mean, not an ordinary average. What does that choice do?
*Probe:* Model A has precision 1.0 and recall near zero. What does the ordinary average say, what does F say, and which is telling the truth?
<sub>`06_Class_Imbalance_Evaluation` — "F-measure (F)"</sub>

**7. Gradient descent, as a direction.** The update subtracts the gradient. Why **minus**?
*Probe:* What would the plus sign train the model to do, and what happens to the loss?
<sub>FP-5 territory — directional inversion, his known weak axis, deliberately placed mid-mock</sub>

**8. K-means stopping.** K-means minimises SSE — the sum over clusters of squared distances from each point to its centroid. Why is it guaranteed to stop?
*Probe:* Stopping and finding the *best* clustering are not the same thing. Which one does it guarantee?
<sub>`13/14 Cluster Analysis` — "A common objective function (used with Euclidean distance measure) is Sum of Squared Error (SSE)"</sub>

**9. DBSCAN.** Define core, border and noise points by the rule, not by the picture.
*Probe:* Name something DBSCAN can do that K-means structurally cannot.
<sub>`15_Cluster_Analysis_III` — "A point is a core point if it has at least MinPts within Eps" / "border point" / "noise point or outlier"</sub>

**10. Curse of dimensionality.** Add hundreds of features and KNN degrades. What happens to the *distances* themselves?
*Probe:* Given that, what does "nearest neighbour" come to mean in high dimensions?
<sub>`03_KNN` — "k-NN suffers from the curse of dimensionality because the notion of 'closeness' between data points degrades in high dimensions"</sub>

---

## Model answers — for instant grading, do not read aloud before scoring

1. Training error falls monotonically with capacity because the model is memorising the sample it is scored on; it measures **fit to the data already seen**, not generalisation. Full marks need "memorising"/"fitting noise", not just "it overfits".
2. Complex → training low, test high. Simple → both high (underfitting). **Only training error is visible**, which is why a held-out set is not optional — the failure is invisible in the quantity you are optimising.
3. Every record serves as both train and test across folds, so the estimate uses all the data and is far less sensitive to one unlucky split; averaging reduces the **variance of the estimate**. Cost: k trainings.
4. y = TPR (recall), x = FPR. Top-left = all positives caught, no false alarms — perfect. Diagonal = random guessing.
5. A hard label fixes one (TPR, FPR) pair. You need **continuous scores**, then sweep the **threshold** to trace the curve.
6. Harmonic mean is dominated by the **smaller** of the two — it punishes imbalance. Ordinary average gives ~0.5 and flatters a useless model; F stays near zero. **F is telling the truth.**
7. The gradient points **uphill**; minus goes downhill, toward lower loss. Plus performs gradient *ascent* and maximises the loss — it diverges.
8. Each step (assign, then recompute centroids) can only reduce or hold SSE, and there are finitely many assignments, so it must terminate. It guarantees **a local optimum, not the global one** — hence the dependence on initialisation.
9. Core: ≥ MinPts points within Eps (counting itself). Border: not core, but inside a core point's neighbourhood. Noise: neither. DBSCAN finds **arbitrarily shaped clusters and labels outliers as noise**; K-means assigns every point to some cluster and leans toward round ones.
10. Distances **concentrate** — nearest and farthest neighbours become nearly equidistant, so the contrast that ranking depends on collapses. "Nearest neighbour" stops being meaningfully nearer than anything else.

## Result
*(unrun — record total /100, the 6-count, and per-item scores here)*
