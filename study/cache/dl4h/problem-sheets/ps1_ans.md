# DL4H — Problem Sheet 1: Solutions
> Source: Google Drive file 1nFfztScT7a2Hxv8_5lN9GPOyA_sAAajL · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Problem Sheet 1 – Solutions 

|  |
| :-: |
| [**Page 1**]() |

Deep Learning in Healthcare

Hilary Term 2026

Problem Sheet 1 – Solutions

1 Backpropagation for medical diagnosis

(a) Chain rule and backpropagation.

The chain rule expression for ∂L/∂W1 is:

∂L

∂W1

\=

∂L

∂y

·

∂y

∂z2

·

∂z2

∂h

·

∂h

∂z1

·

∂z1

∂W1

where:

• ∂L/∂y: How the loss changes with the prediction

• ∂y/∂z2 = σ′(z2): Derivative of sigmoid at output layer

• ∂z2/∂h = w2: Output layer weights

• ∂h/∂z1 = diag(1z1\>0): Derivative of ReLU (0 or 1 per neuron)

• ∂z1/∂W1 = x: Input features

Backpropagation computes gradients in reverse order because each layer’s gradient de-

pends on the gradient from the layer above. The “error signal” ∂L/∂h computed at the

output is reused when computing gradients for earlier layers. Working backwards allows

each intermediate gradient to be computed exactly once, giving an efficient O(n) algorithm

instead of exponentially redundant recomputation.

(b) Vanishing gradients.

(i) Let σ(z) =

1

1+e−z . Using the quotient rule:

dσ

dz

\=

e−z

(1 + e−z)2

\=

1

1 + e−z

·

e−z

1 + e−z

\= σ(z) ·

1 + e−z − 1

1 + e−z

\= σ(z)(1 − σ(z))

The maximum occurs when σ(z)=0.5 (at z = 0):

max

z

dσ

dz

\= 0.5 × 0.5= 0.25

(ii) When backpropagating through L sigmoid layers, the gradient is multiplied by σ′(zℓ)

at each layer ℓ. Since σ′(z) ≤ 0.25 always:

∂L

∂w1

≤ (0.25)L · |other factors|

For L = 10 layers: (0.25)10 ≈ 10−6. The gradient shrinks exponentially with depth,

making it nearly impossible for early layers to learn. This is the vanishing gradient

problem.

-----

|  |
| :-: |
| [**Page 2**]() |

Deep Learning in Healthcare

Hilary Term 2026

(iii) ReLU has derivative:

d

dz

ReLU(z) =

(

1 if z \> 0

0 if z \< 0

For active neurons (z \> 0), the gradient passes through unchanged (multiplied by 1).

Unlike sigmoid, there is no “squashing” that compounds across layers. The gradient

can flow unattenuated through arbitrarily many layers, enabling training of very deep

networks (50, 100, or 1000+ layers). This was a key enabler for architectures like

ResNets used in medical imaging.

(c) Dead ReLU problem.

(i) With zi = −2.5 \< 0:

hi = ReLU(−2.5) = max(0,−2.5) = 0

By the chain rule:

∂L

∂wi

\=

∂L

∂hi

·

∂hi

∂zi

·

∂zi

∂wi

\=

∂L

∂hi

· 0 · x = 0

The gradient is zero regardless of the upstream error signal.

(ii) If the pre-activation is negative for all training examples, the gradient ∂L/∂wi = 0

for every update. The weights never change during gradient descent. The neuron

contributes nothing to the network output (hi = 0 always) and cannot recover. It is

“dead.” This can occur with poor initialization or if the bias becomes too negative

during training.

(iii) Leaky ReLU has:

LeakyReLU(z) =

(

z

if z \> 0

αz if z ≤ 0

⇒

d

dz

LeakyReLU(z) =

(

1 if z \> 0

α if z ≤ 0

with small α \> 0 (typically 0.01). For zi \< 0:

∂L

∂wi

\=

∂L

∂hi

· α · x ̸= 0

Even when zi \< 0, gradients still flow (scaled by α), allowing weights to update and

potentially recover. Neurons can never become permanently dead.

2 Optimization and ill-conditioned losses

(a) The gradient is:

∇L =

∂L/∂w1

∂L/∂w2

\=

w1

20w2

At w = (1,1)⊤:

∇L =

1

20

The gradient in the w2 direction is 20 times larger than in w1, even though both

coordinates have the same value. This reflects the geometry: the loss surface is much

steeper (higher curvature) in the w2 direction. The contours are elongated ellipses with

the major axis along w1.

-----

|  |
| :-: |
| [**Page 3**]() |

Deep Learning in Healthcare

Hilary Term 2026

(b) The Hessian is:

H =

∂2L/∂w2

1

∂2L/∂w1∂w2

∂2L/∂w2∂w1

∂2L/∂w2

2

\=

1 0

0 20

This is diagonal, so the eigenvalues are λ1 = 1 and λ2 = 20.

The condition number is:

κ =

λmax

λmin

\=

20

1

\= 20

A high condition number makes gradient descent difficult because:

• The optimal step size differs dramatically by direction

• A learning rate appropriate for the flat direction (w1) makes negligible progress

• A learning rate appropriate for the steep direction (w2) causes oscillation or diver-

gence

• GD must use a conservative learning rate, leading to very slow convergence along

the “valley floor”

(c) For convergence in direction i, we need |1 − αλi| \< 1:

−1 \< 1 − αλi \< 1 ⇒ 0 \< αλi \< 2 ⇒ α \<

2

λi

For both directions to converge simultaneously:

α \< min

2

λ1

,

2

λ2

\= min

2

1

,

2

20

\=

2

20

\= 0.1

The maximum stable learning rate is αmax = 0.1, constrained by the high-curvature

w2 direction.

With this learning rate, the effective step in w1 is αλ1 = 0.1 × 1=0.1, meaning we take

very small steps along the valley. Hence slow convergence despite stability.

(d) Momentum maintains a velocity that averages past gradients:

v(t+1) = βv(t) + ∇L(w(t)), w(t+1) = w(t) − αv(t+1)

High-curvature direction (w2): Gradients oscillate in sign as we bounce across the

steep valley walls. When averaged over time, these oscillations partially cancel out, re-

ducing the effective step size and damping oscillations.

Low-curvature direction (w1): Gradients consistently point the same way (toward the

minimum). Averaging reinforces them, effectively increasing the step size in this direction.

Net effect: Momentum acts as a low-pass filter on gradients, i.e., dampening high-

frequency oscillations while amplifying consistent low-frequency signal. This allows faster

progress along the valley floor without diverging across the steep walls.

(e) Adam tracks per-parameter squared gradient averages:

v

(t)

i

\= β2v

(t−1)

i

\+ (1 − β2)(g

(t)

i

)2

and scales updates by 1/

√

vi:

w

(t+1)

i

\= w

(t)

i

− α ·

mi

√

vi + ϵ

-----

|  |
| :-: |
| [**Page 4**]() |

Deep Learning in Healthcare

Hilary Term 2026

High-curvature direction (w2): Gradients are large (∼20), so v2 accumulates large

values. Updates are scaled down by 1/

√

v2, automatically reducing the effective learning

rate.

Low-curvature direction (w1): Gradients are small (∼1), so v1 stays small. Updates

are scaled up by 1/

√

v1, automatically increasing the effective learning rate.

Key difference from momentum: Adam directly normalises step sizes per coordinate

based on gradient magnitude, effectively giving each parameter its own adaptive learning

rate. Momentum dampens oscillations through temporal averaging but doesn’t explicitly

compensate for curvature differences. Adam addresses ill-conditioning more directly by

equalising the scale of updates across dimensions.

3 Bias-variance trade-off in medical DL

(a) Model A (100 params, 60%/58%):

• Bias: High. Low training accuracy (60%) indicates the model lacks capacity to fit

the data

• Variance: Low. Small train-val gap (2%) indicates stability across datasets

Model B (10K params, 85%/82%):

• Bias: Moderate. Good training accuracy suggests adequate capacity

• Variance: Low-moderate. Small gap (3%) indicates good generalisation

Model C (1M params, 98%/75%):

• Bias: Low. Near-perfect training accuracy indicates the model can fit any pattern

• Variance: High. Large gap (23%) indicates the model has memorised training-

specific patterns

(b)

• Model A: Underfitting (high bias, low variance)

• Model B: Well-balanced (appropriate bias-variance trade-off)

• Model C: Overfitting (low bias, high variance)

(c) Strategy 1: Data augmentation

Apply random transformations (rotations, flips, crops, intensity variations) to training

images. This artificially increases effective dataset size and forces the model to learn

features invariant to these transformations.

Why it helps: The model cannot memorise specific pixel patterns since each image appears

differently each epoch. It must learn robust features (e.g., “nodule shape”) rather than

spurious correlations (e.g., “this exact pixel pattern”). Particularly effective for medical

imaging where the same pathology can appear at different positions, orientations, and

scales.

Strategy 2: Dropout

Randomly set a fraction of neurons (e.g., 50%) to zero during each training step. At test

time, use all neurons with appropriately scaled weights.

Why it helps: Prevents co-adaptation of neurons. The model cannot rely on any specific

neuron, forcing redundant and robust representations. Acts as an implicit ensemble,

-----

|  |
| :-: |
| [**Page 5**]() |

Deep Learning in Healthcare

Hilary Term 2026

training exponentially many sub-networks that are averaged at test time. Reduces effective

model capacity without reducing the architecture.

(Other valid answers: weight decay/L2 regularisation, early stopping, label smoothing,

reducing model size.)

(d) (i) Model C has 1,000,000 parameters. Under the 10-examples-per-parameter heuristic:

Required examples = 10 × 1,000,000 = 10,000,000

Ten million labelled examples would be needed.

(ii) The dataset has only 1,000 examples: 10,000× fewer than required. Even “large”

medical imaging datasets rarely exceed 10,000 examples due to the cost and expertise

required for annotation.

Implication: Training large models (millions of parameters) from scratch on medical

data is fundamentally infeasible. The model will inevitably overfit severely, as we see

with Model C. This is not a matter of needing “more regularisation”. The sample

complexity mismatch is too extreme.

(iii) Transfer learning pre-trains the model on a large natural image dataset (e.g., Im-

ageNet with 1.2M images). The model learns general visual features (i.e., edges,

textures, shapes, object parts) that transfer to medical images.

When fine-tuning on medical data:

• Early layers (general features) are frozen or updated minimally

• Only the final layers (task-specific features) are trained on the small medical

dataset

• The effective number of parameters being learned from medical data drops from

1M to perhaps 10K–100K

This reduces the sample complexity by 10–100×, making it feasible to train powerful

models with only thousands of medical examples. Transfer learning is not just helpful

but essential for deep learning in healthcare.

4 Architecture design under memory constraints

(a) Fully connected design.

(i) A fully connected layer has:

Parameters = nin × nout + nout = nout(nin + 1)

(one weight per input-output pair, plus one bias per output neuron)

(ii) For a network with input (784) → hidden (h) → output (10):

Layer 1: h(784 + 1) = 785h

Layer 2: 10(h + 1) = 10h + 10

Total: 785h + 10h + 10 = 795h + 10 ≤ 50,000

Solving:

h ≤

50,000 − 10

795

\=

49,990

795

≈ 62.88

Maximum hidden units: h = 62

Verification: 795 × 62 + 10 = 49,290 + 10 = 49,300 \< 50,000 ✓

-----

|  |
| :-: |
| [**Page 6**]() |

Deep Learning in Healthcare

Hilary Term 2026

(b) Convolutional design.

(i) A convolutional layer has:

Parameters = Cin × k2 × Cout + Cout = Cout(Cin · k2 + 1)

(each of Cout filters has k × k weights per input channel, plus one bias)

(ii) Design with 3×3 convolutions and 2×2 max-pooling (stride 2):

Layer

Output size

Params

Input

28 × 28 × 1

0

Conv1: 1 → 16, 3×3

28 × 28 × 16

16(1 · 9 + 1) = 160

MaxPool 2×2

14 × 14 × 16

0

Conv2: 16 → 32, 3×3 14 × 14 × 32

32(16 · 9+1)=4,640

MaxPool 2×2

7 × 7 × 32

0

Flatten

1568

0

FC: 1568 → 10

10

10(1568 + 1) = 15,690

Total

20,490

This uses ∼20,500 parameters, well under the 50,000 budget.

Note: The final FC layer dominates the parameter count. With more budget, we

could add a third conv layer (e.g., 32 → 64) adding 64(32 · 9 + 1) = 18,496 params,

for a total of ∼39,000. Still under budget.

(c) Comparison of designs:

• FC network: 62 hidden units, ∼49,300 parameters

• CNN: 16/32 channel conv layers + FC head, ∼20,500 parameters

The CNN uses less than half the parameters yet provides far greater representational

capacity:

Weight sharing: Each 3×3 filter (9 weights) is applied at every spatial location. Conv1

uses 160 parameters but produces 28 × 28 × 16 = 12,544 activation values. The FC

network would need 784 × 62 = 48,608 parameters just for its first layer to produce only

62 activations.

Translation equivariance: A feature detector (e.g., edge detector) learned in one lo-

cation automatically works everywhere. An FC network must learn the same pattern

independently for each pixel position, wasting capacity.

Hierarchical feature learning: Conv layers build features compositionally: edges com-

bine into textures, textures into shapes. The CNN’s receptive field grows with depth,

enabling it to recognise complex spatial patterns. The FC network has no spatial struc-

ture and must learn all relationships from scratch.

Expected performance: The CNN would significantly outperform the FC network on

image classification despite using fewer parameters. For medical images with spatial struc-

ture (lesions, anatomical features), the CNN’s inductive biases are particularly valuable.

-----

|  |
| :-: |
| [**Page 7**]() |

Deep Learning in Healthcare

Hilary Term 2026

5 Batch normalisation in clinical deployment

(a) Domain shift and deployment.

(i) During training, batch normalisation computes running estimates of mean µ and

variance σ2 from Hospital A’s data. At inference, these fixed statistics normalise

activations.

If Hospital B has different:

• Patient demographics (e.g., older population)

• Imaging protocols (e.g., different scanner, contrast settings)

• Disease prevalence (e.g., different case mix)

then the activation distributions will differ from training. Normalising with Hospital

A’s statistics will shift activations to incorrect ranges and scale them incorrectly,

causing downstream layers to receive out-of-distribution inputs. This can signifi-

cantly degrade performance even if the underlying clinical task is identical.

(ii) At training time:

• Train on multi-site data to learn more robust statistics

• Use aggressive data augmentation to simulate protocol variations

• Consider domain randomisation techniques

At deployment time:

• Batch norm adaptation: collect a small calibration set from Hospital B and

recompute running statistics before deployment

• Use test-time batch statistics if batch size is sufficiently large

Architecture alternatives:

• Use Group Normalisation or Layer Normalisation, which compute statistics per-

example and are less sensitive to distributional shift

• Use batch-free architectures where possible

(b) Training vs inference behaviour.

(i) For a single test example, the “batch” has size 1. Batch normalisation computes

statistics across the batch dimension. With one example:

µB = zi

(for each feature i)

σ2

B = 0 (variance of a single value is zero)

(ii) Substituting into the batch normalisation transform:

zi =

zi − µB

q

σ2

B

\+ ϵ

\=

zi − zi

√

0 + ϵ

\=

0

√

ϵ

\= 0

Every normalised activation becomes zero, regardless of the input values.

(iii) This is catastrophic: all information is destroyed, and the model outputs the same

prediction for any input. The single-example batch statistics contain no information

about the population. They merely centre each activation to zero.

Using running (population) statistics avoids this because:

• µ and σ2 are estimated from the entire training set during training

-----

|  |
| :-: |
| [**Page 8**]() |

Deep Learning in Healthcare

Hilary Term 2026

• They represent stable population statistics, not sample statistics from the current

batch

• A single test example is normalised relative to the training distribution, preserv-

ing meaningful activation magnitudes and differences

This is why models must be switched to “eval mode” at inference time.

(c) Small-batch clinical training.

(i) With very small batches (e.g., 2–4 examples for 3D medical volumes):

• Noisy statistics: Sample mean and variance computed from 2–4 examples are

highly variable estimates of the true population statistics

• Training instability: Noisy normalisation leads to noisy gradients, making

optimisation erratic

• Poor running statistics: The exponential moving average used for inference

is computed from these noisy batch statistics, degrading test performance

• Train-test mismatch: The high-variance training-time statistics don’t match

the stable inference-time statistics, causing distribution shift at test time

(ii) Group Normalisation (GN) is well-suited to small batches.

GN divides channels into groups and normalises within each group independently for

each example:

xi =

xi − µg

q

σ2

g + ϵ

where µg and σ2

g are computed over spatial dimensions and channels within group g,

for each example separately.

Why it addresses BatchNorm’s limitations:

• Statistics are computed per-example, so batch size is irrelevant

• No running statistics needed. Same computation at train and test time

• Works identically with batch size 1

• No train-test mismatch

GN is now standard in medical imaging architectures (e.g., nnU-Net) where memory

constraints force small batches.

(Layer Normalisation or Instance Normalisation are also valid answers.)

(d) Effect on optimisation.

(i) Batch normalisation standardises each layer’s pre-activations to have approximately

zero mean and unit variance (before the learnable affine transform γ,β). This:

• Controls activation scale: Prevents activations from growing or vanishing

exponentially through layers

• Stabilises gradients: Keeping activations in a consistent range ensures gradi-

ent magnitudes remain stable during backpropagation

• Reduces initialisation sensitivity: Even with suboptimal weight initialisa-

tion, activations are renormalised to a reasonable range

(ii) With stable activation and gradient scales:

• Larger learning rates can be used without causing gradient explosion or vanishing

• The loss landscape becomes smoother. Extreme activations that would create

steep cliffs are normalised away

• Training is more robust to hyperparameter choices

-----

|  |
| :-: |
| [**Page 9**]() |

Deep Learning in Healthcare

Hilary Term 2026

Empirically, batch normalisation allows learning rates 10–30× larger than without

it, dramatically accelerating convergence.

(iii) The “internal covariate shift” hypothesis proposed that BatchNorm helps by reduc-

ing the change in layer input distributions during training, stabilising each layer’s

learning problem.

However, Santurkar et al. (2018, “How Does Batch Normalization Help Optimiza-

tion?”) showed:

• BatchNorm does not significantly reduce internal covariate shift (measured di-

rectly)

• The primary benefit is smoothing the loss landscape: the loss becomes more

Lipschitz (bounded gradient changes) with better-conditioned Hessians

• This smoothing allows larger learning rates and more predictable gradient de-

scent steps

Other proposed explanations include:

• Implicit regularisation: Noise from batch statistics acts similarly to dropout

• Length-direction decoupling: Normalisation separates weight magnitude from

direction, simplifying the optimisation problem

• Enabling residual learning: In ResNets, BatchNorm after residual branches

helps the network learn identity mappings
