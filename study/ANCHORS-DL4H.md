# Anchors — DL4H · [OXFORD]

**Four minutes. Built 2026-11-12 (D57).** Companion to `ANCHORS.md`.
For the night before DL4H (20 Nov) — or for Monday, if Monday turns out to be the Oxford one.

> ⚠️ **Read this caveat, it changes how much to trust the sheet.** `ANCHORS.md` is built from **errors you actually made** — nine flags, measured. This sheet mostly isn't, because only **one** of those nine flags is DL4H-specific (the loss/noise-model one). So these are not your measured weak points; they are **the things most likely to be asked and most likely to come out as a label instead of a mechanism**, drawn from the decks and problem sheets. Weaker evidence, honestly flagged. The one measured item is marked ✅MEASURED.
>
> Related and worth knowing: **30 of the 39 DL4H questions I've prepared have never been put to you.** *(Corrected 13 Nov — I wrote 32 here yesterday, from glancing at a truncated search result instead of counting. The real number is 30.)* DL4H is the course with the most material ready and the least of it delivered.

---

## The habit, same as the other sheet

**After you name the thing, say one more sentence starting with "because".**
This is the whole game in an oral. Namburete works in medical imaging — so there's a second half to it here: **carry the method back to the hospital.** An answer that is correct about deep learning and silent about clinical data is a half answer. Say what it does to *a model trained on scans from one hospital*.

---

## Losses and directions

**✅MEASURED — L1 vs L2, and the tails.** You once wrote that L1 penalises outliers *extra*. It penalises them **less**, which is exactly why it's the robust one.
> **Say it via the derivative:** `d(e²)/de = 2e` — pull grows with the residual. `d|e|/de = ±1` — pull is flat. So one far-out point drags an L2 fit much further.
> **Anchor: heavy tail = tolerant.** Laplace/L1 expects big residuals and shrugs; Gaussian/L2 treats a big residual as near-impossible and contorts to kill it.

**Dice vs accuracy under imbalance.** A tumour is a tiny fraction of the voxels.
> Accuracy and pixel-wise cross-entropy are dominated by background — predicting "all background" scores superbly and segments nothing. **Dice measures overlap on the positive class**, so background isn't in the numerator and can't game it.

---

## Depth and gradients

**Vanishing gradients, and what the identity does.** `∂L/∂h₁ = ∂L/∂hₙ · Π ∂h_{k+1}/∂h_k` — the gradient reaching an early layer is everything downstream *multiplied together*. Factors below 1 ⇒ the product collapses ⇒ early layers stop learning.
> **Residual block:** `h_{l+1} = h_l + f(h_l)`, so `∂h_{l+1}/∂h_l = I + ∂f/∂h_l`. **The `I` keeps a term of size 1 in every factor**, so the product can't vanish through the shortcut. Unravelled, the output is the input plus a sum of shallower networks — that picture *is* the same fact.

**Why not initialise the weights to zero.**
> Every unit computes the same output, gets the same gradient, updates identically — they stay identical forever and the layer has the capacity of **one** unit. The thing you failed to do is **break symmetry**.

**Scaling inside attention — the `1/√d_k`.**
> Without it, the dot products grow with `d_k`, the softmax **saturates** onto one key, and a saturated softmax has **near-zero gradient** — so attention stops learning. Dividing by `√d_k` keeps the logits in the range where the softmax still has a usable slope. *(Magnitude → saturation → dead gradient is the same through-line as the KNN scaling story. Same shape, different setting.)*

**BatchNorm's γ and β.** Normalising to zero-mean/unit-variance throws away scale and shift the layer might need.
> **γ and β let the network learn its way back** to any mean and variance, so normalisation costs it no expressiveness. **The catch:** the original "internal covariate shift" explanation is not settled — the benefit is better attributed to a smoother loss landscape. Say that; it's the kind of thing an examiner is listening for.

**Gradient reversal.** Identity on the forward pass, `−λI` on the backward.
> The feature extractor is pushed **away** from hospital-identifying features — the domain classifier tries to identify the site, and the reversed gradient trains the features to defeat it. **Flip the sign and you'd train the features to be maximally site-identifying**, which is the opposite of what you want.

---

## Regularisation and low data

**Dropout.** Train: randomly zero units, so no feature can lean on a fixed partner. Test: dropout off, full network, activations scaled so expected magnitudes match.
> **It's implicit ensembling with shared parameters** — exponentially many thinned sub-networks, one set of weights. "Implicit" because you get the ensemble benefit without training or running many models, which is infeasible in real time.

**Transfer learning on 300 scans.** Photographs look nothing like MRI, and it still works.
> Early layers learn **generic** low-level structure — edges, textures, gradients — which is modality-agnostic and transfers. Later layers encode **dataset-specific semantics** and transfer poorly, so those are what you fine-tune or replace. **Generic-to-specific along depth** is the whole asymmetry.

**Weight sharing in a conv layer.** Not just "fewer parameters".
> **Translation equivariance** — a feature worth detecting is worth detecting anywhere, so every location becomes a training example for the same filter. The deck's phrasing: it is unnecessary for every receptive field to have its own "left ventricle" detector. **It stops being true when position itself carries meaning** — registered images with fixed anatomy, where a location-specific model could legitimately do better.

**Augmentation — the clinical trap.** Safe: small rotations, elastic deformation, intensity jitter, noise, cropping.
> **Never horizontal flip.** Anatomy is laterally asymmetric — situs, cardiac position, left/right organ identity — so flipping teaches the model that a mirrored anatomy is a legitimate sample and destroys exactly the laterality a clinician depends on. Harmless on photographs, wrong here. **Say the mechanism, not "it's wrong".**

---

## Deployment, privacy, trust

**Federated learning.** Hospitals cannot pool data.
> **Model updates move — weights or gradients. The data never leave the hospital.** That solves privacy and the legal barrier.
> **The second word is doing work:** the data are decentralised *and heterogeneous*. Sites are **non-IID** — different scanners, protocols, populations — so naive averaging of updates can degrade or fail to converge. **That is a statistical problem, not a privacy one, and private transport does nothing about it.** Separating those two is the answer that scores.

**Explainability.** A saliency map lights up over the right region.
> That shows **where the gradient is large, not why the decision was made.** It can highlight the right region while the model keys on a confound — a scanner artefact, a marker, a burned-in label correlated with the site. Concrete limitation: **noisy gradients.** Broader caution: **not all explanations are faithful** — an explanation can look right and still be a poor account of the computation.

**Why healthcare is its own problem.** Scarce expert labels · severe imbalance · privacy limits on pooling · scanner/site heterogeneity · label noise and inter-rater disagreement · 3D volumes · distribution shift between hospitals.
> Pick one and give the consequence: *scanner heterogeneity means the model learns site-specific artefacts and collapses on a new hospital's machine.* The consequence is the answer; the list is just the label.

---

## If you read nothing else

1. **Say the "because"** — then say what it does to a model trained on one hospital's scans.
2. **Heavy tail = tolerant.** L1 is robust.
3. **The `I` in `I + ∂f/∂h`** is why residual nets train.
4. **Magnitude → saturation → dead gradient.** That's `√d_k`, and it's the KNN scaling story again.
5. **Federated: updates move, data don't — and heterogeneity is a separate, statistical problem.**
6. **Saliency shows where, not why.**

*Measured-error anchors: `ANCHORS.md`. Flag history: `study/student_progress.md`.*
