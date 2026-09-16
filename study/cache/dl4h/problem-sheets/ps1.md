# DL4H — Problem Sheet 1
> Source: Google Drive file 1WYpUwHEUSISQcwhRAEPnpufUwR8Hust_ · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Problem Sheet 1 

|  |
| :-: |
| [**Page 1**]() |

Deep Learning in Healthcare

Hilary Term 2026

Problem Sheet 1

Note. Questions 1–4 constitute the core of this problem sheet; Question 5 is an optional

extension for further exploration.

1 Backpropagation for medical diagnosis

Consider a two-layer neural network that predicts whether a disease is present (label y ∈ 0,1)

from a patient’s vital signs x = (x1,x2,x3)⊤, representing age (years), BMI (kg/m2), and

systolic blood pressure (mmHg).

The network has the following form:

• Hidden layer with 4 neurons and ReLU activation: h = ReLU(W⊤

1 x + b1) where h ∈ R4

• Output layer with sigmoid activation: y = σ(w⊤

2 h + b2) where y ∈ \[0,1\]

• Binary cross-entropy loss: L = −(y log y + (1 − y) log(1 − y))

(a) Chain rule and backpropagation. Write down the full chain rule expression for

∂L/∂W1 in terms of intermediate derivatives. Clearly identify each factor in the chain

and explain what it represents. Why does backpropagation compute gradients in reverse

order, from the output layer back to the input layer?

(b) Vanishing gradients.

(i) Compute the derivative of the sigmoid function σ(z) =

1

1+e−z and show that

dσ

dz

\= σ(z) 1 − σ(z)&#1;.

What is the maximum possible value of this derivative?

(ii) Consider a deep network composed of L sigmoid layers. If gradients are backprop-

agated through all L layers, explain why the gradient magnitude tends to vanish

(approach zero) as L increases.

(iii) Explain why ReLU activations (ReLU(z) = max(0,z)) typically do not suffer from

this problem in the same way, and why their use enabled the successful training of

much deeper networks.

(c) Dead ReLU problem. Suppose that during training a neuron has pre-activation

zi = w

⊤

i x + bi = −2.5.

(i) Compute the output hi = ReLU(zi) and the gradient ∂L/∂wi using the chain rule

(you may assume that ∂L/∂hi is a non-zero value propagated from higher layers).

(ii) If this neuron’s pre-activation remains negative for all training examples, what hap-

pens to its weights during gradient descent? Explain why such a neuron is referred

to as dead.

(iii) Explain how Leaky ReLU, defined as LeakyReLU(z) = max(αz, z) with small α \> 0,

mitigates this problem.

Remark: This type of simple network could form the core of a clinical risk model for ICU

monitoring based on routinely collected vital signs.

-----

|  |
| :-: |
| [**Page 2**]() |

Deep Learning in Healthcare

Hilary Term 2026

2 Optimization and ill-conditioned losses

Consider the quadratic loss function

L(w)=0.5w2

1 + 10w2

2

where w = (w1,w2)⊤. This loss is representative of the ill-conditioned optimization landscapes

encountered when training deep CNNs for medical image analysis.

(a) Compute the gradient ∇L at w = (1,1)⊤. What do you notice about the relative magni-

tudes of the two components? Relate this to the geometry of the loss surface.

(b) The Hessian of this loss is constant. Write it down and compute its eigenvalues. The

condition number is the ratio of the largest to smallest eigenvalue. What is it for this

loss? Explain why a high condition number makes gradient descent difficult.

(c) For vanilla gradient descent with learning rate α, the update in direction i is wi ← wi −

αλiwi, where λi is the curvature (Hessian eigenvalue) in that direction. For convergence,

we need |1 − αλi| \< 1 for all i. Derive the maximum stable learning rate for this loss.

Which direction constrains it?

(d) Momentum maintains a velocity v that averages past gradients. Explain intuitively why

this helps on ill-conditioned losses. Consider what happens to oscillations in the high-

curvature direction versus progress in the low-curvature direction.

(e) Adam maintains per-parameter running averages of squared gradients and scales updates

inversely by

√

vi. Explain how this addresses the ill-conditioning problem differently from

momentum.

3 Bias-variance trade-off in medical DL

You train three lung nodule classifiers of increasing complexity on a dataset of 1,000 labelled

CT scans. Their performance is summarised below:

Model

Parameters Train Accuracy Validation Accuracy

Model A

100

60%

58%

Model B

10,000

85%

82%

Model C

1,000,000

98%

75%

(a) For each model, estimate the bias and variance qualitatively using the training-validation

gap.

(b) Classify each model as underfitting, well-balanced, or overfitting.

(c) Model C overfits the data. Propose two distinct strategies to improve its generalisation

performance. For each, briefly describe the method and explain why it helps.

(d) A common heuristic suggests that reliable generalisation requires roughly 10 training

examples per parameter.

(i) Under this heuristic, estimate how many labelled examples Model C would need to

generalise well without regularisation.

-----

|  |
| :-: |
| [**Page 3**]() |

Deep Learning in Healthcare

Hilary Term 2026

(ii) Labelled medical imaging datasets rarely exceed 10,000 examples due to the cost of

expert annotation. Given your answer to (i), what does this imply about training

large models from scratch in healthcare?

(iii) Explain how transfer learning (pre-training on large natural image datasets like Im-

ageNet) addresses this fundamental limitation.

4 Architecture design under memory constraints

You are designing a classifier for 28×28 grayscale medical images (10 classes) to run on a

resource-constrained device with a budget of 50,000 parameters.

(a) Fully connected design.

(i) Write down the formula for the number of parameters in a fully connected layer

mapping nin inputs to nout outputs (including biases).

(ii) Design a fully connected network (input → hidden → output) that fits within the

50,000 parameter budget. What is the maximum number of hidden units you can

afford? Show your calculation.

(b) Convolutional design.

(i) Write down the formula for the number of parameters in a convolutional layer with

Cin input channels, Cout output channels, and kernel size k × k (including biases).

(ii) Design a CNN using 3×3 convolutions and 2×2 max-pooling (stride 2) that fits

within the 50,000 parameter budget. Specify the number of layers and channels at

each layer. Hint: the final FC layer from flattened features to 10 classes will consume

most of your budget.

(c) Comparison. Compare the representational capacity of your two designs. Despite using

similar parameter counts, which architecture would you expect to perform better on med-

ical images, and why? Refer to weight sharing, translation equivariance, and hierarchical

feature learning in your answer.

Remark: Understanding the parameter efficiency of different architectures is essential when

deploying models on resource-constrained medical devices.

5 Batch normalisation in clinical deployment (optional)

Batch normalisation has become ubiquitous in medical imaging models, but introduces subtle

challenges at deployment time due to the mismatch between training and inference behavior.

(a) Domain shift and deployment. A model trained with batch normalisation on data

from Hospital A is deployed at Hospital B, where patient demographics, imaging protocols,

or disease prevalence differ.

(i) Explain how batch normalisation statistics can contribute to performance degrada-

tion under such domain shift.

(ii) What practical steps can be taken at training or deployment time to mitigate this

issue?

-----

|  |
| :-: |
| [**Page 4**]() |

Deep Learning in Healthcare

Hilary Term 2026

(b) Training vs inference behaviour. Consider a single test example with pre-activation

z ∈ Rd. Suppose batch normalisation were to use batch statistics at test time.

(i) Compute the batch mean µB = 1

d

Pd

i=1 zi and variance σ2

B = 1

d

Pd

i=1(zi − µB)2 for

this single example.

(ii) Substitute these values into the batch normalisation transform

z =

z − µB

q

σ2

B

\+ ϵ

.

What is the resulting normalised activation z?

(iii) Explain why this behaviour is undesirable, and how using running (population) statis-

tics at inference time avoids this problem.

(c) Small-batch clinical training. In many clinical applications (e.g. 3D imaging or high-

resolution scans), batch sizes are very small due to memory constraints.

(i) Explain why batch normalisation can become unstable or ineffective in this regime.

(ii) Briefly describe one alternative normalisation method that is better suited to small

batch sizes, and explain why it addresses the limitations of batch normalisation.

(d) Effect on optimisation.

(i) Explain how batch normalisation affects the scale of activations and gradients during

training.

(ii) Why does this often allow for larger learning rates and faster convergence?

(iii) The original BatchNorm paper (Ioffe & Szegedy, 2015) hypothesised that the primary

benefit comes from reducing “internal covariate shift”: the change in the distribution

of layer inputs during training. Recent work has questioned whether this is the main

mechanism. Briefly discuss what alternative explanations have been proposed.

Remark: Batch normalisation remains a standard component in medical imaging architec-

tures (U-Nets, ResNets), but practitioners must be aware of its behaviour under domain shift

and small-batch regimes common in clinical settings.
