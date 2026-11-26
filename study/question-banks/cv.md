# Question Bank — Computer Vision · [OXFORD]
<!-- Appended by tutor sessions. Sprint: overlap decks only (02, 06, 07, 08, 09, 16, 17, 18); full course in phase 2. -->

> ⚠️ **EMPTY as of 2026-11-11 (D56) — flagged, not forgotten.** 20 CV decks are cached in `study/cache/cv/`; **zero questions are banked here.** The campaign is scheduled to turn CV-only on **20 Nov** and the assessment is **25 Dec (T-44)**, so this is not yet late — but it is the one genuinely hollow artefact on the board, and it was found by an audit that initially *passed* it, because the file exists. Mining starts 20 Nov per SYLLABUS Block 5; the eight overlap decks (02, 06, 07, 08, 09, 16, 17, 18) are the first targets since they were taught in Blocks 1–2 and are half-warm. Recorded here so that the first CV window does not arrive expecting a bank that was never written.

---

## Mined 2026-11-17 (D62) — overlap decks, batch 1

*The pause on **serving** CV holds until 20 Nov; mining the bank is not serving. Built now so the first CV window has something to draw on rather than arriving empty — the same mistake as the mock that was discussed for nine Saturdays and never written. No arithmetic in any item: both completed orals were structural, and the CV assessment is assumed the same until told otherwise.*

### QB-CV-0001 · [OXFORD] · forced-choice direction · `02_Filtering` — "Nyquist-Shannon sampling theorem" · not yet asked
The theorem says the sampling frequency must be **at least twice** the maximum frequency in the signal to reconstruct it perfectly.
**(a)** You halve the sampling rate on a detailed texture. Does the problem come from frequencies *above* or *below* the new limit?
**(b)** Name what you see when it goes wrong — the deck gives three symptoms.
> Above. Content above half the sampling rate cannot be represented and **masquerades as low-frequency content** — that impersonation is what "aliasing" names. Deck's symptoms: **disintegrating textures, Moiré patterns, false colour.**

### QB-CV-0002 · [OXFORD] · mechanism, "why deliberately destroy information" · `02_Filtering` — "Anti-aliasing" · not yet asked
The deck's fix: *before* sampling, remove all frequencies greater than half the new sampling frequency — and it says plainly this **loses information, but is still better than aliasing.**
**Why is throwing information away the better option?** Answer as a mechanism, not "because aliasing is bad."
> Because the high frequencies are not merely lost when you subsample — they are **re-encoded as false low frequencies** that are indistinguishable from real signal, so they corrupt the data you kept. Blurring first **deletes** them; subsampling without it **disguises** them. A known absence beats an unrecognisable lie.

### QB-CV-0003 · [OXFORD] · forced choice · `02_Filtering` — "Sampling and reconstruction" / "Images as Functions" · not yet asked
The deck frames an image two ways: as a grid of pixels, and as a **function**.
Which framing do you need to state the sampling theorem at all, and why can't the other one express it?
> The function view. Sampling theory is about **frequency content**, which only exists for a continuous signal being measured at intervals; a finished pixel grid is already the *result* of sampling and has no notion of what was lost. You cannot talk about exceeding a limit from inside the thing the limit produced.

### QB-CV-0004 · [OXFORD] · mechanism + the limit case · `07_CNNs` — "Parameter sharing" · not yet asked
The deck's justification: *"detecting e.g. an edge is important at any position of the image."*
**(a)** What property of images does that sentence assert?
**(b)** Name a vision task where the assertion is false.
> **(a)** Translation invariance of *what is worth detecting* — feature usefulness does not depend on location, so one filter can serve every position and every position becomes a training example for it. **(b)** It fails where position carries meaning: registered medical images with fixed anatomy, document layout, or anything where "top-left" is semantically different from "bottom-right". *(Same shape as the DL4H weight-sharing anchor — one fact, two courses.)*

### QB-CV-0005 · [OXFORD] · forced-choice direction · `07_CNNs` — "CNN Architecture" (stride) · not yet asked
The deck: **stride > 1 results in spatial sub-sampling of the feature maps.**
**(a)** Raise the stride — does the feature map get bigger or smaller, and what happens to the receptive field of the next layer measured in input pixels?
**(b)** Connect this to `QB-CV-0001`. What have you just done to the sampling rate, and what does the theorem then warn you about?
> **(a)** Smaller map; the next layer's receptive field grows, because each of its units now spans more input. **(b)** You have **subsampled** — so the theorem applies, and striding without blurring first is exactly the aliasing case. **This is the through-line worth having: stride is subsampling, and subsampling without a low-pass is aliasing.**

### QB-CV-0006 · [OXFORD] · structural, "which invariance" · `07_CNNs` — "Pooling Layers" / "Max-Pooling Example" · not yet asked
Max-pooling, 2×2 window, stride 2 — the deck's common case.
**(a)** What does it keep and what does it discard?
**(b)** What invariance does that buy, and state the cost in the same breath.
> **(a)** Keeps the **maximum response** in each window; discards *where in the window* it occurred and the other three values. **(b)** Buys **small-translation invariance** — the answer is unchanged if the feature shifts within the window — at the cost of **spatial precision**, which is why segmentation and localisation architectures either pool less or must recover the lost resolution later.

## Mined 2026-11-17 (D62, S3) — overlap decks, batch 2

*`06_Classification` turned out to carry **nearest-neighbour, embeddings and precision/recall** — which means three of his nine measured flags (FP-1, FP-2, FP-4) can be re-attacked in a third course, using CV's own artefacts instead of IntroML's. That is worth more than generic CV coverage: a flag re-attacked from an unused angle is the one thing the flag protocol actually requires, and these angles have never been used.*

### QB-CV-0007 · [OXFORD] · formula-reading, **FP-1 re-attack from a new course** · `06_Classification` — "Embedding Function Example" · not yet asked
The deck's toy embedding: **count the blue pixels and count the green pixels**, so `f : ℝ^(H×W×3) → ℝ²`, then classify boats vs deer by nearest neighbour in that 2-D space.
**(a)** Both coordinates are pixel *counts*, so they share a scale. Now replace one axis with **image width in pixels** and keep the other as a blue-pixel count. What happens to the nearest-neighbour decision, and which term in the squared distance tells you?
**(b)** Say the fix and say what it does.
> **(a)** The width axis has a far larger numeric range, so its squared difference **dominates the sum** and the neighbour ranking is decided almost entirely by image size — the blue-pixel evidence is drowned out. **(b)** Scale the features (min–max or standardisation) so each contributes comparably. *This is his own 23 Sep mechanism — "income decides, it's several magnitudes higher" — in CV's clothing. If it comes out complete here, that is FP-1's second clean pass on a new day and a new format.*

### QB-CV-0008 · [OXFORD] · forced-choice direction, **FP-4 re-attack** · `06_Classification` — "Precision and Recall" · not yet asked
The deck: *"Accuracy can be misleading when the label distribution is skewed. In a dataset where 90% of samples are of class 0, you can obtain 90% accuracy by always predicting 0."* And it gives **Precision = TP/(TP+FP)**, **Recall = TP/(TP+FN)**.
**(a)** For that always-predict-0 classifier, what are precision and recall **on class 1**? One of them is awkward to state — say which and why.
**(b)** Which denominator is "everything I flagged" and which is "everything that was really there"?
> **(a)** Recall on class 1 is **0** (TP = 0, so 0/FN). Precision is **0/0 — undefined**, because the model never flags class 1 at all; the awkwardness is that you cannot be wrong about predictions you never make. **(b)** Precision's denominator TP+FP is everything flagged; recall's TP+FN is everything actually present. *Third course, same denominators — and the undefined-precision case is a sharper version of the IntroML 99% item.*

### QB-CV-0009 · [OXFORD] · structural, where the cost sits · `06_Classification` — "Nearest Neighbour Classification / Algorithm" · not yet asked
The deck splits it explicitly. **Training:** precompute embeddings of all training samples, optionally build a fast lookup structure such as a kd-tree. **Testing:** embed the new image, look up the k nearest, compute the class histogram.
**(a)** Which phase does the real work, and what is the kd-tree *for*?
**(b)** The deck calls the training step "precompute". Is anything actually **learned** there?
> **(a)** Testing. Every query must be compared against the training set, so cost scales with dataset size at *prediction* time — which is what the kd-tree exists to blunt, by making the lookup sub-linear instead of a full scan. **(b)** No parameters are fitted: "training" here is **storage plus indexing**, which is exactly why it is called a lazy learner. *Third angle on the item he did not answer on 23 Sep (LR-0002), and this time the deck hands him the two-phase split rather than asking for it.*

### QB-CV-0010 · [OXFORD] · mechanism, "why patches" · `08_Transformers` — "CNNs to Transformers" (ViT, Dosovitskiy 2021) · not yet asked
The paper title the deck leads with: ***"An image is worth 16×16 words."***
**(a)** Why cut the image into patches at all, rather than feeding pixels as tokens?
**(b)** Connect this to `QB-CV-0005`. What have you done to the spatial sampling rate, and what is the standing warning?
> **(a)** Attention cost grows quadratically in the number of tokens, so pixels-as-tokens is intractable; a patch is a token-sized unit that keeps the sequence short enough. **(b)** Patching is **subsampling with a stride equal to the patch size** — so the aliasing warning from the filtering deck applies here too, and fine detail smaller than a patch cannot be recovered downstream. **That makes three decks saying one thing: stride, patching and subsampling are the same operation under different names.**
> ⚠️ **Shares an answer with QB-CV-0012.** *"Attention cost is quadratic in the number of tokens, which is why ViT patches first"* answers **0010(a)** and **0012(b)**. They are different questions, but a pass on both is **one measurement, not two** — do not log them as independent evidence, and serve them well apart.

### QB-CV-0011 · [OXFORD] · structural, the asymmetry · `08_Transformers` — "Attention", slide 14 · **✅ VERIFIED against the PDF 2026-11-26** · not yet asked
**Your deck writes all three the same:** *"A query function `Q: ℝ^d → ℝ^d` · A key function `K: ℝ^d → ℝ^d` · A value function `V: ℝ^d → ℝ^d`"*, and later `Attn(Q,K,V) = softmax(QKᵀ/√d)`. The original Transformer instead gives query and key a shared width `d_k` and the value its own `d_v`.
**(a)** Which of the three comes from the token doing the looking, and which come from the tokens being looked at?
**(b)** One of those two dimension choices is **forced** and the other is **free**. Which is which, and what forces it?
**(c)** So why can your deck collapse all three to `d` without breaking anything?
> **(a)** The **query** comes from `x_i`, the one doing the looking; **keys and values** come from every `z_j` being looked at. **(b)** Query and key **must** match: their dot product is the relevance score, and a dot product needs two vectors of the same length. That one is **forced.** The value is never compared with anything — it is only weighted and summed — so its width is **free**, and all it sets is the output width. **(c)** Because putting `d_v = d_k = d` satisfies the forced constraint and picks an arbitrary-but-legal value for the free one. **The deck is choosing a simple instance, not stating a requirement** — and knowing which of the three widths you could change without touching anything else *is* the mechanism.
> *Naming q, K, V without the comparison/transport distinction is FP-9 in attention's clothing. **And note a trap in your own slides:** one reads *"compute similarities between keys and values using a dot product"* where it means keys and **queries** — the next line, *"large if key is similar to query"*, confirms it. That is in the PDF itself, not an extraction artefact.*

### QB-CV-0012 · [OXFORD] · compare, with the cost named · `08_Transformers` — "CNNs to Transformers" / "Attention" · not yet asked
A convolution looks at a **fixed local window**; attention lets every token look at **every other token**.
**(a)** What does attention buy that stacking more conv layers does not?
**(b)** Name the price, and say which quantity it scales with.
> **(a)** A **constant-length path** between any two positions — a conv net needs depth to connect distant pixels, and each extra hop is another factor in the gradient product, which is the vanishing-gradient story. Attention reaches across the image in one step. **(b)** Cost is **quadratic in the number of tokens** (every token attends to every token), which is precisely why ViT patches first. *Pairs with the DL4H residual/vanishing-gradient anchor: both are about path length between distant things.*
> ⚠️ **Shares an answer with QB-CV-0010** — see the note there. Different question, same sentence for the quadratic-cost half; count the pair as one measurement.

## Mined 2026-11-18 (D63) — overlap decks, batch 3

*`18_Unsupervised` names its own **Failure Cases** and **Inherent Ambiguity**, which is what an examiner probes — a deck that admits where its method breaks is handing you the question. And one of those failures turns out to be the **L1/L2 noise-model anchor (FP-6, FP-5) in disguise**, which makes it a fourth measured flag re-attackable in CV.*

### QB-CV-0013 · [OXFORD] · mechanism, "why is this a design requirement" · `18_Unsupervised` — "What we need to do" · not yet asked
The deck's list of what self-supervision has to do ends on a blunt one: *"Often: **prevent trivial solutions and cheating**."*
**(a)** Why is that a *design requirement* rather than a bug to fix later?
**(b)** Give a concrete trivial solution for a pretext task of your choice.
> **(a)** Because the pretext task is a **proxy** — you only care about the representation it forces the network to build, so any shortcut that solves the pretext *without* building that representation defeats the entire point while still minimising the loss. The loss cannot tell you this happened. **(b)** E.g. inpainting where the mask boundary leaks colour statistics, so the model interpolates edges rather than learning objects; or a rotation-prediction task on images with visible watermarks or sky-at-top priors.

### QB-CV-0014 · [OXFORD] · mechanism, **FP-6/FP-5 re-attack in a third setting** · `18_Unsupervised` — "Inherent Ambiguity" / "Failure Cases" · not yet asked
Colorization from greyscale. The deck shows **Prediction** beside **Ground Truth** under the heading *Inherent Ambiguity*, and the predictions come out **washed out**.
**(a)** A grey car could plausibly have been red or blue. What does that make the ground-truth colour, statistically?
**(b)** Train this with a squared-error loss. What colour does the model produce for that car, and **why is that the loss's fault rather than the model's?**
> **(a)** One **sample** from a multimodal distribution over plausible colours — not *the* answer. **(b)** Squared error is minimised by the **conditional mean**, so averaging red and blue gives a desaturated grey-brown: the model outputs the mean of the modes, which is a colour nobody would ever paint a car. **A model that is right about the distribution scores badly under a loss that assumes one answer.** *This is the L2-assumes-a-single-peaked-target point from DL4H, arriving as a picture — and the reason the real fix is to change the loss (classification over colour bins) rather than the network.*

### QB-CV-0015 · [OXFORD] · forced-choice direction · `18_Unsupervised` — "Learning Signal Toolbox" · not yet asked
The deck: *"Learning signals are general ideas to incorporate **priors**"*, and *"priors model general assumptions about the world/task."*
You need features for **segmentation** (dense, per-pixel) and separately for **retrieval** (one vector per image). Which way does the choice of pretext task push, and why?
> Toward pretext tasks whose output shape matches the downstream need: **dense reconstruction-style tasks** (inpainting, colorization) build per-pixel features useful for segmentation; **instance-level tasks** (contrastive, matching whole images) build a single discriminative vector useful for retrieval. The prior you inject is the assumption you are making about the world, so it should be the assumption the downstream task actually relies on.

### QB-CV-0016 · [OXFORD] · mechanism, FP-9 bait · `17_RepresentationLearning` — "Handcrafting Representations" · not yet asked
Handcrafted features *"(almost) worked"* for image retrieval, structure-from-motion and face detection. The deck then lists why alternatives were needed — and the last reason is the interesting one: *"Fusion non-trivial. Rule-based fusion outruled. **Fusion of contributing factors itself a comparably complex representation problem.**"*
**Say what that sentence means.** The lazy answer is "deep learning is better" — that is a label, not a mechanism.
> Finding individual discriminative cues by hand was often possible; **combining** them was not. Any rule you write to weigh cue A against cue B is itself a representation of the problem, of roughly the same difficulty as the one you were trying to avoid — so hand-design just relocates the hard part instead of removing it. **Learning wins because it learns the fusion**, not because any single learned feature beats a hand-designed one.

### QB-CV-0017 · [OXFORD] · structural · `17_RepresentationLearning` — "Representation Mathematical Model" / "Representations" · not yet asked
The deck pairs an image with a vector of numbers and calls the vector a *"transcript"*, then feeds it to e.g. a classifier.
**(a)** What is the representation's job, stated so that it does not mention neural networks?
**(b)** Two different images of the same cat should give what, and two images of different animals should give what?
> **(a)** To map the raw signal into a space where the **downstream decision becomes easy** — ideally linearly separable — by discarding what is irrelevant and keeping what distinguishes. **(b)** Same cat → **nearby** vectors (invariance to pose, lighting, scale); different animals → **distant** vectors (discriminativeness). Those two demands pull against each other, and that tension *is* the representation-learning problem.

### QB-CV-0018 · [OXFORD] · compare, "when is the old way still right" · `17_RepresentationLearning` — "Correspondences" (SIFT) · not yet asked
The deck shows point correspondences from **SIFT**, a classic hand-designed algorithm, in a lecture arguing for learned representations.
**Why is it still there?** Name a situation where you would reach for SIFT over a learned descriptor.
> Because hand-designed is not the same as obsolete: SIFT needs **no training data**, is **deterministic and inspectable**, and its invariances (scale, rotation) are *guaranteed by construction* rather than hoped for from data. Reach for it with **no labels and no time to train**, on a geometric task like structure-from-motion where correspondence accuracy matters more than semantics, or where you must be able to explain why two points matched. *Knowing when the classic tool is the right one is a better answer than "learned is better".*

## Mined 2026-11-21 (D66) — first non-overlap decks, batch 4

*Two findings worth more than the items. **(1) The aliasing through-line is the lecturer's own, not mine:** `03_FourierTransforms` opens with *"Observation 1 — From lecture 02: down-sampling leads to aliasing"* and shows 512×512 → 64×64 → 16×16. So QB-CV-0005/0010 are testing a link the course itself draws, which makes it examinable rather than merely true. And `03` supplies the **tool** that the chain was missing. **(2) `11_Segmentation`'s own caveat explains the DL4H tumour problem** — *"IoU is favourable to large objects (harder to intersect small objects)"* — a fifth cross-course link.*

### QB-CV-0019 · [OXFORD] · formula-reading, completes the chain · `03_FourierTransforms` — "Convolution theorem" · not yet asked
`ℱ{f ∗ g} = ℱ{f} · ℱ{g}` — convolution in space is **multiplication** in frequency, and vice versa.
**(a)** Deck 02 said: before subsampling, remove frequencies above half the new sampling rate. Using this theorem, say what "remove" means **mechanically**.
**(b)** So why is a blur the right tool for the job?
> **(a)** You multiply the image's spectrum by a mask that is 1 below the cutoff and 0 above it — the unwanted frequencies are **multiplied by zero**, i.e. genuinely deleted rather than hidden. **(b)** Because by this theorem, multiplying the spectrum by a low-pass mask *is* convolving the image with the mask's inverse transform — and that spatial kernel is a blur. **A blur is a low-pass filter; those are two descriptions of one operation.**

### QB-CV-0020 · [OXFORD] · forced choice, "why bother with the other domain" · `03_FourierTransforms` — "Convolution theorem" / "2D convolution theorem example" · not yet asked
You need to convolve a large image with a large kernel.
**Which domain, and what decides it?**
> Frequency. Spatial convolution costs roughly (image pixels × kernel pixels); in frequency it is **two transforms, one elementwise multiply, one inverse transform**. The crossover is kernel size: tiny kernels are cheaper convolved directly, large ones are far cheaper multiplied. **The theorem is not just an identity, it is a performance decision** — and saying which way it goes *and why* is the mechanism.

### QB-CV-0021 · [OXFORD] · interview-style, the four-deck chain · `03_FourierTransforms` — "Observation 1" · not yet asked
The deck opens by pointing back: *"From lecture 02: down-sampling leads to aliasing."*
**Tell the whole story across the course in four steps**, naming where each piece comes from.
> **02** states the constraint (Nyquist: sample at ≥ 2× the max frequency, or high content masquerades as low — aliasing). **03** supplies the tool (convolution theorem: a blur *is* a low-pass, so you can delete the offending frequencies before sampling). **07** performs the operation without naming it (stride > 1 **is** subsampling — so stride without a blur aliases). **08** performs it again at a coarser grain (ViT patching is subsampling with stride = patch size, and detail below patch scale is unrecoverable). **One constraint, one tool, two silent applications.** *This is the single most reusable answer in the CV material, and the lecturer draws the first link himself.*

### QB-CV-0022 · [OXFORD] · structural, the ladder · `11_Segmentation` — "Granularity" · not yet asked
The deck lays out a granularity ladder: **image classification → object detection → pixel-level segmentation**, labelled *image-scale*, *localization / spatial (regions)*, and *labelling*.
**(a)** What is the output of each, concretely?
**(b)** Semantic segmentation *"does not differentiate instances, only cares about pixels."* What question can it therefore not answer?
> **(a)** One label for the whole image → a set of boxes with labels → one label per pixel. The axis is **how finely the answer is localised in space**. **(b)** "How many?" Two touching cats are one undifferentiated cat-coloured region, so counting, tracking individuals, or per-object measurement all need **instance** segmentation.

### QB-CV-0023 · [OXFORD] · mechanism, **and the DL4H link** · `11_Segmentation` — "Evaluation" · not yet asked
The deck: *"Per-class IoU… compare the binary masks of prediction and GT for each class, average over classes."* And then its own warning: ***"IoU is favourable to large objects (harder to intersect small objects)."***
**(a)** Why is overlap harder to achieve on something small? Answer geometrically.
**(b)** Your DL4H course segments a tumour occupying a tiny fraction of the voxels. What does (a) say about reading its score?
> **(a)** IoU is intersection over union, and a fixed boundary error costs a far larger *fraction* of a small object than a large one — a two-pixel miss around a ten-pixel lesion is catastrophic, around a thousand-pixel organ it is noise. **Perimeter-to-area scales against you as objects shrink.** **(b)** A low Dice/IoU on a small tumour may reflect its **size**, not the model's quality — so compare like with like, and never read a single averaged overlap score as "how good is this model". *The DL4H item says Dice survives imbalance where accuracy does not; this one says Dice is still size-biased. Both are true and the pair is the complete answer.*

### QB-CV-0024 · [OXFORD] · mechanism, "what is wasteful" · `11_Segmentation` — "Sliding Window" · not yet asked
The naive approach: *"Slide a window over the whole image. Classify the centre pixel of the window."*
**(a)** Name what is wasted, precisely.
**(b)** What is the fix, and why does it work?
> **(a)** Neighbouring windows overlap almost entirely, so nearly every convolution is **recomputed** for each pixel — the same features are extracted thousands of times. **(b)** Make the network **fully convolutional**: run it once over the whole image and let the conv layers produce a dense output map. It works because convolution is **already sliding** — the redundancy was in the loop around the network, not in the network. *The window never needed to move; the computation already did.*

## Mined 2026-11-23 (D68) — batch 5

*`04_Restoration` is the **fifth deck in the Fourier chain** and the one that shows why the chain has a limit. `20_EthicsPrivacy` turns out to be **FP-4 with stakes** — it recaps the same confusion matrix he has twice swapped, in a case where a false positive is a longer prison sentence. That is the sixth cross-course link, and the most likely thing an examiner opens an ethics question with.*

### QB-CV-0025 · [OXFORD] · formula-reading, extends the chain · `04_Restoration` — "Modelling Degradation" / "Degradation Model" · not yet asked
The deck models an observed image as `g(x,y) = ∬ d(x−u, y−v) f(u,v) du dv + n(x,y)` — i.e. **`g = f ∗ d + n`**: the true image convolved with the kernel `d`, plus noise. *(The deck names the kernel **`d`**; much of the literature calls it `h`. Convolution commutes, so which factor carries the shift does not matter.)*
**(a)** Name each of the four symbols.
**(b)** By the convolution theorem (`03`), `ℱ{g} = ℱ{f}·ℱ{h} + ℱ{n}`. So restoring `f` looks like simple division. **Why is that a trap?**
> **(a)** `g` observed, `f` true scene, `d` the blur kernel, `n` additive noise. **(b)** Because dividing by `ℱ{d}` also divides the **noise** by it — and `ℱ{d}` is near zero at high frequencies, exactly where a blur has destroyed information. Dividing a noise term by something near zero **amplifies it without bound**, so naive inverse filtering returns a picture of amplified noise. *This is the limit of the chain: `03`'s theorem says restoration is division, and `04` says the noise term is why you cannot just do it.*

### QB-CV-0026 · [OXFORD] · definition + "why it matters" · `04_Restoration` — "Degradation Model" (PSF) · not yet asked
The deck: *"`d(x,y)` is called the **impulse response** or **point spread function** of the imaging system."* **✅ VERIFIED against the PDF 2026-11-26** — the extraction rendered this symbol as an unreadable glyph and it was transcribed as `h` from convention.
**(a)** What does the name *point spread function* literally describe?
**(b)** Why does knowing `d` decide whether restoration is possible at all?
> **(a)** Feed the system a single point of light and `h` is the blob that comes out — **how a point gets spread.** Since any image is a sum of points, convolving with `h` is the whole degradation. **(b)** Restoration is undoing a known operation; if `d` is unknown you are solving for `f` **and** `d` from one equation (blind deconvolution), which is underdetermined. **Knowing the PSF converts an ill-posed problem into a merely difficult one.**

### QB-CV-0027 · [OXFORD] · assumptions, same family as Naive Bayes · `04_Restoration` — "Degradation Model" · not yet asked
The deck adds its own hedge: *"This is only one way of modelling degradation. Others are possible too."*
**What is this model assuming?** Name two assumptions and say what each buys.
> **Linearity and shift-invariance** (the same blur everywhere, so degradation is a convolution) and **additive, signal-independent noise.** They buy you the convolution theorem and therefore a frequency-domain solution. They fail for **spatially varying blur** (motion in part of the frame, depth-dependent defocus) and for **multiplicative or Poisson noise**, which is what low-light and medical imaging actually have. *Same shape as the Naive Bayes item in IntroML: an assumption that is obviously false, kept because of what it makes computable — and the answer is always what it buys versus where it breaks.*

### QB-CV-0028 · [OXFORD] · **FP-4 re-attack, with stakes** · `20_EthicsPrivacy` — "Case Study: COMPAS" / "Recap: Error Metrics" · not yet asked
COMPAS predicts recidivism, and the deck notes its scores **influenced criminal sentences** in New York, Wisconsin, California and Florida.
**(a)** For this classifier, say in plain words what a **false positive** and a **false negative** each mean *to the person*.
**(b)** Which error does a longer sentence follow from, and which denominator is it in?
> **(a)** False positive: predicted to re-offend, **did not** — a person punished for a crime they were never going to commit. False negative: predicted safe, did re-offend. **(b)** The harm from the sentencing decision follows the **false positive**, which sits in precision's denominator (TP+FP, "everything I flagged"). *Third course, same two denominators he swapped twice on D1 — and here naming the wrong one gets the ethics of the case backwards, which is why this is the version worth remembering.*

### QB-CV-0029 · [OXFORD] · interview-style, the impossibility · `20_EthicsPrivacy` — "Case Study: COMPAS" (ProPublica, >7000 people, Broward County) · not yet asked
ProPublica analysed COMPAS scores for over 7,000 arrests and found the error rates fell differently across groups; the vendor replied that the scores were **calibrated** — a given score meant the same re-offence probability for everyone.
**Both claims were true. How?**
> Because they are **different fairness criteria, and when base rates differ between groups they cannot both hold.** Calibration fixes *what a score means*; equal false-positive rates fix *who bears the cost of being wrong*. Satisfy one and the other must break. **So "is this model fair?" has no answer until you say which definition you mean** — and the choice is a decision about who absorbs the error, which is a question for the people affected, not a hyperparameter. *If an examiner asks one ethics question, it is likely to be this one, and the answer that scores is naming the trade-off rather than picking a side.*

### QB-CV-0030 · [OXFORD] · mechanism, FP-9 bait · `20_EthicsPrivacy` — "Case Study: COMPAS" · not yet asked
A common defence: *"the model isn't biased, it just learns from the data."*
**Say precisely why that is not a defence.** The lazy answer is "but the data is biased" — that is a label, not a mechanism.
> Because the **label itself is a measurement, not the truth.** "Recidivism" in the training data means *re-arrested*, which is a record of policing as much as of offending — so a group policed more heavily generates more positive labels at the same underlying rate. The model faithfully reproduces **the measurement process**, and faithfulness to a biased measurement is exactly how a statistically correct model produces unjust decisions. **"Learning from the data" is the mechanism of the problem, not an alibi for it.** *Note the shape: this is the same move as the colorization item — the model is right about what it was trained on, and what it was trained on was the wrong target.*

## Mined 2026-11-23 (D68, S3) — batch 6: the two decks that were claimed as mined and were not

*`09_VisualizationUnderstanding` and `16_GenerativeModels` are **overlap** decks — they were named in "all 8 overlap decks mined" on 18 Nov and have produced zero items until now. Both are among the most valuable in the course. 09 is **FP-9 pointed at a model**; 16 contains the item that reads the L1/L2 anchor from the other side, which is the **seventh cross-course link**.*

### QB-CV-0031 · [OXFORD] · mechanism, **FP-9 in a mirror** · `09_VisualizationUnderstanding` — "Clever Hans" / "Does the model know what a horse is?" · not yet asked
The deck tells the story of **Clever Hans** (a German horse, 1895–1916, that appeared to do arithmetic) and then shows a PASCAL VOC horse classifier with high accuracy whose average heatmap lights up **a copyright notice**.
**(a)** What was actually wrong with the Clever Hans conclusion?
**(b)** What does the heatmap say about the classifier?
**(c)** The deck lists explainability as *"an additional tool beyond test set evaluation."* **Why is test accuracy structurally unable to catch this?**
> **(a)** The horse was not computing — it was reading involuntary cues from its trainer, **who did not know he was giving them.** Performance on the task was real; the mechanism was not the one everyone assumed. **(b)** Many horse images in that dataset carry a watermark, so the model learned **the watermark**, not the horse. **(c)** Because the test set is drawn from the **same distribution** as the training set, so the spurious feature is in the test images too — **the shortcut scores exactly as well as the real mechanism.** A held-out set can only catch failures it happens to contain.
> *Say this one out loud: **a number without a mechanism is Clever Hans.** That is FP-9 — his own dominant flag — stated about a model instead of a candidate, which is why it is the version worth remembering.*

### QB-CV-0032 · [OXFORD] · structural, three-way trade-off · `09_VisualizationUnderstanding` — "Taxonomy – Approaches" · not yet asked
The deck splits explainability into **post-hoc analysis**, **transparent models** and **learned explanations**.
**Which costs nothing at training time, and what do you pay instead?** Then name the cost of each of the other two.
> **Post-hoc** is free at training time — the model is already fixed, so there is **no impact on performance**. You pay in scope: the explanations are **local around individual predictions**, so you learn *"why this one"* and not *"what the model does in general."* **Transparent models** build semantics into the mechanism, but need a **task-specific architecture** and can cost performance. **Learned explanations** come out alongside predictions with no post-hoc step, can cost performance, and **might need meta-explanations** — you now have to explain the explainer.
> *The shape to notice: none of the three is free. Each moves the cost to a different place, and naming which place is the answer.*

### QB-CV-0033 · [OXFORD] · **interview-style with a follow-up chain** · `09_VisualizationUnderstanding` — "Explainability" (GDPR Art. 13/14/22) + "Explanations: Recipient" · links to `20_EthicsPrivacy` · not yet asked
The deck lists among explainability's purposes *"it is in the law: (GDPR Art. 13,14,22) the right for explanation"*, and separately insists explanations must **adapt to the recipient** — developers, domain experts, users — and to the **content**: representations, individual predictions, behaviour, examples.
A model you deployed declines loan applications.
**(a)** Who are the recipients, and what content does each need?
**(b)** *Follow-up:* your post-hoc saliency map says which input features mattered. Why might that satisfy a developer and **fail the applicant**?
**(c)** *Follow-up:* connect this to COMPAS.
> **(a)** The **developer** needs representations and behaviour — is the model using the feature I think it is, across the population. The **domain expert** needs individual predictions they can sanity-check against their own judgement. The **applicant** needs a reason that is **actionable and contestable**: what about my case, and what would change it. **(b)** Because saliency answers *where the model looked*, and the applicant is owed *why the decision went against them.* **Saliency shows where, not why** — a highlighted feature is not a reason, and "your postcode mattered" is an explanation that makes things worse rather than better. **(c)** COMPAS is the same gap with the stakes raised: a risk score influenced sentences, and a defendant cannot contest a number whose basis they cannot see. **`20` gives the harm; `09` gives the response — and the response only works if it is aimed at the right recipient.**

### QB-CV-0034 · [OXFORD] · formula-reading · `16_GenerativeModels` — "Autoregressive Models" · not yet asked
The deck decomposes an image's likelihood by the chain rule: **`p(x) = Π_i p(x_i | x_1, …, x_{i−1})`**, calls it an **explicit** model, and notes it is the main generative model in NLP.
**(a)** Why is this an *exact* likelihood rather than an approximation or a bound?
**(b)** What does it cost you at sampling time?
> **(a)** Because the chain rule is an **identity** — every joint distribution factorises this way, with no assumption added. So modelling each conditional gives the exact likelihood, which you can maximise directly and, crucially, **evaluate on a test set**. **(b)** Generation is **sequential**: each pixel is conditioned on all the ones before it, so producing one image costs as many forward passes as there are pixels, and none of them can be done in parallel.
> *Pair this with QB-CV-0036: both autoregressive models and diffusion buy quality by spending many passes per sample. Different reason, same bill.*

### QB-CV-0035 · [OXFORD] · **the seventh cross-course link — the L2 anchor read from the other side** · `16_GenerativeModels` — "Training a diffusion model" · re-attacks FP-6 · not yet asked
Diffusion trains with what the deck calls a **"simple L2 loss"**: the slide reads `Loss ‖f(x_t, t) − ε_t‖²₂` over training examples `(x_t, ε_t)`. **✅ VERIFIED against the PDF 2026-11-26** — *the deck names the network **`f`**; the DDPM paper writes `ε_θ`, and this item previously used that symbol as though it were the deck's.*
But the colorization anchor (QB-CV-0014, and FP-6 on the flag sheet) says squared error **fails exactly when the target is ambiguous**, returning the mean of the modes and painting a colour nobody would choose.
**Both statements are true. So why doesn't diffusion suffer the colorization problem?**
> Because the regression target is **not an ambiguous image** — it is **the specific noise sample that was actually added** to make `x_t`. That is one known value, not one draw from a distribution over plausible answers, so **the conditional mean is the right thing to return.** The multimodality has not gone away; it lives in the **iteration**. Each reverse step is a small, nearly single-peaked correction, and the many plausible final images come from the chain of fresh samples (`z ~ N(0,I)` injected at each step), not from any one regression target.
> **So the rule was never "L2 is bad."** It is: **L2 returns the conditional mean, which is correct precisely when the target is single-peaked.** Diffusion *engineered its target to be single-peaked*; colorization did not. **Same principle, opposite verdict** — and being able to say that is the difference between having memorised the anchor and understanding it.

### QB-CV-0036 · [OXFORD] · structural, "name the axis" · `16_GenerativeModels` — "Sampling from a diffusion model" / "Latent diffusion" · not yet asked
The sampling loop runs `for t = T, …, 1`, and the deck states plainly: *"Evaluate diffusion model T times to generate one sample."* It then offers **latent diffusion** — compress the image first with a VQ-VAE and diffuse in a `3 × H × W` latent space — as the way to make it **cheaper**.
**Which cost does latent diffusion reduce, and which does it leave untouched?**
> It reduces the **cost per evaluation**: each of the T passes now runs on a small latent grid instead of full-resolution pixels. It does **not reduce T**, so the number of **sequential, un-parallelisable steps is unchanged** — the latency floor is still T model calls deep.
> *"It's faster" is the FP-9 answer here. **Name which axis the trick moves**, and say which one it does not.*

### QB-CV-0037 · [OXFORD] · mechanism + the deck's own picture · `16_GenerativeModels` — "Evaluation" / "Fréchet Distance" / "FID" · not yet asked
The deck: *"Evaluation of explicit generative models is easy — measure `log p(x)` on a test set; whichever model has higher probability wins. Evaluation of implicit models is very difficult: we can only sample from the model, and we do not know how to measure the quality/probability of a sample."*
**(a)** Say why likelihood is simply unavailable for a GAN.
**(b)** The deck's picture for Fréchet distance: *a dog and its owner walk separate paths, can only go forward, and the distance is the **shortest leash** that lets both finish.* In **FID**, what two things are on the two paths?
**(c)** Why is asking people which images they prefer not the fallback?
> **(a)** A GAN gives you a **sampler, not a density**. There is no tractable `p(x)` to evaluate, so there is nothing to measure on a test set — the thing the explicit models are scored on does not exist. **(b)** Two **distributions**, not two images: real images and generated images, each summarised by Inception features. The leash measures how far apart the two *paths* stay, so FID scores **the population you generate**, not any individual sample. **(c)** Because preference is **vague and confounded** — it mixes realism with faithfulness to the prompt — and it does not scale or give you a signal you can optimise against.
> *This is the metric-choice family one more time: accuracy, then precision/recall, then Dice, then IoU, now FID. **Every one of them exists because the previous one could not see something.** Being able to say what a metric cannot see is the answer that scores.*

## Mined 2026-11-24 (D69, S3) — batch 7: the deck that gives FP-2 a handle

*Mined because verifying `ANCHORS-CV.md` against the flag table showed its headline claim — "seven of the nine flags have a CV handle" — was **false when written**: FP-2 (cosine vs Euclidean) appeared nowhere in it, and had fallen through silently rather than being named as an omission. `05_MatchingIndexingSearch` turns out to hold the best possible handle for it, because **the lecturer makes the text-retrieval link himself.** Doing the work made the claim true rather than editing the number down.*

### QB-CV-0038 · [OXFORD] · **FP-2 re-attack — and the lecturer's own framing** · `05_MatchingIndexingSearch` — "Visual Words" / "Bag of Visual Words" · not yet asked
The deck builds a global image descriptor: run SIFT over a large dataset, **K-means the descriptors into K "classes"**, then describe an image by a **histogram of which feature classes it contains**. Then, in its own words:
> *"When computing the histogram, it does not matter where each feature comes from in the image. **This is similar to classic text-based retrieval systems: count how often each word appears in a document.** Documents on similar topics have similar statistics."* And: *"With large K the image descriptor is usually **sparse** (most entries are 0)."*
**(a)** A richly-textured photo yields far more keypoints than a plain one, so its histogram counts are larger across the board. Under **Euclidean** distance, what ends up deciding retrieval?
**(b)** What does **cosine** similarity change, and which quantity does it remove from the decision?
**(c)** What does the sparsity remark add to the argument?
> **(a)** The **total number of detected features** — i.e. how textured the image is. A dense image sits far from everything in Euclidean terms regardless of *what* it contains, exactly as a long document does. **(b)** Cosine compares **direction only**: the *mix* of visual words, normalised by magnitude. It removes **count** — the one quantity you do not want deciding whether two images show the same thing. **(c)** Most entries are zero, and **two images sharing a zero is not evidence they are alike.** The dot product only sums over visual words that actually co-occur, so cosine scores agreement on what is *present* rather than on a vast shared absence.
> *This is FP-2 exactly — his IntroML flag was cosine-vs-Euclidean on **text documents**, and the deck says BoW **is** classic text retrieval. So the transfer is the lecturer's, not an analogy, which makes it examinable rather than merely true. **Eighth cross-course link, and the cleanest: same model, new domain.***

### QB-CV-0039 · [OXFORD] · mechanism, cross-course · `05_MatchingIndexingSearch` — "SIFT Descriptor" (**the same slide also appears in `17_RepresentationLearning`, so it is repeated material and likelier to be examined**) · not yet asked
The deck: edge directions are *"invariant to brightness changes, **equivariant to rotation**"* — and then the very next step is *"**rotate all edges so that the global orientation is 'up'**."*
**(a)** What does *equivariant to rotation* mean for this descriptor, as distinct from *invariant*?
**(b)** What does the rotate-to-'up' step accomplish, and what is that manoeuvre called in general?
**(c)** Name the DL4H operation that achieves the same end by the opposite route.
> **(a)** Rotate the image and the descriptor's contents **rotate correspondingly** — the response is predictable, not unchanged. Invariant would mean *identical*. **(b)** By always measuring from the patch's own dominant orientation, two rotated copies of the same patch produce the **same** descriptor: it **converts equivariance into invariance**, by **canonicalisation** — align to a reference frame, then describe. **(c)** **Global average pooling.** A conv feature map is equivariant to translation; averaging it to one number per channel makes it invariant.
> *Two courses, one goal, two routes: **average the equivariant thing away, or align to a canonical frame first.** Being able to name both is a much better answer than defining equivariance.*

### QB-CV-0040 · [OXFORD] · structural, "why this shape" · `05_MatchingIndexingSearch` — "SIFT Descriptor" (the 128) · not yet asked
SIFT splits the neighbourhood into **4×4 = 16 regions**, computes an **8-direction** edge histogram in each, and concatenates: a **128-dimensional** vector.
**Why a grid of local histograms rather than one histogram over the whole patch?**
> Because a single histogram over the patch throws away **where inside the patch** each edge direction sits — two quite different structures with the same edge statistics would be indistinguishable. The 4×4 grid **keeps coarse spatial layout**; the histogram inside each cell **tolerates small shifts** of an edge within that cell. **So the grid buys discriminative power and the per-cell histogram buys tolerance, and 128 is where that trade was struck.** *Say the trade, not the number.*

### QB-CV-0041 · [OXFORD] · **interview-style with a follow-up chain** · `05_MatchingIndexingSearch` — "Feature Matching" · not yet asked
Brute-force matching: *"for each descriptor in the first image, return the one with the lowest distance (e.g. Euclidean distance); sort all matches by their distance and take the top N."* Then: *"check if matches are consistent with a transformation, e.g. a homography. **This is geometric verification.**"*
**(a)** The top-N matches are the closest in appearance. Why is that not enough?
**(b)** *Follow-up:* could a better descriptor fix it?
**(c)** *Follow-up:* so what is geometric verification actually supplying?
> **(a)** Because a descriptor sees only a **local patch**, and real scenes are full of **repeated structure** — windows on a facade, bricks, leaves. The nearest descriptor can be the **wrong instance of a correct-looking pattern**, and its distance will be genuinely small. **(b)** **No.** The ambiguity is in the image, not in the descriptor: the patches really do look the same, so no amount of descriptor quality distinguishes them. *That is the point worth making out loud.* **(c)** A **global constraint**. Correct matches must all agree on **one** transformation; wrong ones have no reason to agree with each other. So it is **evidence of a different kind, not more of the same kind.**
> *Same family as Clever Hans: every individual score was fine and the mechanism was still wrong, and the fix was an independent check rather than a better number.*
