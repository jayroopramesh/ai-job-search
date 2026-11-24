# Anchors — CV

**For the [OXFORD] Computer Vision oral, Fri 25 Dec (unconfirmed — it is Christmas Day).**
Built 2026-11-24 (D69), a month ahead, because the thing this campaign gets wrong most reliably is writing the artefact on the day it is needed instead of before it.

**What the evidence here is, stated plainly — this sheet is stronger than the DL4H one and weaker than the AUS one.**
The **flags are measured**: all nine come from answers you actually gave in IntroML and DL4H. The **handles are new**: each is a picture or formula from your own CV decks, chosen because it attacks a flag from an angle that course has never used. So the diagnosis is evidence; the delivery is mined, not tested. **Which flags this sheet covers, listed rather than counted** — so you can check it instead of trusting a total. **Covered:** FP-9, FP-1, FP-2, FP-4, FP-5, FP-6, FP-7. **Deliberately not covered:** FP-3 (GINI impurity extremes) and FP-8 (attribute-type taxonomy) — both IntroML-only, that assessment is past, and inventing CV versions would be padding.

Everything below is cited to a deck you have. Where the lecturer makes the link himself, it says so — that upgrades an answer from *true* to *examinable*.

---

## The one that matters most

**FP-9 — you stop at the label and leave out the mechanism.** It fired on **5 of 5** clinic items. Pressed for a mechanism you tend to give the *remedy* instead of the *failure*.

**The habit, and it is the whole sheet in one line:** *after you name the thing, say one more sentence starting with "because."*

**And CV hands you the best version of this you will ever get.** `09_VisualizationUnderstanding` opens with **Clever Hans** — the horse that appeared to do arithmetic and was in fact reading involuntary cues from its trainer, *who did not know he was giving them.* The next slide shows a horse classifier scoring high on PASCAL VOC whose heatmap lights up a **copyright watermark**.

> **Say it like this:** *"The held-out set is drawn from the same distribution as training, so the watermark is in the test images too — the shortcut scores exactly as well as the real mechanism. A number without a mechanism is Clever Hans."*

That sentence is your own dominant failure, stated about a model. If you remember one thing from this page, remember that you are the horse's trainer: **the accuracy was real and the explanation was wrong.**

---

## The two answers you can reuse on almost anything

**1. The aliasing chain — and the lecturer builds it himself.** `03_FourierTransforms` opens *"Observation 1 — From lecture 02: down-sampling leads to aliasing."* So this is his link, not your construction:

> **02** states the constraint (sampling theorem) · **03** supplies the tool (**convolution theorem**, `ℱ{f ∗ g} = ℱ{f}·ℱ{g}` — *a blur **is** a low-pass; multiplying the spectrum by a mask and convolving with a blur are two descriptions of one operation*) · **07** performs it as **stride** · **08** performs it again as **ViT patching**.
> **Say it like this:** *"One constraint, one tool, two silent applications. Stride > 1 is subsampling, and subsampling without a low-pass first is aliasing."*

And `04_Restoration` is where the chain hits its limit: the degradation model is `g = f ∗ h + n`, so by the convolution theorem restoration looks like dividing spectra — **except dividing by `ℱ{h}` divides the noise by something near zero exactly where the blur destroyed the signal.** *03 says a blur is a low-pass; 04 says that is why you cannot simply invert one.*

**2. The metric-choice family.** Accuracy → precision/recall → Dice → IoU → FID. **Every one of them exists because the previous one could not see something.**

> **Say it like this:** *"Pick the metric by what it is blind to."* Accuracy is blind to class imbalance · precision/recall split the two ways of being wrong · Dice survives imbalance but **IoU is size-biased** (`11`'s own warning: *"favourable to large objects"*, since a fixed boundary error costs a far bigger fraction of a small lesion) · FID exists because **a GAN gives you a sampler, not a density**, so there is no `p(x)` to score.

Being able to say what a metric **cannot** see is the answer that scores. Naming metrics is not.

---

## Directions — get the arrow right

**FP-5 (directional inversion, reset to 0/3) and FP-1 (unscaled features, 1/3 — your best flag).**

**FP-1's CV handle is `06_Classification`'s own toy embedding**: count the blue pixels, count the green pixels, classify by nearest neighbour in that 2-D space. Both axes are pixel counts, so they share a scale — *until you put image width on one of them.*

> **Say it like this:** *"The width axis has a far larger numeric range, so its squared difference dominates the sum `(x₁−y₁)² + (x₂−y₂)²`, and the neighbour ranking is decided by image size. The blue-pixel evidence is drowned out. Scale the features so each contributes comparably."*

**You have already produced this, unprompted, in IntroML:** *"income decides, it's several magnitudes higher, age gets drowned out without scaling."* That is a complete mechanism. **It is the same sentence here with different nouns** — do not re-derive it, reuse it.

**For FP-5, the arrows worth having straight:** subsample without a low-pass → **aliasing** (not the reverse) · heavy-tailed noise → **L1**, because a heavy tail means tolerance · impurity goes **down** in the children · small object → Dice/IoU go **down** for a fixed boundary error.

---

## Direction or magnitude — which one should decide

**FP-2 (cosine vs Euclidean, 0/3).** In IntroML this was about **text documents**. CV gives you the same thing back, and the deck makes the link itself.

`05_MatchingIndexingSearch` builds **Bag of Visual Words**: SIFT features over a big dataset, K-means them into `K` classes, then describe an image by a **histogram of which classes it contains**. The deck then says, in its own words:

> *"When computing the histogram, it does not matter where each feature comes from in the image. **This is similar to classic text-based retrieval systems: count how often each word appears in a document.** Documents on similar topics have similar statistics."* And: *"with large `K` the image descriptor is usually **sparse** (most entries are 0)."*

**So this is not an analogy you are drawing — it is his.** That matters: it makes the transfer examinable rather than merely true.

> **Say it like this:** *"A heavily-textured photo yields more keypoints, so its histogram counts are larger across the board. Under Euclidean distance that makes **how textured the image is** decide retrieval — the same way document **length** would. Cosine compares direction only: the mix of visual words, with magnitude normalised away. And since the vectors are sparse, two images sharing a zero is not evidence they are alike — the dot product only sums over words that actually co-occur, so cosine scores agreement on what is **present**."*

**The one-line version:** *Euclidean lets size decide; cosine asks only about the mix.* Pick by whether magnitude is information or nuisance.

---

## Denominators — say the formula, not the name

**FP-4 (precision ↔ recall, 1/3).** You have swapped these three times. **Stop naming them and say the denominator.**

> **Precision = TP/(TP+FP)** — denominator is *everything I flagged.*
> **Recall = TP/(TP+FN)** — denominator is *everything that was really there.*

**CV gives you two handles, and the second one is why this is worth real care.**

**The sharp one:** on always-predict-0 with 90% class 0, recall on class 1 is **0**, and precision is **0/0 — undefined**. *You cannot be wrong about predictions you never make.*

**The one with stakes:** `20_EthicsPrivacy` runs the **COMPAS** case — recidivism scores that influenced sentences in four states — and then recaps the confusion matrix on the next slide. **So precision and recall turn up deciding bail.** A false positive here is a person punished for a crime they were never going to commit.

> **And the question most likely to be asked:** ProPublica found unequal error rates; the vendor replied the scores were *calibrated*. **Both were true.** Say it like this: *"Those are different fairness criteria, and when base rates differ they cannot both hold. Calibration fixes what a score means; equal false-positive rates fix who bears the cost of being wrong. So 'is this fair' has no answer until you say which definition — and that choice is about who absorbs the error, not a hyperparameter."*

Naming the wrong denominator here does not cost a mark. **It gets the ethics of the case backwards.**

---

## The loss one — and you now know it from both sides

**FP-6 (losses encode noise models, 0/3).** The first handle was the derivative. The better one is a picture, and the third is the one that proves you understand it.

**The picture** (`18_Unsupervised`, under its own heading *"Inherent Ambiguity"*): colorization predictions come out washed-out. A grey car could have been red *or* blue, so the ground-truth colour is **one sample from a multimodal distribution**; squared error is minimised by the **conditional mean**; averaging red and blue gives desaturated grey-brown.

> *"L2 assumes a single-peaked target. When the truth is multimodal, minimising it returns the average of the modes, which can be a value that is never correct. So a model that is right about the distribution scores badly, and the fix is the loss, not the network."*

**Now the other side, and this is the item that separates memorising from understanding.** `16_GenerativeModels` trains diffusion with what the deck calls a **"simple L2 loss"**. That looks like a flat contradiction.

> **Say it like this:** *"The diffusion target is the specific noise that was actually added — one known value, not an ambiguous one — so the conditional mean **is** the right answer. The multimodality lives in the iteration, not the loss. So the rule was never 'L2 is bad': it is 'L2 returns the conditional mean, which is correct precisely when the target is single-peaked.' Diffusion engineered its target to be single-peaked; colorization did not."*

**Same principle, opposite verdict.** If you can say that, FP-6 is not a weakness any more.

---

## Two more worth having from `05`

**Equivariance → invariance, and you can now name both routes.** SIFT edge directions are *"invariant to brightness changes, **equivariant** to rotation"* — and the next step is *"rotate all edges so that the global orientation is 'up'."*

> **Say it like this:** *"Equivariant means rotate the image and the descriptor rotates correspondingly — predictable, not unchanged. Aligning every patch to its own dominant orientation turns that equivariance into **invariance** by **canonicalisation**. Global average pooling reaches the same place by the opposite route: it averages the equivariant thing away instead of aligning it first."*

**And why appearance distance is never enough.** Matching takes the lowest Euclidean distance and the top N — then does **geometric verification** against a homography.

> **Say it like this:** *"A descriptor sees one local patch, and real scenes repeat — windows, bricks, leaves — so the nearest descriptor can be the wrong instance of a correct-looking pattern, with a genuinely small distance. **A better descriptor cannot fix that**, because the ambiguity is in the image, not the descriptor. Geometric verification adds a global constraint: the right matches all agree on one transformation and the wrong ones have no reason to agree. It is evidence of a different kind, not more of the same."*

*Note the shape — it is Clever Hans again. Every individual number was fine and the mechanism was still wrong, and the fix was an independent check rather than a better score.*

---

## Naming versus mechanism

**FP-7 (adjacent-concept substitution, 1/3)** — reaching for the neighbouring concept's name.

Two CV items are built as bait for it, so expect them:
- **`08_Transformers`, q/K/V.** Naming the three is not the answer. *Query and key share a dimension **because they are compared**; value's dimension is free **because it is only mixed**.* The asymmetry is the answer.
- **"Learned beats hand-designed."** `17_RepresentationLearning` says the honest version: *fusing hand-designed factors is itself a comparably complex representation problem.* So **hand-design relocated the hard part rather than removing it, and learning wins because it learns the fusion.** And know when SIFT is still right — a classic tool's guarantees beat a vague preference for learning.

---

## If you read nothing else

1. **After you name it, say one more sentence starting with "because."** That single habit is the biggest gap between what you know and what you score.
2. **A number without a mechanism is Clever Hans.** The held-out set contains the shortcut too.
3. **Say the denominator, not the name.** Precision = what I flagged. Recall = what was there.
4. **L2 returns the conditional mean** — right when the target is single-peaked, wrong when it is not. Change the loss, not the network.
5. **Stride is subsampling, and subsampling without a low-pass is aliasing.** One constraint, one tool, two silent applications.
6. **Euclidean lets size decide; cosine asks only about the mix.** Bag of Visual Words *is* text retrieval — the deck says so itself.

**And in the room:** take a breath before answering — a pause reads as thinking, not blanking. Say what you would **do** rather than guessing a name. Give the half you know and name which half; examiners listen for whether you know where your own edges are.
