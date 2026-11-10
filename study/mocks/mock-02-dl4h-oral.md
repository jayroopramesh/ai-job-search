# Mock #2 — [OXFORD] DL4H oral dress rehearsal

**Built 2026-11-10 (D55), unattended. Ready to run on "go".**
Target date: Fri 13 Nov · Real interview: Fri 20 Nov (DL4H, Ana Namburete, Oxford)

## Protocol
Same as `mock-01-aus-oral.md`: **10 items · ~8 minutes · cold · timed · scored /100**, each item plus one follow-up probe, never queued, no arithmetic, read the clock aloud at item 5.

**DL4H only**, and deliberately **healthcare-framed throughout** — the examiner works in medical imaging, so an answer that is correct about deep learning but says nothing about clinical data is a half answer. Several probes exist purely to check he carries the method back to the hospital setting.

**Avoids all five items served 9 Nov** (entropy, L1-vs-L2, lazy learner, vanishing gradients/residual, Naive Bayes) and the archived set (√d_k, BatchNorm, gradient reversal) — this has to be cold.

## Scoring — 10 points per item
| Score | Meaning |
|---|---|
| **10** | Main answer correct **and** probe answered with the mechanism, unprompted. |
| **6** | Main correct, probe gave a label or restatement. **FP-9. Expect it; count them.** |
| **3** | Partial, or correct only once the probe did the work. |
| **0** | Wrong, inverted, or unanswered. |

Log the total **and the 6-count** separately.

---

## The items

**1. Why healthcare is its own problem.** Name three things about medical data that make deep learning harder here than on natural images.
*Probe:* Take the one you think is worst. What does it actually do to the trained model?
<sub>`L1` — "Deep Learning in Healthcare: Unique Data, Unique Challenges"</sub>

**2. Class imbalance, clinically.** A tumour occupies a tiny fraction of the voxels in a scan. What goes wrong if you train on plain accuracy or pixel-wise cross-entropy?
*Probe:* Dice is the usual answer. What is Dice actually measuring, and why does that survive the imbalance when accuracy doesn't?
<sub>`L2` — "Dice Loss: What it optimises (and why)"</sub>

**3. Zero initialisation.** Why can you not initialise all the weights in a layer to zero?
*Probe:* What are all those units doing to each other during backprop — and what is the name for what you've failed to do?
<sub>`L4` — "Zero Initialisation"</sub>

**4. Weight sharing.** A convolutional layer reuses the same filter across the whole image instead of learning separate weights per location. What does that buy, beyond "fewer parameters"?
*Probe:* The deck puts it as — *it is unnecessary for every receptive field to have its own "left ventricle" detector.* Unpack that. What property of the data makes it true, and when would it stop being true?
<sub>`L5` — weight sharing / receptive field</sub>

**5. Receptive field.** What is the receptive field of a unit deep in a CNN, and why does it grow with depth?
*Probe:* Why does that matter for finding something large and diffuse in a scan rather than small and sharp?
<sub>`L5` — receptive field</sub>

**6. Dropout.** What does dropout do during training, and what does it do at test time?
*Probe:* The deck calls it *implicit ensembling with shared parameters.* Why "implicit", and what is the practical problem with real ensembling that this gets around?
<sub>`L7-8` — "Dropout: implicit ensembling with shared parameters" / "combining several models at test time is infeasible in real-time applications"</sub>

**7. Transfer learning.** You have 300 labelled scans. Why does pretraining on a large natural-image dataset help at all, given photographs look nothing like MRI?
*Probe:* Which layers transfer, which don't, and why that asymmetry?
<sub>`L9-10` — "Low-data regimes: Self-Supervised Learning, Transfer Learning, and Domain Adaptation"</sub>

**8. Augmentation, with a clinical catch.** Name two augmentations you'd apply to medical scans — and one you must not. Why is that one dangerous here but harmless on photographs?
*Probe:* What does an unsafe augmentation teach the model, stated as a mechanism rather than "it's wrong"?
<sub>`L9-10` — data augmentation</sub>

**9. Federated learning.** Hospitals cannot pool their data. What does federated learning move between sites instead, and what does that solve?
*Probe:* The deck says the data are decentralised **and heterogeneous**. The second word is doing work — what problem does it create that privacy alone doesn't?
<sub>`L13` — "Problem: Data are decentralised and heterogeneous" / "Cannot be freely centralised"</sub>

**10. Explainability.** A saliency map lights up over the right region. Why is that not proof the model is reasoning correctly?
*Probe:* The deck gives one concrete limitation of saliency maps and one broader caution. Give either, precisely.
<sub>`L16` — "Saliency Maps • Limitation: Noisy gradients" / "Not all explanations are faithful"</sub>

---

## Model answers — for instant grading, do not read aloud before scoring

1. Any three of: scarce labels (expert annotation is expensive), severe class imbalance, privacy/legal limits on pooling, heterogeneity across scanners and sites, label noise and inter-rater disagreement, 3D volumetric data, distribution shift between hospitals. Full marks need the consequence — e.g. scanner heterogeneity → the model learns site-specific artefacts and collapses on a new hospital's machine.
2. Accuracy and pixel-wise CE are dominated by the overwhelming background; predicting "all background" scores superbly while segmenting nothing. Dice measures **overlap between prediction and ground truth on the positive class** — background is not in the numerator, so it cannot be gamed by it.
3. Every unit in the layer computes the same output, receives the same gradient, and updates identically — they stay identical forever, so the layer has the capacity of one unit. The failure is **symmetry breaking**.
4. **Translation equivariance** / the inductive bias that a feature is worth detecting wherever it occurs — plus statistical efficiency, since every location is a training example for the same filter. It stops holding when position itself carries meaning and structure is not translation-invariant (registered images with fixed anatomy, where a location-specific model could legitimately do better).
5. The region of input a unit can see. It grows because each layer composes over the previous layer's outputs, so the window compounds with depth (and faster with pooling/stride). Large diffuse findings need a receptive field big enough to contain the evidence; too small and the unit cannot see the thing it is being asked to call.
6. **Train:** randomly zero units each pass, so no feature can rely on a fixed partner. **Test:** dropout off, whole network used, activations scaled so expected magnitudes match. "Implicit" because the exponentially many thinned sub-networks share one set of weights — you get the ensembling benefit without training or running many models, which the deck notes is infeasible in real time.
7. Early layers learn generic low-level structure — edges, textures, gradients — which is modality-agnostic and genuinely transfers. Later layers encode dataset-specific semantics and transfer poorly, so they are the ones fine-tuned or replaced. The asymmetry is **generic-to-specific along depth**.
8. Safe: small rotations, elastic deformation, intensity/contrast jitter, noise, cropping. **Unsafe: horizontal flipping** (also any label-destroying intensity transform). Flipping is dangerous because anatomy is laterally asymmetric — situs, cardiac position, left/right organ identity — so it teaches the model that a mirrored anatomy is a legitimate sample, destroying the very laterality a clinician relies on. Mechanism, not "it's wrong".
9. **Model updates** — weights or gradients — move; the data never leave the hospital. That solves privacy and the legal barrier to pooling. **Heterogeneity** is the separate problem: sites are non-IID (different scanners, protocols, populations), so naive averaging of updates can degrade or fail to converge; it is a statistical problem, not a privacy one, and privacy-preserving transport does nothing about it.
10. Saliency shows **where** the gradient is large, not **why** a decision was made; it can highlight the right region while the model keys on a confound (a scanner artefact, a marker, a text label correlated with the site). Concrete limitation: **noisy gradients**. Broader caution: **not all explanations are faithful** — the explanation can look right while being a poor account of the computation.

## Result
*(unrun — record total /100, the 6-count, and per-item scores here)*
