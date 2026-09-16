# DL4H — L11-12: Generative Modelling
> Source: Google Drive file 1PbhCfj1EqvWvJyKEYGEpWD7hCTK7M78t · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Low-data regimes: Generative modelling 

|  |
| :-: |
| [**Page 1**]() |

Ana Namburete

Department of Computer Science

University of Oxford

**Deep Learning in Healthcare**

Low-data regimes:

Generative modelling

-----

|  |
| :-: |
| [**Page 2**]() |

From representations to distributions

• Two different objectives:

• Representation learning

• Generative modelling

**Last lecture:**

Learn representations ð§=ð\!

(ð¥)

**This lecture:**

Model the data distribution ð"\#$\#

(ð¥)

-----

|  |
| :-: |
| [**Page 3**]() |

What does it mean to model ð(ð¥)?

• Why?

• Generate realistic samples

• Model (population) variability

• Detect anomalies (e.g., OOD cases)

• Quantify likelihood

**Goal:**

Learn ð\!

ð¥ ≈ð"\#$\#

(ð¥)

-----

|  |
| :-: |
| [**Page 4**]() |

What makes a good generative model?

1\. Efficient sampling

2\. High-quality sampling

3\. Coverage

4\. Well-behaved latent space

5\. Disentangled latent space

6\. Efficient likelihood computation

Desiderata

Out-of-distribution

(OOD)

In-distribution

(ID)

-----

|  |
| :-: |
| [**Page 5**]() |

Generative modelling: two approaches

[Sourc](https://towardsdatascience.com/understanding-generative-adversarial-networks-gans-cd6e4651a29)e

Generator

Example: Generative Adversarial Network (GAN)

Unit Gaussian, ð§

Generated distribution

ð\!(ð¥)

True data distribution

ð(ð¥)

loss

• Generate samples

• No explicit density

• No tractable likelihood

Implicit distribution matching

Generative

models

Explicit

density

models

Tractable

density

Approximate

density

Implicit

distribution

matching

-----

|  |
| :-: |
| [**Page 6**]() |

Generative modelling: two approaches

[Sourc](https://towardsdatascience.com/understanding-generative-adversarial-networks-gans-cd6e4651a29)e

Generative

models

Explicit

density

models

Tractable

density

Approximate

density

Implicit

distribution

matching

Example: Normalising Flows

• Define probability density, ð\!

(ð¥)

• Evaluate exact likelihood

• Generate samples

Explicit density modelling

Unit Gaussian, ð§

Density,

ð"(ð¥)

-----

|  |
| :-: |
| [**Page 7**]() |

From distribution matching

to adversarial learning

-----

|  |
| :-: |
| [**Page 8**]() |

Implicit distribution matching

Slide credit: Jorge Cardoso

• No explicit density, ð\!(ð¥)

• Generated distribution moves toward real

• Eventually indistinguishable

• Classifier-based logic

-----

|  |
| :-: |
| [**Page 9**]() |

Generative Adversarial Networks (GANs)

• Let:

• ðº%

be the generator

• ð·&

be the discriminator

• (ð and ð are the parameters of ðº

and ð·, respectively)

• The generator is a neural

network which takes as input a

noise vector ð\~ð(0,1) and

produces ðº\!

ð§ =ð

• The discriminator is a NN which

takes an input a real image (ð)

or a generated ð=ðº\!

ð§ , and

classifies it as real or fake

Real images

ð\~ð(0,1)

Generator

Discriminator

Real or fake?

,ð¦

ℝ\!

ℝ"

ℝ"

-----

|  |
| :-: |
| [**Page 10**]() |

Generator’s Objective

• Generator: maps a latent

variable (ð§) into image space

• The goal is to **minimise**:

min

\!

ð¼"\~$(")

log 1 − ð·'

ðº\!

(ð§)

Push discriminator output toward 1

Real images

ð\~ð(0,1)

Generator

Discriminator

Real or fake?

,ð¦

ðº\# ð§

ð·$(ðº\# ð§ )

-----

|  |
| :-: |
| [**Page 11**]() |

Discriminator’s Objective

• Discriminator: assigns a high score

to real images, and a low score

to fake images

• The goal is to **maximise**:

Real images

ð\~ð(0,1)

Generator

Discriminator

Real or fake?

,ð¦

ðº\# ð§

ð·$(ðº\# ð§ )

max

\!

ð¼,%&'&

log ð·\!

ð¥ + ð¼-\~,(-)

log 1 − ð·\!

ðº/

(ð§)

Real → 1

Fake → 0

Interpret as: ð *real* ∣ð¥ .

-----

|  |
| :-: |
| [**Page 12**]() |

The Min-Max Objective

• Combining the losses of the generator and discriminator,

we get a **min-max** game:

Real images

ð\~ð(0,1)

Generator

Discriminator

Real or fake?

,ð¦

ðº\# ð§

ð·$(ðº\# ð§ )

min

"

max

\#

ð¼$\~& $

logð· ð¥ +ð¼'\~& '

log 1 − ð· ðº(ð§)

-----

|  |
| :-: |
| [**Page 13**]() |

min

(

max

)

ð¼\*\~$ \*

logð· ð¥ +ð¼"\~$ "

log 1−ð· ð¥

If the generator is fixed, what is the optimal discriminator?

-----

|  |
| :-: |
| [**Page 14**]() |

**Bayes-optimal classifier** between:

• Real samples from ð(ð¥)

• Fake samples from ð(

(ð¥)

ð·

∗

(ð¥) =

ð,

(ð¥)

ð ð¥ + ð,

(ð¥)

Sanity check:

• when ð ð¥ ≫ ð(

ð¥ , ð·∗ ð¥ ≈1;

• when ð(

ð¥ ≫ ð ð¥ , ð·∗ ð¥ ≈0.

min

(

max

)

ð¼\*\~$ \*

logð· ð¥ +ð¼"\~$ "

log 1−ð· ð¥

If the generator is fixed, what is the optimal discriminator?

-----

|  |
| :-: |
| [**Page 15**]() |

What distance are GANs really minimising?

• **Jensen-Shannon divergence (JSD)**

• A **symmetric** measure of difference between two distributions

• Always finite, bounded by \[0,1\]

• ð·34

\= 0 iff the distributions are identical, i.e. ðð¥ ==ð5

(ð¥)

ð·\-.

ð,

∥ð =ð·/0

ð,

∥ð +

1

2

ð·/0

ð∥ð

**Quality**

Penalises generated

samples where real

data density is low

**Coverage**

Penalises regions

where real data

exists but the

generator produces

none.

where ð(ð¥) =

% & '%"(&)

\*

-----

|  |
| :-: |
| [**Page 16**]() |

Training GANs in practice

• Alternate between two steps:

Real images

ð\~ð(0,1)

Generator

Discriminator

Real or fake?

,ð¦

ðº\# ð§

ð·$(ðº\# ð§ )

max

$

ð¼&\~%\#$%$

log ð·$ ð¥ + ð¼,\~%(,) log 1 − ð·$ ðº\#(ð§)

Step 1

Gradient ascent on discriminator

Step 2

Gradient descent on generator

min

\#

ð¼,\~%(,) log 1 − ð·$ ðº\#(ð§)

\* In practice, this generator loss function does not work well

(so there is a slightly modified version)

\= max

\#

ð¼,\~%(,) log ð·$ ðº\#(ð§)

-----

|  |
| :-: |
| [**Page 17**]() |

Why JSD fails in high dimensions

If the real and generated

distributions **do not overlap**:

ð·"\#

ð$

∥ ð = log 2

Constant.

Therefore,

∇%

ð·"\#

ð$

∥ð =0

No gradient signal for the

generator.

Vanishing gradients

ð5

(ð¥)

ð(ð¥)

No overlap,

ð·\-.= constant

-----

|  |
| :-: |
| [**Page 18**]() |

The GAN Dilemma

Vanishing gradients

If the **discriminator becomes perfect**:

• ð· ð¥ = 1 for real samples

• ð· ð¥ = 0 for generated samples

Then:

• Generator gradients → 0

• Learning stalls

If the **discriminator is weak**:

• Poor feedback

• No meaningful density signal

Training becomes delicate.

-----

|  |
| :-: |
| [**Page 19**]() |

Practical instability

• Let the function be ð = ð¥ð¦

• Player 1 controls ð¥:

• **minimises** ð/ ð¥ =ð¥ð¦

• Player 2 controls ð¦:

• **maximises** ð\*(ð¦) = −ð¥ð¦

• Gradients:

ðð\*

ðð¥

\= ð¦ and

ðð+

ðð¦

\= −ð¥

• Parameters updated as

ð¥,-\*

\= ð¥,

− ðð¦,

ð¦,-\*

\= ð¦,

\+ ðð¥,

(where ð is the learning rate)

Min-max optimisation is not

standard optimisation

-----

|  |
| :-: |
| [**Page 20**]() |

Practical instability

• Very high-dimensional data

• There exists a separating hyperplane between real and synthetic data

High-dimensional separability

[Proo](https://arxiv.org/pdf/1701.04862.pdf)f

-----

|  |
| :-: |
| [**Page 21**]() |

Practical instability

Mode collapse

-----

|  |
| :-: |
| [**Page 22**]() |

Wasserstein GAN: A better distance

• Wasserstein distance:

ð ð,ð,

\= min

1

: ð¥−ð¦ ðð(ð¥,ð¦)

(Optimal transport plan)

-----

|  |
| :-: |
| [**Page 23**]() |

Wasserstein GAN: A better distance

• Wasserstein distance:

ð ð,ð,

\= min

1

: ð¥−ð¦ ðð(ð¥,ð¦)

• Dual form:

ð ð,ð,

\= max

2 '

34

ð¼\*\~$

ð(ð¥) − ð¼\*\~$(

ð(ð¥)

• Constraint:

∇\*

ð(ð¥) ≤ 1

(Optimal transport plan)

(1-Lipschitz)

Formally:

∣ð ð¥ −ð ð¦ ∣ ≤ ∥ð¥−ð¦∥

-----

|  |
| :-: |
| [**Page 24**]() |

WGAN Objective

• Replace discriminator with **critic** ð5

(ð¥):

max ð¼\*\~$

ð5

(ð¥) − ð¼"\~$(")

ð5

ðº(ð§)

• Generator minimises this quantity.

**Why this works**

Unlike JSD:

• Well-defined even if supports are disjoint

• Varies smoothly as distributions move closer

• Provides meaningful gradients

-----

|  |
| :-: |
| [**Page 25**]() |

JSD vs WGAN Behaviour

**Property**

**JSD**

**WGAN**

Requires overlap

Yes

No

Gradient when disjoint

0

Non-zero

Training stability

Fragile

Improved

-----

|  |
| :-: |
| [**Page 26**]() |

How do we evaluate generative models?

• If ð'

ð¥ is **tractable**:

• Evaluate ð¼I\~,%&'&

log ð\!

(ð¥)

**Key question:**

Does ð\!

ð¥ ≈ð"\#$\#

(ð¥) ?

• If density is **intractable** (e.g.

GANs):

• Compare ð\!

and ð"\#$\#

via

sample statistics

Explicit density modelling

Implicit distribution matching

-----

|  |
| :-: |
| [**Page 27**]() |

Fréchet Inception Distance (FID)

Real images

Inception-

V3

Generated images

Gen. features

Real features

Inception-

V3

ð© ð0,Σ0

ð© ð1,Σ1

**FID**

Embed samples into feature space

(using a pretrained network):

ð¥ ⟶ ð(ð¥)

Approximate real and generated

features as Gaussians:

ð ð¥NO\#P

\~ ð© ðN

,ΣN

ð ð¥5OQ

\~ ð© ð5

,Σ5

ð¹ð¼ð· = ð.

− ð(

\+

\+ðð Σ.

\+ Σ(

−2 Σ.

Σ(

\*

\+

Perceptual distance between two distributions

ð¥1

Step 1

Step 2

\* Lower is better.

-----

|  |
| :-: |
| [**Page 28**]() |

Limitations of FID (esp. in healthcare)

• Depends on pretrained feature extractor (representation)

• Not task-specific

• Sensitive to sample size

**Better alternatives in healthcare:**

• Performance on downstream tasks

• Radiologist evaluation

• Precision/recall for generative models

-----

|  |
| :-: |
| [**Page 29**]() |

Precision/Recall for Generative Models

• Let:

ℳ6787

: data manifold

ℳ9:6;\<

: model manifold

Precision=

Generated samples in ℳ\!232

Total generated samples

Measures realism

Recall =

Real samples in ℳ45\!67

Total real samples

Measures coverage

-----

|  |
| :-: |
| [**Page 30**]() |

Normalising Flows

Normalising flows turn density estimation into geometry.

-----

|  |
| :-: |
| [**Page 31**]() |

Explicit Probability Models

Generative

adversarial

models

Probabilistic

models

VAEs

Normalising flows

Diffusion models

GANs

-----

|  |
| :-: |
| [**Page 32**]() |

Change of variables

-----

|  |
| :-: |
| [**Page 33**]() |

Change of variables

• Let ð be a deterministic map

• ð¥ = ð(ð§)

• with inverse ð§=ð

\=4

(ð¥)

ð§, +ðð§

/

ð¥, +ðð¥

Same event, different coordinates

ð\!

(ð¥) ðð¥ = ð"

(ð§) ðð§

-----

|  |
| :-: |
| [**Page 34**]() |

Change of variables

• ð **redistributes** the probability

mass

Derivative

From probability mass to densities

ð\!

(ð¥) = ð"

(ð§)

ðð§

ðð¥

With ð¥ = ð(ð§), ð§=ð^\_(ð¥)

-----

|  |
| :-: |
| [**Page 35**]() |

Local linearisation and volume distortion

• Local linearisation: ð ð§+ð¿ð§ ≈ð ð§ +ð½ð¿ð§

• Jacobian, ð½: local linear map

• Determinant, det ð½ : volume scaling factor

Density rescales inversely with volume change.

ð¿ð§\#

ð¿ð§$

ð§\#

ð§$

ð¥\#

ð¥$

ð§ ↦ ð¥ = ð(ð§)

Area: ð¿ð§& ð¿ð§'

Area:

det ð½ ð¿ð§

&

ð¿ð§'

ð½ð¿ð§\#

ð½ð¿ð§$

-----

|  |
| :-: |
| [**Page 36**]() |

Multivariate change of variables

The **Jacobian** of the inverse map measures

the change in volume:

ðð§ = det

ðð8/

ðð¥

ðð¥

ð\>

(ð¥) ðð¥ = ð?

(ð§) ðð§

Conservation of probability mass:

In higher dimensions:

• We stretch or compress **volumes**

• The Jacobian matrix measures local linear behaviour

• Its determinant measures **volume distortion**

Density scales by inverse volume change.

-----

|  |
| :-: |
| [**Page 37**]() |

Multivariate change of variables

ð\>

(ð¥) ðð¥ = ð?

(ð§) ðð§

**Step 1:** Conservation of probability mass

ð¥ = ð(ð§)

The probability of a small regions around ð¥ is

**exactly the same** as the probability of the

corresponding region around ð§=ð8/(ð¥).

-----

|  |
| :-: |
| [**Page 38**]() |

Multivariate change of variables

ð\>

(ð¥) = ð?

(ð

\=4

(ð¥)) det

ðð

\=4

ðð¥

Jacobian determinant

The **Jacobian** of the inverse map measures

the change in volume:

ðð§ = det

ðð8/

ðð¥

ðð¥

ð\>

(ð¥) ðð¥ = ð?

(ð§) ðð§

Density at ð¥ is the density at the corresponding

latent point, scaled by its volume change:

**Step 2:** Volume scaling

ð¥ = ð(ð§)

-----

|  |
| :-: |
| [**Page 39**]() |

Multivariate change of variables

ð\>

(ð¥) = ð?

(ð

\=4

(ð¥)) det

ðð

\=4

ðð¥

Jacobian determinant

ð\>

(ð¥) ðð¥ = ð?

(ð§) ðð§

Density at ð¥ is the density at the corresponding

latent point, scaled by its volume change:

**Step 3:** Forward Jacobian

ð¥ = ð(ð§)

Identify: ð§=ð8/(ð¥)

ð\>

(ð¥) = ð?

ð§ det

ðð

ðð§

\=4

ð½

9() = ð½9

8/

det ð½

9()

\= det ð½9

8/

\=

1

det ð½9

-----

|  |
| :-: |
| [**Page 40**]() |

Multivariate change of variables

**Step 4:** Log-Likelihood Form

ð\>

(ð¥) = ð?

(ð

\=4

(ð¥)) det

ðð

\=4

ðð¥

Jacobian determinant

log ð\>

(ð¥) = log ð?

(ð§) − log det

ðð

ðð§

Log-likelihood:

**Maximise** this when training a normalising flow

ð\>

(ð¥) = ð?

ð§ det

ðð

ðð§

\=4

-----

|  |
| :-: |
| [**Page 41**]() |

Building a flow: from theory to construction

• Desiderata for each transformation, ð@

• is invertible

• Its inverse can be computed efficiently

• We can compute the determinant of its Jacobian

ð¥=ð/

∘ ð/=4

∘⋯∘ð4

(ð§)

-----

|  |
| :-: |
| [**Page 42**]() |

Composition and Jacobians

Figure credit: Lil’Log

ð¥=ð/

∘ ð/=4

∘⋯∘ð4

(ð§)

log det

ðð

ðð§

\= I

AB4

/

log det

ððA

ðℎA=4

Each layer

contributes

**additively** to the

total objective

-----

|  |
| :-: |
| [**Page 43**]() |

From theory to construction

• We need transformations ð@

such that:

• Dense ð×ð Jacobian determinant:

ð(ð

C

)

(infeasible in high dimensions)

Invertible

Inverse is efficient

log det ð½ is tractable

-----

|  |
| :-: |
| [**Page 44**]() |

RealNVP: Affine coupling layers

Example

Split the input

ℎ = ℎ\*,ℎ+

Step 1

-----

|  |
| :-: |
| [**Page 45**]() |

RealNVP: Affine coupling layers

Example

Split the input

ℎ = ℎ\*,ℎ+

Step 1

Leave one half unchanged

ℎ\*′=ℎ\*

Step 2

-----

|  |
| :-: |
| [**Page 46**]() |

RealNVP: Affine coupling layers

Split the input

ℎ = ℎ\*,ℎ+

Example

Step 1

Leave one half unchanged

ℎ\*′=ℎ\*

Step 2

Transform the other half conditionally

ℎ

\+

/

\= ℎ+

⊙exp ð  ℎ\*

\+ ð¡ ℎ\*

Step 3

where ð  ⋅ ,ð¡(⋅) are neural networks.

-----

|  |
| :-: |
| [**Page 47**]() |

RealNVP: Affine coupling layers

Example

Inverse (closed form)

ℎ\*

\= ℎ\*

′

ℎ+

\= ℎ

\+

/

− ð¡ ℎ

\*

/

⊙ exp −ð  ℎ

\*

/

Why is this invertible?

log det ð½ =P ð  ℎ\*

Log-determinant

Why this works

• Invertible

• Inverse is explicit

• Jacobian is triangular

• Determinant is cheap

Inverse mapping

-----

|  |
| :-: |
| [**Page 48**]() |

RealNVP: Affine coupling layers

Example

Jacobian structure

ð½ =

ðℎ

\*

/

ðℎ\*

ðℎ

\*

/

ðℎ+

ðℎ

\+

/

ðℎ\*

ðℎ

\+

/

ðℎ+

\=

ð¼

0

∗ diag exp ð  ℎ\*

Why is the Jacobian determinant cheap?

log det ð½ =P

0

ð 0

ℎ\*

Triangular matrix

→ determinant = product of diagonal entries

det ð½ = S

0

exp ð 0 ℎ\*

No ð ð: determinant. Just a sum.

-----

|  |
| :-: |
| [**Page 49**]() |

ℎ′

/

; = ð ℎ′/ ℎ′\*

RealNVP: Affine coupling layers

Example

**Layer 1:**

ℎ\*,ℎ+ ⟶ ℎ′\*, ℎ′+

Expressivity via stacking

Stack many layers ⟹ global interaction.

**Layer 2 (swap roles):**

ℎ′\*

, ℎ′+

⟶ ℎ

\*

//

,ℎ

\+

//

ℎ

\*

; =ð ℎ\* ℎ/

-----

|  |
| :-: |
| [**Page 50**]() |

RealNVP: Affine coupling layers

Example

Putting it all together

Each layer contributes additively.

log ð(ð¥) = log ð(ð§) − I

A

log det ð½A

-----

|  |
| :-: |
| [**Page 51**]() |

Forward direction

ð§\~ð© 0,ð¼

ð¥ = ð ∎,ð

Data

Noise

Generative direction (ð§ → ð¥)

ð/ ∎, ð/

ð\* ∎, ð\*

ð: ∎, ð:

During **sampling**:

• Draw ð§∼ð© 0ð¼ .

• Apply forward transformations.

-----

|  |
| :-: |
| [**Page 52**]() |

Training

Data

Noise

ð/

8/ ∎, ð/

ð\*

8/ ∎, ð\*

ð:

8/ ∎, ð:

log det

ðð

ðð§

\= I

AB4

/

log det

ððA

ðℎA=4

During **training**:

• Take data ð¥.

• Compute ð§=ð

\#

8/ ð¥ .

• Accumulate log-determinants.

• Evaluate base density ð(ð§).

Inverse direction (ð¥ → ð§)

-----

|  |
| :-: |
| [**Page 53**]() |

Limitations of Normalising Flows

**Invertibility constrains architecture**

No arbitrary downsampling or information loss.

-----

|  |
| :-: |
| [**Page 54**]() |

Limitations of Normalising Flows

**Invertibility constrains architecture**

No arbitrary downsampling or information loss.

**Expressivity can require many layers**

Structured layers must be stacked to model complex distributions.

-----

|  |
| :-: |
| [**Page 55**]() |

Limitations of Normalising Flows

**Invertibility constrains architecture**

No arbitrary downsampling or information loss.

**Expressivity can require many layers**

Structured layers must be stacked to model complex distributions.

**Exact likelihood ≠ best perceptual sample quality**

Likelihood optimisation does not directly optimise visual sharpness.

-----

|  |
| :-: |
| [**Page 56**]() |

Limitations of Normalising Flows

**Invertibility constrains architecture**

No arbitrary downsampling or information loss.

**Expressivity can require many layers**

Structured layers must be stacked to model complex distributions.

**Exact likelihood ≠ best perceptual sample quality**

Likelihood optimisation does not directly optimise visual sharpness.

**Memory-heavy at high resolution**

Invertible mappings often require storing large intermediate states.

-----

|  |
| :-: |
| [**Page 57**]() |

Families of Normalising Flows

Coupling-based flows

• RealNVP

• Glow

• NICE

Split the variables.

Transform half conditioned on the other half.

Generation

Inference

-----

|  |
| :-: |
| [**Page 58**]() |

Families of Normalising Flows

Coupling-based flows

Autoregressive flows

• RealNVP

• Glow

• NICE

Split the variables.

Transform half conditioned on the other half.

Instead of splitting variables into 2 blocks,

transform each dimension sequentially.

-----

|  |
| :-: |
| [**Page 59**]() |

Families of Normalising Flows

Coupling-based flows

Autoregressive flows

• RealNVP

• Glow

• NICE

Continuous-time flows

• Neural ODE flows

• Continuous Normalising Flows (CNFs)

Split the variables.

Transform half conditioned on the other half.

Instead of stacking discrete layers, they define

a transformation via a differential equation:

ðð§

ðð¡

\= ð(ð§, ð¡)

Instead of splitting variables into 2 blocks,

transform each dimension sequentially.

-----

|  |
| :-: |
| [**Page 60**]() |

Families of Normalising Flows

Coupling-based flows

Autoregressive flows

• RealNVP

• Glow

• NICE

Continuous-time flows

• Neural ODE flows

• Continuous Normalising Flows (CNFs)

Spline-based flows

• Rational quadratic splines

• Neural spline flows

Split the variables.

Transform half conditioned on the other half.

Instead of stacking discrete layers, they define

a transformation via a differential equation:

ðð§

ðð¡

\= ð(ð§, ð¡)

Instead of splitting variables into 2 blocks,

transform each dimension sequentially.

-----

|  |
| :-: |
| [**Page 61**]() |

Different ways to control the Jacobian

**Family**

**Core idea**

**How log-det is tractable Typical examples**

**Coupling flows**

Split variables; transform

half conditioned on half

Block-triangular

Jacobian

RealNVP, Glow, NICE

**Autoregressive flows**

Transform dimensions

sequentially

Strictly triangular

Jacobian

MAF, IAF

**Continuous-time flows**

Define transformation

via ODE

Integrate trace of

Jacobian

CNFs, Neural ODE flows

**Structured linear flows**

Constrain linear

transforms

Structured matrices (LU,

1×1 conv)

Glow 1×1 conv

**Spline flows**

Replace affine maps

with monotonic warps

Still triangular via

coupling/autoregressive

structure

Neural spline flows

-----

|  |
| :-: |
| [**Page 62**]() |

Diffusion models: A third paradigm

Gradually corrupt data with Gaussian noise:

After many steps:

ð¥\< ≈ ð©(0, ð¼)

ð¥3 = ð¼3ð¥38/ + 1−ð¼3ð ð \~ ð©(0,ð¼)

Train a neural network to predict the noise:

Forward process (fixed, not learned)

Reverse process (learned)

Loss:

ℒ ð = ð¼&\*,\>,3

ð−ð$ ð¥3,ð¡ \*

ð$(ð¥3, ð¡)

-----

|  |
| :-: |
| [**Page 63**]() |

Diffusion models: A third paradigm

• No adversarial min-max game

• Stable optimisation (MSE-style objective)

• Extremely high sample quality

• Approximate likelihood possible

• Not purely implicit like GANs

• Not exact-density like flows

• A modern alternative based on

iterative denoising

Key characteristics

-----

|  |
| :-: |
| [**Page 64**]() |

Three philosophies of generative modelling

**GANs**

**Normalising Flows**

**Diffusion Models**

**Core idea**

Match distributions via

**adversarial game**

Transform densities via

**invertible geometry**

Reverse a stochastic

**corruption process**

**Likelihood**

✗ Implicit

✓ Exact

\~ Approximate

**Training**

Min–max optimisation

Maximum likelihood

Denoising regression

**Strength**

Sharp samples

Exact density, stable

training

State-of-the-art synthesis

**Weakness**

Unstable training

Architectural constraints

Slow sampling

-----

|  |
| :-: |
| [**Page 65**]() |

Generative modelling in healthcare

• Cross-modality synthesis

• Useful when:

• Certain modalities are

unavailable

• Radiation exposure needs

to be reduced

• Multimodal alignment is

required

Conditional synthesis (e.g., MRI → CT)

**1**

S. Kazeminia et al, GANs for medical image analysis, Artificial Intelligence in Medicine, 109, 2020

-----

|  |
| :-: |
| [**Page 66**]() |

Generative modelling in healthcare

• Remove aliasing artifacts

• Fill in missing information

• Reduce motion artifacts

• Improve patient comfort

• Increase scanner

throughput

Reconstruction & Acceleration

**2**

S. Kazeminia et al, GANs for medical image analysis, Artificial Intelligence in Medicine, 109, 2020

-----

|  |
| :-: |
| [**Page 67**]() |

Generative modelling in healthcare

• Simulation of rare

pathologies

• Augmentation of training

sets

• Model variability in lesion

appearance

• Stress-test detection

systems

Disease detection & simulation

**3**

S. Kazeminia et al, GANs for medical image analysis, Artificial Intelligence in Medicine, 109, 2020

-----

|  |
| :-: |
| [**Page 68**]() |

Generative modelling in healthcare

• Reconstruct cleaner

images from noisy

measurements

• The model must not

hallucinate structure.

De-noising & artifact removal

**4**

S. Kazeminia et al, GANs for medical image analysis, Artificial Intelligence in Medicine, 109, 2020

-----

|  |
| :-: |
| [**Page 69**]() |

Risks and failure modes

**Hallucinated pathology**

Models may invent or remove clinically

relevant findings.

**Mode collapse / bias**

Under-representation of rare disease.

**Distribution shift**

Poor generalisation across scanners or

populations.

**Privacy leakage**

Memorisation of patient data.

**False confidence**

High realism ≠ clinical validity

-----

|  |
| :-: |
| [**Page 70**]() |

Risks and failure modes

**Hallucinated pathology**

Models may invent or remove clinically

relevant findings.

**Mode collapse / bias**

Under-representation of rare disease.

**Distribution shift**

Poor generalisation acros
