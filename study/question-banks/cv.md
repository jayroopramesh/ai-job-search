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

### QB-CV-0011 · [OXFORD] · structural, the asymmetry · `08_Transformers` — "Attention" (q/K/V) · not yet asked
The deck introduces three functions: a **query** `q : ℝ^d → ℝ^k`, a **key** `K : ℝ^d → ℝ^k`, a **value** `V : ℝ^d → ℝ^v`. Intuition given: *x_i looks at all z_j and decides what is relevant.*
**(a)** Which of the three comes from the token doing the looking, and which come from the tokens being looked at?
**(b)** Why do query and key share the output dimension `k` while value has its own `v`?
> **(a)** The **query** comes from `x_i`, the one doing the looking; **keys and values** come from every `z_j` being looked at. **(b)** Query and key are **compared** — their dot product is the relevance score — so they must live in the same space. The value is never compared with anything; it is only **mixed**, so its dimension is free and sets the output width. *The comparison/transport distinction is the whole mechanism; naming q, K, V without it is the FP-9 failure in attention's clothing.*

### QB-CV-0012 · [OXFORD] · compare, with the cost named · `08_Transformers` — "CNNs to Transformers" / "Attention" · not yet asked
A convolution looks at a **fixed local window**; attention lets every token look at **every other token**.
**(a)** What does attention buy that stacking more conv layers does not?
**(b)** Name the price, and say which quantity it scales with.
> **(a)** A **constant-length path** between any two positions — a conv net needs depth to connect distant pixels, and each extra hop is another factor in the gradient product, which is the vanishing-gradient story. Attention reaches across the image in one step. **(b)** Cost is **quadratic in the number of tokens** (every token attends to every token), which is precisely why ViT patches first. *Pairs with the DL4H residual/vanishing-gradient anchor: both are about path length between distant things.*
