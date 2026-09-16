# DL4H — Problem Sheet 2: Worked Solutions
> Source: Google Drive file 10NH8aLQ4kEDBk5WJLeb02fUE3auO56AQ · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Problem Sheet 2: Worked Solutions 

|  |
| :-: |
| [**Page 1**]() |

Deep Learning in Healthcare

Hilary Term 2026

Problem Sheet 2: Worked Solutions

Inductive Biases, Uncertainty & Transfer Learning

Important: These solutions are for instructor use only. Provide to students only after submis-

sion deadlines.

1 Inductive Biases and Geometric Equivariance in Medical Im-

age Analysis

(a) Translation equivariance in CNNs.

(i) Why convolution is translation equivariant:

Convolution applies the same kernel weights at every spatial location. If we shift the

input by δ pixels, each local patch that the kernel sees is the same as before, just at

a different location. Therefore, the output is also shifted by δ pixels.

Formally: (k∗Tδ\[x\])\[i, j\] = Pm,n k\[m, n\]·x\[i−m+δx,j−n+δy\]=(k∗x)\[i+δx,j+δy\] =

Tδ\[k ∗ x\]\[i, j\]

Implications for Task A (segmentation):

Translation equivariance is desirable. If a lung nodule appears at a different location

in the image, the segmentation mask should shift correspondingly. The network

doesn’t need to re-learn what a nodule looks like at each possible position. It learns

location-independent features that transfer across the image.

Implications for Task B (classification with geometric variability):

Translation equivariance is insufficient and potentially problematic. The network’s

intermediate representations shift when the input shifts, but the classification target

(cardiomegaly: yes/no) should be invariant to patient positioning. The network must

learn to be robust to these variations from data, which requires seeing many examples

of the same pathology at different positions. Inefficient use of limited medical data.

Additionally, if training data comes from hospitals with consistent positioning but

test data has more variability, the equivariant features may not generalise well.

(ii) Effect of global average pooling:

Global average pooling (GAP) computes the spatial mean of each feature map:

GAP(F)\[c\] =

1

H × W

X

i,j

F\[c, i, j\]

This converts translation equivariance into translation invariance. If the input shifts,

the feature maps shift (equivariance), but summing over all positions produces the

same scalar value (invariance).

Appropriate for classification:

For Task B, we want the output to be the same regardless of where the heart appears

in the image. GAP achieves this by discarding spatial information entirely after the

convolutional layers have extracted features.

-----

|  |
| :-: |
| [**Page 2**]() |

Deep Learning in Healthcare

Hilary Term 2026

Inappropriate for segmentation:

For Task A, we need to output a mask that preserves spatial correspondence with

the input. GAP destroys exactly the information we need: where in the image each

feature was detected. Segmentation networks like UNet therefore avoid GAP and

instead use transposed convolutions or upsampling to preserve spatial structure.

Trade-off: GAP provides perfect translation invariance but loses all spatial infor-

mation. This is acceptable when the task is purely about what is in the image, but

fails when we also need to know where.

(⋆ Challenge) Proof and characterisation:

Proof of convolution equivariance:

Let Tδ be the translation operator: (Tδx)\[i\] = x\[i − δ\] (in 1D for simplicity).

For discrete convolution (k ∗ x)\[i\] = Pm k\[m\] · x\[i − m\]:

(k ∗ Tδx)\[i\] =

X

m

k\[m\] · (Tδx)\[i − m\] =

X

m

k\[m\] · x\[i − m − δ\]

\= (k ∗ x)\[i − δ\] = Tδ(k ∗ x)\[i\]

Therefore k ∗ Tδ = Tδ ◦ (k∗), i.e., convolution commutes with translation.

Characterisation of translation-equivariant linear operators:

A linear operator L is translation equivariant iff Tδ ◦ L = L ◦ Tδ for all δ.

Claim: The only such operators are convolutions.

Proof sketch: Let L be a linear, translation-equivariant operator. Define k = L(δ0) where

δ0 is the impulse at the origin.

For any input x = Pi x\[i\] · δi (sum of shifted impulses):

L(x) = L

X

i

x\[i\] · Tiδ0

\!

\=

X

i

x\[i\] · L(Tiδ0)

\=

X

i

x\[i\] · TiL(δ0) =

X

i

x\[i\] · Tik = k ∗ x

Thus L is convolution with kernel k = L(δ0). This is the discrete analogue of the contin-

uous result that translation-equivariant linear operators on L2(Rn) are precisely convolu-

tions (via the convolution theorem and Fourier analysis).

(b) Skip connections as an inductive bias.

(i) Assumption encoded by skip connections:

UNet’s skip connections encode the assumption that input and output are spatially

aligned. That is, the feature at encoder position (i, j) is directly relevant to the

output at decoder position (i, j).

More precisely, skip connections assume:

• The input and output share the same coordinate system

• Spatial correspondence is preserved (no geometric transformation between input

and output)

• Fine-grained details from the input should directly inform the output at matching

locations

-----

|  |
| :-: |
| [**Page 3**]() |

Deep Learning in Healthcare

Hilary Term 2026

Medical imaging scenario where this is violated:

Image registration / atlas alignment: Given a patient’s brain MRI, predict the defor-

mation field needed to align it to a standard atlas. The input is the patient image;

the output is a displacement field. However, the displacement at position (i, j) de-

pends on the global relationship between patient and atlas anatomy, not just the

local appearance at (i, j).

Cross-modality synthesis: Predicting a CT image from an MRI where the patient

moved between acquisitions. The MRI voxel at (i, j, k) may not correspond to the

same anatomical location in the target CT.

Multi-view reconstruction: Generating a sagittal view from an axial slice. The spatial

axes are permuted, so encoder position (i, j) has no direct correspondence to decoder

position (i, j).

(ii) Analysis of removing skip connections:

Optimisation landscape:

Without skip connections, gradients must flow through the entire encoder-bottleneck-

decoder path (∼20+ layers). This creates:

• Vanishing gradients: Each layer multiplicatively attenuates gradients, making

early encoder layers hard to train

• Longer path to supervision: The loss signal must propagate further, slowing

convergence

• More complex optimisation surface: Deeper networks without shortcuts have

more saddle points and poor local minima

Skip connections provide “gradient highways” that allow direct error signal to early

layers, dramatically improving trainability.

What the network must learn:

With skip connections, the decoder receives:

• High-resolution spatial details from encoder (via skip connections)

• Semantic/contextual information from bottleneck

The decoder only needs to learn how to combine these; a relatively simple task.

Without skip connections, the network must:

• Compress all relevant spatial information into the bottleneck (lossy)

• Learn to reconstruct fine spatial details from compressed representation

• Essentially learn an inverse mapping that “hallucinates” high-frequency details

This is much harder. The bottleneck becomes an information bottleneck in the

technical sense: I(X;Zbottleneck) must be high enough to reconstruct the output, but

the bottleneck’s limited capacity makes this challenging.

Conclusion: Removing skip connections forces the network to solve a harder prob-

lem (reconstruction from lossy compression) with a harder optimisation landscape

(vanishing gradients). A deeper bottleneck adds parameters but doesn’t fundamen-

tally change this difficulty.

(c) Spatial Transformer Networks.

(i) Data augmentation vs STN:

Data augmentation:

• Applies random transformations to training data

• Forces the network to learn features invariant to these transformations

• The invariance is implicit; learned through exposure to varied examples

-----

|  |
| :-: |
| [**Page 4**]() |

Deep Learning in Healthcare

Hilary Term 2026

• Requires the network to “use up” capacity learning invariance

Spatial Transformer Network:

• Learns to predict the transformation present in each input

• Applies the inverse transformation to canonicalise the input

• Downstream layers see standardised inputs (e.g., centred, upright)

• The invariance is explicit; built into the architecture

Key difference for unseen transformations:

With data augmentation, if test images contain transformations not seen during

training (e.g., 45° rotation when only trained on ±15°), the network may fail because

it never learned features invariant to that transformation.

An STN can potentially extrapolate: the localisation network learns to predict trans-

formation parameters as a continuous function of the input. If this function gen-

eralises smoothly, the STN can handle 45° rotations by predicting θ = −45 and

applying the inverse, even if it only saw smaller rotations during training.

Caveats:

• STN extrapolation depends on the localisation network generalising

• Very large or unusual transformations may still fail

• STN adds complexity and can be harder to train

• STN learns invariance, not equivariance; unsuitable for tasks requiring equivari-

ant outputs

(ii) Restricting to rigid transformations:

A 2D affine transformation is:

x/

y/

\=

a b

c d

x

y

\+

tx

ty

The localisation network outputs 6 parameters: (a, b, c, d, tx,ty).

A rigid transformation (rotation + translation) has the form:

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

Modified parameterisation:

Have the localisation network output only 3 parameters: (θ, tx,ty).

Then construct the transformation matrix:

a = cosθ, b = −sinθ, c = sinθ, d = cosθ

This ensures:

• No scaling: a2 + c2 = cos2 θ + sin2 θ = 1

• No shear: The matrix is orthogonal

• Only rotation and translation are possible

Implementation: Add a layer after the localisation network that computes (cosθ,−sinθ, tx,sinθ,cosθ, ty)

from the raw outputs (θ, tx,ty), then reshape into the 2 × 3 affine matrix.

(⋆ Challenge) Jacobian derivation:

Rigid transformation:

x

/

\= R(θ)x + t =

cosθ −sinθ

sinθ

cosθ

x

y

\+

tx

ty

-----

|  |
| :-: |
| [**Page 5**]() |

Deep Learning in Healthcare

Hilary Term 2026

Jacobian with respect to θ:

∂x/

∂θ

\=

∂R(θ)

∂θ

x =

−sinθ −cosθ

cosθ

−sinθ

x

y

\=

−xsinθ − y cosθ

xcosθ − y sinθ

This can be written more elegantly as:

∂x/

∂θ

\= R(θ + 90)x = R(θ)

−y

x

Jacobian with respect to t:

∂x/

∂tx

\=

1

0

,

∂x/

∂ty

\=

0

1

Why this avoids singularities:

Alternative rotation representations can have singularities:

• Euler angles (in 3D): Gimbal lock occurs when two axes align, making the Jacobian

rank-deficient

• Direct matrix elements: Constraining a2 +b2 = 1 via normalisation creates singular-

ities when (a, b) → (0,0)

The angle parameterisation θ is singularity-free for 2D rotations because:

• θ ∈ \[0,2π) smoothly covers all rotations

• ∂R/∂θ is never zero (rotation rate is constant)

• The mapping θ 7→ R(θ) is a diffeomorphism onto SO(2)

The only subtlety is the discontinuity at θ = 0 ≡ 2π, but this is typically handled by

using sinθ,cosθ as network outputs and computing θ = atan2(sinθ,cosθ), or by keeping

θ unbounded and relying on the periodicity of sin,cos.

In 3D, quaternions or the 6D rotation representation (Zhou et al., 2019) are preferred to

avoid gimbal lock.

(d) Architectural choices for clinical deployment.

Option 1: Standard CNN with aggressive data augmentation

Approach: Apply random rotations, translations, scaling, and cropping during training to

simulate the variability in portable X-rays.

Pros:

• Simple to implement; no architectural changes

• Well-understood; extensive literature on augmentation strategies

• No additional parameters or computational cost at inference

Cons:

• Network must “waste” capacity learning invariance implicitly

• May not generalise to transformations outside the augmentation distribution

• Requires careful tuning of augmentation hyperparameters

• Sample inefficient: needs many examples to learn invariance

-----

|  |
| :-: |
| [**Page 6**]() |

Deep Learning in Healthcare

Hilary Term 2026

Failure modes: If portable X-rays have geometric distortions (e.g., oblique angles) not

covered by augmentation, the model may fail silently with confident but wrong predictions.

Option 2: CNN with STN module

Approach: Prepend an STN that learns to canonicalise inputs (centre, rotate upright,

normalise scale) before the classifier.

Pros:

• Explicit geometric invariance built into architecture

• Can potentially extrapolate to unseen transformations

• More sample-efficient (invariance is architectural, not learned from data)

• Interpretable: can visualise the learned transformation

Cons:

• Harder to train (localisation network must learn without direct supervision)

• Additional computational cost

• May learn spurious canonicalisation (e.g., always crop to centre, missing peripheral

pneumothorax)

• STN failures can cause catastrophic misalignment

Failure modes: If the localisation network makes a large error, the canonicalised image

may be severely distorted, causing confident misclassification. Failure may be hard to

detect without visualising the transformation.

Option 3: Test-time augmentation (TTA) with uncertainty estimation

Approach: Train a standard CNN. At test time, apply multiple geometric transformations

to each input, run inference on each, and aggregate predictions.

Pros:

• Simple architecture; augmentation only at inference

• Provides uncertainty estimate (variance across augmented predictions)

• Can detect when geometric variation affects predictions (high variance = uncertain)

• No additional training complexity

Cons:

• Higher inference cost (multiple forward passes)

• Still relies on the augmentation distribution being appropriate

• May not improve accuracy if the underlying model is weak

Failure modes: If all augmented versions agree on a wrong answer, TTA provides false

confidence. However, this is detectable if the variance is monitored.

Recommendation:

For clinical deployment of pneumothorax detection from portable X-rays, I would recom-

mend Option 3 (TTA with uncertainty) combined with moderate training augmen-

tation, for the following reasons:

(a) Safety: The built-in uncertainty estimate allows flagging cases where geometric vari-

ation affects the prediction, routing them to human review.

(b) Interpretability: Clinicians can see predictions across augmented versions, building

trust.

-----

|  |
| :-: |
| [**Page 7**]() |

Deep Learning in Healthcare

Hilary Term 2026

(c) Simplicity: Easier to validate and debug than an STN.

(d) Failure detection: High variance signals potential problems, unlike STN failures

which may be silent.

The STN (Option 2) could be superior if training data is very limited and the geometric

variations are well-characterised, but the risk of silent failures makes it less suitable for

safety-critical deployment without extensive validation.

2 Dropout and Uncertainty Quantification in Medical Imaging

(a) Dropout as regularisation.

(i) During training with dropout probability p, each neuron is zeroed independently with

probability p. This means only a fraction (1 − p) of neurons are active on average.

Why scaling by 1/(1 − p) is necessary:

Let a be a neuron’s activation before dropout. During training:

E\[output\] = (1 − p) ·

a

1 − p

\+ p · 0 = a

The scaling ensures the expected output magnitude remains a, matching what the

next layer expects.

Without scaling:

During training, the expected output would be (1 − p) · a. At test time (dropout

disabled), the output would be a. This mismatch means:

• Test-time activations are 1/(1 − p)=2× larger (for p = 0.5)

• All downstream layers receive inflated inputs

• Softmax outputs become overconfident (sharper distributions)

• Model predictions are systematically wrong

Alternative: Inverted dropout (used in practice) scales during training by 1/(1−

p), so no adjustment is needed at test time.

(ii) Why dropout is problematic in early convolutional layers:

1\. Spatial correlation undermines dropout’s effect:

In early conv layers, feature maps have high spatial resolution (e.g., 256×256). Ad-

jacent pixels are highly correlated because they represent nearby image regions.

If dropout zeros a neuron at position (i, j), its neighbours (i±1,j ±1) contain nearly

identical information. The network can easily “fill in” the missing activation from

neighbours, defeating dropout’s regularisation purpose.

In FC layers, neurons represent independent features with no spatial structure, so

dropping one neuron genuinely removes unique information.

2\. Loss of critical low-level features:

Early layers learn fundamental features (edges, textures) that are essential for all

downstream processing. Randomly dropping these features during training can:

• Destabilise learning of edge detectors

• Create inconsistent gradient signals

• Force the network to learn redundant low-level features (wasteful)

-----

|  |
| :-: |
| [**Page 8**]() |

Deep Learning in Healthcare

Hilary Term 2026

3\. Gradient flow disruption:

Early layers already receive weaker gradients (further from loss). Adding dropout

noise to these weak signals can impair learning.

Alternative for conv layers: Spatial dropout (drop entire feature maps) or Drop-

Block (drop contiguous regions) are more effective because they remove spatially

coherent information that cannot be recovered from neighbours.

(b) Monte Carlo Dropout for uncertainty estimation.

(i) How variance estimates uncertainty:

With dropout enabled at test time, each forward pass uses a different random subset

of neurons, effectively creating a different “thinned” network. Running T = 50 passes

produces T different predictions:

{ˆp1, ˆp2,..., ˆp50}

The variance across these predictions reflects how sensitive the model is to which

neurons are active:

• Low variance: All thinned networks agree → prediction is robust

• High variance: Different subnetworks disagree → prediction is uncertain

Connection to Bayesian inference:

In Bayesian deep learning, we want to compute:

p(y|x,D) =

Z

p(y|x,θ)p(θ|D)dθ

This integral over all possible weight configurations θ is intractable.

Gal & Ghahramani (2016) showed that dropout training approximately minimises

the KL divergence to a variational posterior q(θ). Each dropout mask samples a

different θ from this approximate posterior.

MC Dropout approximates the Bayesian integral:

p(y|x,D) ≈

1

T

T

X

t=1

p(y|x,

ˆ

θt)

where ˆθt is the “thinned” network from dropout mask t.

The variance of predictions estimates the epistemic uncertainty: uncertainty about

which weights are correct given finite training data.

(ii) Image 1: Mean = 0.73, SD = 0.04

Image 2: Mean = 0.71, SD = 0.31

Both would be classified as grade 2 (moderate diabetic retinopathy) based on the

mean prediction exceeding 0.5. However, the clinical interpretation should differ

substantially:

Image 1 (low uncertainty):

• All 50 subnetworks consistently predict ∼0.73 (range roughly 0.65–0.81)

• The model is confident in its prediction

• Clinical action: Can be triaged automatically with high confidence

• The prediction is likely reliable

Image 2 (high uncertainty):

-----

|  |
| :-: |
| [**Page 9**]() |

Deep Learning in Healthcare

Hilary Term 2026

• Predictions vary widely (range roughly 0.09–1.0, spanning nearly all grades)

• Different subnetworks strongly disagree

• Clinical action: Should be flagged for ophthalmologist review

• Possible reasons for uncertainty:

– Image quality issues (blur, artefacts)

– Unusual pathology not well-represented in training data

– Borderline case between severity grades

Key insight: The mean prediction alone (0.71 vs 0.73) suggests similar confidence.

The uncertainty estimate reveals that Image 2’s prediction is essentially unreliable;

the model is “guessing.” A screening system using only mean predictions would treat

these identically, potentially missing a case requiring expert review.

(c) Aleatoric vs epistemic uncertainty.

Scenario 1: Images from a hospital with different scanner characteristics

This primarily represents epistemic uncertainty.

Reasoning:

• The model has not seen images with these characteristics during training

• The uncertainty arises from the model’s lack of knowledge about this image type

• With more training data from this scanner, the model could learn to handle these

images

• MC Dropout would show high variance: different subnetworks extrapolate differently

to unseen input distributions

Implications for improvement:

• Collect labelled data from the new hospital/scanner

• Fine-tune or retrain to include this domain

• Uncertainty should decrease as the model gains experience with this image type

• Domain adaptation techniques could help bridge the distribution gap

Scenario 2: Images with poor focus or lens artefacts

This primarily represents aleatoric uncertainty.

Reasoning:

• The relevant diagnostic information (retinal vessels, microaneurysms) is physically

obscured

• No amount of training data can recover information that isn’t in the image

• Even a perfect model cannot reliably grade DR from a blurry image

• This is inherent noise in the data, not model ignorance

Implications for improvement:

• Adding more training data will not reduce this uncertainty

• Solution requires improving data acquisition (better cameras, quality control)

• The model should learn to detect poor quality images and flag them for re-acquisition

• A well-calibrated model should output high uncertainty for these images regardless

of its prediction

Practical distinction:

To determine whether uncertainty is epistemic or aleatoric:

-----

|  |
| :-: |
| [**Page 10**]() |

Deep Learning in Healthcare

Hilary Term 2026

• Train with 10× more data from similar distributions

• If uncertainty decreases → was epistemic

• If uncertainty remains high → is aleatoric

In practice, most real-world uncertainty is a mixture. The scanner difference might also

introduce some aleatoric uncertainty (e.g., different noise characteristics), and poor-quality

images from underrepresented populations might have an epistemic component.

(d) Clinical decision-making under uncertainty.

Should triage use uncertainty estimates?

Yes, incorporating uncertainty estimates significantly improves clinical safety. Using pre-

dicted probability alone is insufficient.

Concrete example:

Consider two patients, both predicted “normal” with P(normal) = 0.85:

Patient A: MC Dropout SD = 0.03

• All 50 subnetworks agree: consistently predict 0.82–0.88

• High confidence in “normal” classification

• Safe to clear automatically

Patient B: MC Dropout SD = 0.25

• Predictions range from 0.35 to 1.0

• Some subnetworks predict DR with high probability

• Mean happens to be 0.85, but this masks disagreement

• Should be reviewed by ophthalmologist

Using probability alone, both patients are cleared. Patient B’s potential DR could be

missed.

Recommended triage logic:

(a) Clear automatically only if: P(normal) \> 0.9 AND uncertainty \< 0.1

(b) Flag for review if: uncertainty \> 0.2 regardless of predicted class

(c) This catches cases where the model is uncertain even if the mean prediction seems

confident

Explanations for elevated uncertainty in patients over 80:

Explanation 1 (Training data \[epistemic\]):

The training set of 35,000 images from 3 hospitals may underrepresent elderly patients:

• Elderly patients may be less likely to attend screening

• The 3 hospitals may serve younger demographics

• Result: Model has seen fewer examples of elderly retinas

• The model is uncertain because it lacks experience with this subpopulation

• Solution: Collect more training data from elderly patients; uncertainty should de-

crease

Explanation 2 (Clinical characteristics \[potentially aleatoric\]):

Elderly patients have genuinely different retinal characteristics:

• Age-related macular changes (drusen, pigment changes)

-----

|  |
| :-: |
| [**Page 11**]() |

Deep Learning in Healthcare

Hilary Term 2026

• Cataracts causing image haziness

• More comorbidities (glaucoma, hypertensive retinopathy) that complicate DR as-

sessment

• Atypical presentations of DR in elderly patients

These factors make the classification task inherently harder:

• Features that indicate DR in younger patients may be confounded by age-related

changes

• The “ground truth” itself may be more ambiguous for elderly patients

• Solution: Some uncertainty is appropriate and irreducible; elderly patients may

genuinely warrant more careful human review

Distinguishing the explanations:

If the elevated uncertainty is epistemic (Explanation 1), adding elderly patients to the

training set should reduce it. If it’s aleatoric (Explanation 2), uncertainty will remain

elevated even with more data, reflecting genuine diagnostic difficulty. In practice, both

factors likely contribute.

Clinical implication: Rather than viewing elevated uncertainty in elderly patients as a

model failure, it may be appropriate to set age-specific triage thresholds that route more

elderly patients to human review, acknowledging the inherent complexity of their cases.

3 Transfer Learning in Medical Image Analysis (Optional)

(a) Feature transferability and fine-tuning.

Feature hierarchy and transferability:

Early layers learn low-level visual features (edge detectors, colour gradients, texture

elements). These are highly generic and domain-independent. An edge is an edge whether

it occurs at the boundary of a car or a skin lesion. They are strongly transferable to

dermatoscopy.

Middle layers learn mid-level features (combinations of edges forming shapes, texture

patterns, part-like structures). These are partially transferable: circular and blob-like

patterns may be relevant to dermatoscopy, but features specific to natural images (e.g.,

fur textures) are less useful.

Late layers learn high-level, task-specific features (object-level detectors like “dog face,”

“car wheel”). These are largely not transferable and must be retrained. Transferability

decreases with depth.

Strategy A: Fixed feature extractor. Freeze all convolutional layers, train only a new

classification head.

• Very few trainable parameters, so minimal overfitting risk on 500 images

• But late-layer features are optimised for ImageNet, not dermatoscopy; performance

is capped by how well these features happen to represent the target domain

Strategy B: Full end-to-end fine-tuning. Initialise from pretrained weights, train

everything.

• All layers can adapt, potentially higher accuracy ceiling

-----

|  |
| :-: |
| [**Page 12**]() |

Deep Learning in Healthcare

Hilary Term 2026

• But ∼25M trainable parameters with only 500 images creates severe overfitting risk;

early layers may lose useful generic features through unnecessary updates

Strategy C: Progressive unfreezing. First train only the head, then gradually unfreeze

deeper layers.

• Addresses the key problem with Strategy B: at the start of training, the randomly ini-

tialised head produces random gradients. If deeper layers are unfrozen immediately,

these random gradients corrupt useful pretrained features (catastrophic forgetting)

• By training the head first, gradients become informative before deeper layers are

exposed to them

• Can use smaller learning rates for earlier layers (“discriminative learning rates”)

With only 500 images, Strategy A is the safest starting point. Strategy C offers the best

balance if Strategy A’s performance is insufficient.

Why a large learning rate (10-2) causes accuracy to collapse:

With pretrained weights, a learning rate designed for training from scratch is far too

large. The large weight updates destroy the carefully learned feature representations.

The network “forgets” its ImageNet knowledge and effectively restarts from scratch. With

only 500 images, it cannot re-learn good features, so accuracy drops sharply. It partially

recovers as the network re-learns some features, but these are inferior to the originals

(learned from 1.2M images).

Fine-tuning requires a much smaller learning rate (typically 10-4 to 10-5) to make incre-

mental adjustments rather than overwriting the pretrained weights.

(b) Source model selection and clinical deployment.

Analysis of each source model:

ImageNet (1.2M natural images): Low domain similarity to dermatoscopy, but very

large dataset produces excellent generic low- and mid-level features. Good baseline;

early/mid features transfer well, late features need retraining.

Model P (200K chest X-rays): Both are medical images, but chest X-rays are greyscale,

low-contrast radiographs while dermatoscopy images are high-resolution colour photographs.

Low-level features tuned for greyscale radiographs may be less useful than ImageNet’s

colour-aware features. Likely worse than ImageNet despite being “medical.”

Model Q (100K dermatoscopy images): Very high domain similarity: same imaging

modality, same tissue type, closely related task. Features at all levels (pigment patterns,

border characteristics, colour variegation) are directly relevant. Almost certainly the best

choice.

Ranking: Model Q ≫ ImageNet \> Model P. The key insight is that “medical” does

not mean “similar.” Domain similarity should be assessed by visual characteristics, not

by the broad category.

When transfer can hurt (negative transfer):

• Source model has learned to suppress features important for the target task (e.g.,

ImageNet models may learn colour invariance, but colour is diagnostically critical in

dermatoscopy)

• Mismatched batch normalisation statistics cause large activation mismatches early

in fine-tuning

• Very small target dataset with full fine-tuning leads to rapid overfitting

-----

|  |
| :-: |
| [**Page 13**]() |

Deep Learning in Healthcare

Hilary Term 2026

Addressing the clinician’s concern (“trained on dogs and cars”):

The model does not transfer knowledge about dogs and cars. What transfers are generic

perceptual skills: edge detection, texture analysis, colour gradient detection: analogous

to how a medical student who studied general biology develops visual pattern recognition

skills that transfer to dermatology. The 1000-way ImageNet classification head is discarded

entirely; high-level object concepts are overwritten during fine-tuning. The final model’s

decision boundaries are determined entirely by the dermatoscopy training data.

Analogy: Transfer learning transfers perceptual skills, not diagnostic knowledge.

However, rigorous validation is still essential before deployment: external validation on

unseen hospitals/scanners, subgroup analysis across skin tones and lesion subtypes (Im-

ageNet underrepresents dark skin tones, which may introduce biases), calibration assess-

ment, and comparison with dermatologist performance.

Remark: These solutions demonstrate the core principles underlying modern deep learning

for healthcare. Inductive biases (from translation equivariance in CNNs to spatial alignment as-

sumptions in UNet’s skip connections) determine what models can learn efficiently from limited

data. Spatial Transformer Networks offer explicit geometric invariance for handling acquisition

variability. Uncertainty quantification through MC Dropout enables safer deployment by iden-

tifying predictions that warrant human review. Transfer learning is the dominant paradigm in

medical image analysis, where understanding what transfers across domains (and what does

not) is essential for building reliable systems from limited labelled data.
