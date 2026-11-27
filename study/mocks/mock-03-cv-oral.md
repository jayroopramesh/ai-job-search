# Mock #3 — [OXFORD] Computer Vision oral dress rehearsal

**Built 2026-11-27 (D72), unattended — 16 days before its own build-by date of 13 Dec, and 25 before the assessment.**
Target: post self-timed ~22 Dec · Assessment: Fri 25 Dec (**unconfirmed — it is Christmas Day; asked 16 and 20 Nov, no reply**)

**Why it exists this early.** Mock #1 was discussed across nine Saturdays and never written; Mocks #1 and #2 were both withdrawn unrun once their assessments passed. The lesson taken was *build early*, and the lesson taken after that was that **building early and delivering early are different decisions** — so this is written now and **held for ~22 Dec**.

## Protocol
**10 items · ~8 minutes · cold · timed · scored /100**, each item plus one follow-up probe. Read the clock aloud at item 5. **No arithmetic anywhere** — the oral will not ask for calculation, so neither does this.

**Honour system, stated plainly when posted:** set a timer, look nothing up, short answers, *write "pass" and move on if you blank — that is real information and costs you nothing*, stop at 8 minutes even if unfinished. **Nobody times it but you, so the score is softer evidence than a supervised sitting.** What it keeps: the items are genuinely cold, and it yields a score plus a per-item reading.

**Cold-set discipline — this is the whole value.** Avoids every CV item already served: **QB-CV-0007, 0008, 0020, 0029, 0031, 0042** (the unscaled-axis embedding, undefined precision, which-domain-to-convolve, the COMPAS impossibility, Clever Hans, and the horse-heatmap picture). Drawn instead from the 36 unserved items.

**One honest caveat about "cold".** Item 9 is a different question from the served QB-CV-0029, but it uses **the same COMPAS case**, so he arrives with the setup already in mind. That is not a flaw — it is closer to how an oral actually runs, where one case carries several questions — but **a pass on item 9 is weaker evidence than a pass on the other nine**, for the same reason two items sharing an answer are one measurement rather than two. Score it, note it, do not count it as an independent reading of FP-9 alongside a Clever Hans pass.

**Every formula below is ✅ verified against the real PDFs** (26–27 Nov), after four of nine attributions turned out to carry a wrong symbol. Nothing here is quoted from the lossy cache.

## Scoring — 10 points per item
| Score | Meaning |
|---|---|
| **10** | Main answer correct **and** probe answered with the mechanism, unprompted. |
| **6** | Main correct, probe gave a label or a restatement. **FP-9. Expect it; count them.** |
| **3** | Partial, or correct only once the probe had done the work. |
| **0** | Wrong, inverted, or unanswered. |

Log the total **and the 6-count** separately. *The 6-count is the direct reading on FP-9, which has fired on 5 of 5 clinic items and is the dominant flag.*

---

## The items

**1. One operation, four names.** `03` opens by pointing back: *"From lecture 02: down-sampling leads to aliasing."* Tell the chain across the course in four steps, naming which deck supplies each.
*Probe:* Which single step is the one people skip, and what goes wrong when they do?

**2. What "remove the frequencies" actually means.** The convolution theorem is `ℱ{f ∗ g} = ℱ{f} ℱ{g}`. Deck 02 says: before subsampling, remove everything above half the new sampling rate. Say mechanically what *remove* means here.
*Probe:* So why is a blur the right tool — what is the connection?

**3. Where the chain hits its limit.** The degradation model is `g = f ∗ d + n`, with `d` the point spread function. By the theorem, restoration looks like dividing spectra.
*Probe:* That is a trap. Say precisely why.

**4. Size or mix.** Bag of Visual Words describes an image by a histogram of visual-word counts, and `05` says outright that this is *"similar to classic text-based retrieval systems."* A heavily-textured photo yields far more keypoints. Under Euclidean distance, what ends up deciding retrieval?
*Probe:* What does cosine remove from the decision, and why does the vectors' **sparsity** strengthen the argument?

**5. Both verdicts are right.** Colorisation under squared error comes out washed-out, and the deck calls that *inherent ambiguity*. Diffusion trains with what its deck calls a *"simple L2 loss"*. Both are true.
*Probe:* Resolve it in one sentence that works for both.

— *clock check: you should be around 4 minutes* —

**6. What a metric cannot see.** `11` warns that IoU is *"favourable to large objects."* A model segments a small tumour and scores badly.
*Probe:* Before concluding the model is bad, what else could that score mean — and what does that imply about choosing a metric at all?

**7. Forced or free.** Attention uses a query, a key and a value function. Your slide writes all three as `ℝ^d → ℝ^d`; the original Transformer gives the value its own width.
*Probe:* One of those dimension choices is forced and one is free. Which, and what forces it?

**8. Two routes to the same place.** SIFT edge directions are *equivariant* to rotation, and the next step rotates every patch so its dominant orientation points up.
*Probe:* Name the DL4H operation that reaches invariance by the opposite route, and say how the two differ.

**9. Not an alibi.** A model is accused of racial bias; the defence is *"it isn't biased, it just learns from the data."*
*Probe:* "The data is biased" is a label, not a mechanism. Give the mechanism.

**10. Evidence of a different kind.** Matching takes the lowest descriptor distance and the top N, then runs **geometric verification** against a homography.
*Probe:* Could a better descriptor remove the need for it? Answer yes or no and say why.

---

## Model answers — for instant grading; do not read before scoring

1. **02** states the constraint (sampling theorem) · **03** supplies the tool (convolution theorem — a blur *is* a low-pass) · **07** performs it as **stride** · **08** again as **ViT patching**. *Probe:* the low-pass **before** subsampling. Skip it and high frequencies fold down into low ones — aliasing — and the detail is not recoverable afterwards.
2. Multiply the spectrum by a mask that is 1 below the cutoff and 0 above: the unwanted frequencies are **multiplied by zero**, deleted rather than hidden. *Probe:* by the theorem, multiplying the spectrum by a low-pass mask **is** convolving the image with that mask's inverse transform — and that kernel is a blur. One operation, two descriptions.
3. *Probe:* dividing by `ℱ{d}` divides the **noise** by it too — and `ℱ{d}` is near zero at high frequencies, precisely where the blur destroyed the signal. Naive inverse filtering returns amplified noise.
4. **How textured the image is** — the total count — exactly as document *length* would in text retrieval. *Probe:* cosine compares **direction only**, the mix of words, normalising magnitude away. Sparsity: most entries are zero, and **two images sharing a zero is not evidence they are alike**; the dot product only sums over words that co-occur.
5. *Probe:* **"L2 returns the conditional mean, which is correct exactly when the target is single-peaked."** Colorisation's target is multimodal (the grey car could have been red or blue), so the mean is a colour nobody would choose. Diffusion's target is the specific noise actually added — one known value — so the mean is right, and the multimodality lives in the iteration.
6. The score may reflect the **object's size** rather than the model: a fixed boundary error costs a far larger fraction of a small lesion, perimeter-to-area scaling against you. *Probe:* every metric is blind to something — accuracy to imbalance, Dice less so, IoU to scale, FID needs Inception features because a GAN has no density. **Pick the metric by what it cannot see.**
7. *Probe:* **query and key are forced** to share a width — their dot product is the relevance score and a dot product needs equal lengths. **The value is free**: it is never compared, only weighted and summed, so its width just sets the output width. Collapsing all three to `d` satisfies the constraint and picks a legal value for the free one.
8. Rotating each patch to a canonical orientation converts **equivariance into invariance** by **canonicalisation**. *Probe:* **global average pooling** — it averages the equivariant thing away instead of aligning it first. Same destination, opposite route.
9. *Probe:* **the label is a measurement, not the truth.** "Recidivism" in the data means *re-arrested*, which records policing as much as offending, so a more heavily policed group generates more positive labels at the same underlying rate. The model faithfully reproduces the **measurement process** — and fidelity to a biased measurement is how a statistically correct model produces unjust decisions.
10. *Probe:* **No.** The ambiguity is in the **image**, not the descriptor — repeated structure (windows, bricks, leaves) really does look the same, so the nearest descriptor can be the wrong instance with a genuinely small distance. Geometric verification adds a **global constraint**: correct matches agree on one transformation, wrong ones have no reason to. **Evidence of a different kind, not more of the same.**

---

## Result
Run on: — · Score: — /100 · 6-count (FP-9): — · Items passed: —

**Grading note.** Items 4, 5, 7 and 9 re-attack measured flags (FP-2, FP-6, FP-7-adjacent, FP-9). **Grade those against the flag, not as generic CV.** A 6 on any of them is the flag firing again in a fourth course.
