# DL4H — Problem Sheet 2: Student Solutions
> Source: Google Drive file 158nasuCSd8-KGM1CcDovMGTDI5sBulF3 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Problem Sheet 2 – Student Solutions 

|  |
| :-: |
| [**Page 1**]() |

Deep Learning in Healthcare

Hilary Term 2026

Problem Sheet 2 – Student Solutions

Inductive Biases, Uncertainty & Transfer Learning

This guide provides key results and concise explanations for each question. Use it to check your

own working and to fill in any gaps in understanding.

1 Inductive Biases and Geometric Equivariance in Medical Im-

age Analysis

(a) Translation equivariance in CNNs.

(i) Convolution applies the same kernel at every spatial location. Shifting the input by

δ pixels shifts the output by δ pixels.

Task A (segmentation): Translation equivariance is desirable. If a lung nodule

shifts in the image, the segmentation mask should shift correspondingly.

Task B (classification with geometric variability): Translation equivariance is

insufficient. The classification target (cardiomegaly: yes/no) should be invariant to

positioning, but equivariant features shift with the input. The network must learn

robustness from data, which is sample-inefficient.

(ii) Global average pooling (GAP) computes the spatial mean of each feature map:

GAP(F)\[c\] =

1

H × W

X

i,j

F\[c, i, j\]

This converts translation equivariance into translation invariance.

Appropriate for classification (Task B): discards spatial information, which is

what we want.

Inappropriate for segmentation (Task A): destroys the spatial correspondence

needed to produce a mask. Segmentation networks like UNet avoid GAP and instead

use upsampling to preserve spatial structure.

(⋆ Challenge) Proof and characterisation:

Proof sketch: Let Tδ be the translation operator. For convolution (k ∗x)\[i\] = Pm k\[m\]·

x\[i − m\]:

(k ∗ Tδx)\[i\] =

X

m

k\[m\] · x\[i − m − δ\]=(k ∗ x)\[i − δ\] = Tδ(k ∗ x)\[i\]

Characterisation: The only linear, translation-equivariant operators are convolutions.

This follows by expressing any input as a sum of shifted impulses and using linearity plus

equivariance.

(b) Skip connections as an inductive bias.

-----

|  |
| :-: |
| [**Page 2**]() |

Deep Learning in Healthcare

Hilary Term 2026

(i) UNet’s skip connections encode the assumption that input and output are spatially

aligned: the feature at encoder position (i, j) is directly relevant to the output at

decoder position (i, j).

Scenario where this is violated: Image registration (predicting a deformation

field), where the displacement at (i, j) depends on the global relationship between

patient and atlas anatomy, not just local appearance. Cross-modality synthesis with

patient movement is another example.

(ii) Without skip connections, gradients must traverse the entire encoder-bottleneck-

decoder path, causing vanishing gradients. Furthermore, the bottleneck must com-

press all relevant spatial information (lossy), and the decoder must reconstruct fine

details from this compressed representation. With skip connections, the decoder re-

ceives high-resolution details directly and only needs to learn how to combine them

with semantic information from the bottleneck. Removing skip connections forces a

harder learning problem with a harder optimisation landscape.

(c) Spatial Transformer Networks.

(i) Data augmentation: applies random transformations during training; invariance

is implicit, learned through exposure. If test images contain transformations not seen

during training, the network may fail.

STN: learns to predict and invert the transformation, canonicalising the input; in-

variance is explicit, built into the architecture. The STN can potentially extrapolate

to unseen transformations if the localisation network generalises smoothly.

Caveats: STNs are harder to train, learn invariance (not equivariance), and locali-

sation failures can cause catastrophic misalignment.

(ii) A rigid transformation (rotation + translation) has the form:

x/

y/

\=

cosθ −sinθ

sinθ

cosθ

x

y

\+

tx

ty

The localisation network outputs only 3 parameters (θ, tx,ty) instead of the full 6

affine parameters. The rotation matrix is constructed from θ via cos and sin, ensuring

orthogonality (no scaling or shear).

(⋆ Challenge) Jacobian derivation:

The Jacobian with respect to θ is:

∂x/

∂θ

\=

−sinθ −cosθ

cosθ

−sinθ

x

y

The Jacobian with respect to t is the identity. The angle parameterisation is singularity-

free for 2D rotations because θ 7→ R(θ) smoothly covers all of SO(2) and ∂R/∂θ is never

zero. In 3D, quaternions or the 6D representation (Zhou et al., 2019) are preferred to

avoid gimbal lock.

(d) Architectural choices for clinical deployment.

Three reasonable options exist:

Option 1: Standard CNN with data augmentation. Simple to implement and no

extra inference cost, but invariance is implicit, sample-inefficient, and may not generalise

to unseen transformations.

-----

|  |
| :-: |
| [**Page 3**]() |

Deep Learning in Healthcare

Hilary Term 2026

Option 2: CNN with STN module. Provides explicit geometric invariance and

can extrapolate, but is harder to train and STN failures can cause silent, catastrophic

misalignment.

Option 3: Test-time augmentation (TTA) with uncertainty estimation. Runs

multiple geometric transformations at inference and aggregates predictions. The variance

across predictions provides an uncertainty estimate.

Recommendation: For clinical deployment of pneumothorax detection from portable X-

rays, Option 3 (TTA with uncertainty) combined with moderate training augmentation is

often preferred. The built-in uncertainty estimate allows flagging of cases where geometric

variation affects the prediction, routing them to human review. It is also simpler to

validate and debug than an STN.

2 Dropout and Uncertainty Quantification in Medical Imaging

(a) Dropout as regularisation.

(i) During training with dropout probability p, only a fraction (1 − p) of neurons are

active. Scaling by 1/(1 − p) ensures the expected output magnitude remains un-

changed:

E\[output\] = (1 − p) ·

a

1 − p

\+ p · 0 = a

Without scaling, test-time activations would be 1/(1 − p) times larger than during

training, causing systematically wrong predictions. In practice, “inverted dropout”

applies the scaling during training so no adjustment is needed at test time.

(ii) In early convolutional layers, adjacent pixels are highly correlated. If dropout zeros

a neuron at position (i, j), its neighbours contain nearly identical information, so the

network can easily fill in the gap. Dropout’s regularisation effect is therefore weak.

Better alternatives for conv layers: Spatial dropout (dropping entire feature

maps) or DropBlock (dropping contiguous regions) remove spatially coherent infor-

mation that cannot be recovered from neighbours.

(b) Monte Carlo Dropout for uncertainty estimation.

(i) With dropout enabled at test time, each forward pass uses a different random subset

of neurons. Running T = 50 passes gives T predictions. Low variance means all

subnetworks agree (robust prediction); high variance means they disagree (uncertain

prediction).

Gal & Ghahramani (2016) showed this approximates Bayesian inference: each dropout

mask samples from an approximate posterior over weights. The variance estimates

epistemic uncertainty, i.e., uncertainty about which weights are correct given finite

training data.

(ii) Image 1 (mean 0.73, SD 0.04): all subnetworks consistently predict grade 2. The

model is confident and the prediction is likely reliable.

Image 2 (mean 0.71, SD 0.31): predictions vary widely (roughly 0.09 to 1.0). Differ-

ent subnetworks strongly disagree. This case should be flagged for ophthalmologist

review.

Key insight: The mean predictions are nearly identical (0.71 vs 0.73), but the

uncertainty reveals that Image 2’s prediction is essentially unreliable. A system

using only mean predictions would treat these identically.

-----

|  |
| :-: |
| [**Page 4**]() |

Deep Learning in Healthcare

Hilary Term 2026

(c) Aleatoric vs epistemic uncertainty.

Scenario 1 (different scanner characteristics): Primarily epistemic uncertainty.

The model lacks knowledge about this image type. Adding training data from the new

scanner should reduce uncertainty.

Scenario 2 (poor focus or lens artefacts): Primarily aleatoric uncertainty. The

diagnostic information is physically obscured. No amount of training data can recover

information that is not in the image.

Practical test: Train with 10× more data from similar distributions. If uncertainty

decreases, it was epistemic; if it remains high, it is aleatoric. In practice, most real-world

uncertainty is a mixture of both types.

(d) Clinical decision-making under uncertainty.

Yes, triage should use uncertainty estimates. Two patients both predicted “normal” with

P(normal) = 0.85 may have very different uncertainty: one with SD 0.03 (all subnetworks

agree, safe to clear) and one with SD 0.25 (subnetworks disagree, should be reviewed).

Recommended logic: Clear automatically only if both the predicted probability is high

and uncertainty is low. Flag for review if uncertainty is high, regardless of the predicted

class.

Elevated uncertainty in patients over 80 has two plausible explanations:

(a) Epistemic: Elderly patients may be underrepresented in training data. Collecting

more examples from this subpopulation should reduce uncertainty.

(b) Aleatoric: Age-related retinal changes (drusen, cataracts, comorbidities) make clas-

sification genuinely harder. Some uncertainty is appropriate and irreducible.

If adding elderly training data reduces uncertainty, it was epistemic. If it persists, it is

aleatoric and age-specific triage thresholds may be warranted.

3 Transfer Learning in Medical Image Analysis (Optional)

(a) Feature transferability and fine-tuning.

Feature hierarchy: Early layers learn generic low-level features (edges, textures) that

are highly transferable. Middle layers learn mid-level combinations that are partially

transferable. Late layers learn task-specific features (e.g., “dog face”) that are largely not

transferable and must be retrained. Transferability decreases with depth.

Strategy A (fixed feature extractor): Freeze all conv layers, train only a new head.

Very few trainable parameters and minimal overfitting risk on 500 images, but performance

is capped by how well ImageNet features happen to represent dermatoscopy.

Strategy B (full fine-tuning): Train everything from pretrained initialisation. Higher

accuracy ceiling, but ∼25M trainable parameters with only 500 images creates severe

overfitting risk.

Strategy C (progressive unfreezing): Train the head first, then gradually unfreeze

deeper layers. This prevents the randomly initialised head from sending uninformative

gradients into pretrained layers (catastrophic forgetting). Can use smaller learning rates

for earlier layers.

With only 500 images, Strategy A is the safest starting point. Strategy C offers the best

balance if Strategy A is insufficient.

-----

|  |
| :-: |
| [**Page 5**]() |

Deep Learning in Healthcare

Hilary Term 2026

Why a large learning rate (10-2) causes accuracy to collapse: Updates are far too

large and destroy the pretrained feature representations. The network effectively restarts

from scratch and cannot re-learn good features from only 500 images. Fine-tuning requires

much smaller learning rates (typically 10-4 to 10-5).

(b) Source model selection and clinical deployment.

ImageNet (1.2M natural images): Low domain similarity but excellent generic low-

and mid-level features due to dataset size. Good baseline.

Model P (200K chest X-rays): Both are medical images, but chest X-rays are greyscale,

low-contrast radiographs while dermatoscopy images are high-resolution colour photographs.

Features tuned for greyscale radiographs may be less useful than ImageNet’s colour-aware

features. Likely worse than ImageNet despite being “medical.”

Model Q (100K dermatoscopy images): Very high domain similarity; features at all

levels (pigment patterns, border characteristics, colour variegation) are directly relevant.

Almost certainly the best choice.

Ranking: Model Q ≫ ImageNet \> Model P. “Medical” does not mean “similar.”

Domain similarity should be assessed by visual characteristics, not by the broad category.

Addressing the clinician’s concern (“trained on dogs and cars”): The model does

not transfer knowledge about dogs and cars. What transfers are generic perceptual skills:

edge detection, texture analysis, colour gradient detection. The ImageNet classification

head is discarded entirely; high-level concepts are overwritten during fine-tuning. Transfer

learning transfers perceptual skills, not diagnostic knowledge.

Rigorous validation remains essential: external validation on unseen hospitals/scanners,

subgroup analysis across skin tones and lesion subtypes, calibration assessment, and com-

parison with dermatologist performance.
