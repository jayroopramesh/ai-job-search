# DL4H — L2: Loss Functions & Metrics
> Source: Google Drive file 1x0WllSeF3bSFO0HAxo2FjCGOswqCQUxM · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Neural networks as modelling objects under constraint 

|  |
| :-: |
| [**Page 1**]() |

Ana Namburete

Department of Computer Science

University of Oxford

**Deep Learning in Healthcare**

Neural networks as

modelling objects

under constraint

-----

|  |
| :-: |
| [**Page 2**]() |

What does it mean to “learn a function”?

• Training a neural network means minimising a loss over

data

• This is **empirical risk minimisation**

min

\!

ð¼ ",$ \~ð

\[ℒ ð\!

ð¥ ,ð¦ \]

ℒ reflects what we care about

ð\!"\#$%

≈ ð&'()\*+

Implicit assumptions

-----

|  |
| :-: |
| [**Page 3**]() |

Linear models as decision boundaries

• Linear decision boundary

• Interpretable, stable

ð¥\!

ð¥"

ð¥\#

ð¦ ∈ {0,1}

…

ð¤\!

ð¤"

ð¤\#

ð

ð

ð¥,

ð¥-

\!

\!"\#

$

ð¤\! ∗ ð¥\! = 0

ð

ð

-----

|  |
| :-: |
| [**Page 4**]() |

XOR: Limits of linear models

ð¥\!

ð¥"

(0,0)

(1,0)

(1,1)

ð¤$

\+ ð¤%

⋅ 0 +ð¤&

⋅ 0 \<0 ⟹ ð¤$

\< 0

ð¤$

\+ ð¤%

⋅ 0 +ð¤&

⋅ 1 ≥0 ⟹ ð¤&

≥ −ð¤$

ð¤$

\+ ð¤%

⋅ 1 +ð¤&

⋅ 0 ≥0 ⟹ ð¤%

≥ −ð¤$

ð¤$

\+ ð¤%

⋅ 1 +ð¤&

⋅ 1 \<0 ⟹ ð¤%

\+ ð¤&

\< −ð¤$

The fourth condition contradicts conditions 2 and 3

No solution possible to satisfy this set of inequalities

Data are **not linearly separable**.

(0,1)

-----

|  |
| :-: |
| [**Page 5**]() |

XOR: Solved with stacked

• The XOR can be broken down

into simpler Boolean functions

ð¦

ððð ð´,ðµ =ð´⋅4ðµ + ðµ⋅̅ð´

\= ⋯

\= ð´+ðµ ⋅(ð´ðµ)

ðð

ðð´ðð·

ð´ðð·

ððð

ð¥'

ð¥(

ððð ð¥%

,ð¥&

\= ð¥%

\+ ð¥&

⋅ ð¥%

⋅ ð¥&

OR

NAND

-----

|  |
| :-: |
| [**Page 6**]() |

Multi-layer perceptron (MLP)

• A multi-layer perceptron is also

called a **feedforward neural**

**network**

• A collection of neurons organised

in **layers**

ð¥'

ð¥(

ð¥)

:ð

Input

layer

Output

layer

**Model:**

&ð¦$

\=ð ð¥$

\= ð . ð - ð , (ð¥)

\= ð\*

ð\[.\]ð ð\[-\]ð ð\[,\]ð¥$

\+ ð\[,\] + ð\[-\] + ð\[.\]

**Data:** ð¥,

,ð¦, ,-%

.

ð \! : ℝ\# → ℝ$\!

-----

|  |
| :-: |
| [**Page 7**]() |

Anatomy of an MLP

ð¾

\[+,'\]

ð¾

\[+\]

ð¥'

ð¥(

ð¥)

ð¾

\[+,(\]

:ð=ℎ 4 = ð(ð)

ð\[46&\]

ð\[46%\]

ð\[4\]

**Pre-activation** at layer ð is given by

ð % ð¥ =ð % ℎ %&\! ð¥ +ð %

**Activation** at layer ð is given by

ℎ % ð¥ = ð ð % (ð¥)

ð is the activation function

(e.g. sigmoid, tanh, linear, etc)

**Activation** at the output layer is given by

ð ð¥ = ℎ ' = ð( ð ' (ð¥)

ð( is the output activation function

(e.g. softmax, linear, etc)

ℎ ) = ð ∈ ℝ\#×\!

ð % ∈ ℝ+×\!

ℎ %&\! ∈ ℝ\#×\!

ð % ∈ ℝ+×\#

ð % ∈ ℝ+×\!

ð

\[12-\]

ð\[12-\]

ð\[12,\]

ð\[12,\]

ð\[1\]

ℎ % ∈ ℝ+×\!

-----

|  |
| :-: |
| [**Page 8**]() |

Common activation choices

-----

|  |
| :-: |
| [**Page 9**]() |

What does a ReLU network represent?

Linear pieces stitched together

-----

|  |
| :-: |
| [**Page 10**]() |

Representation power ≠ Learning

• Representation power does not imply

learnability or safety

• Neural networks are expressive

(**Universal Approximation Theorem)**

• This is an **existence** result, not a

learning guarantee

• It says nothing about:

• Data requirements

• Optimisation dynamics

• Generalisation under shift

[Figure sourc](https://medium.com/analytics-vidhya/neural-networks-and-the-universal-approximation-theorem-e5c387982eed)e

-----

|  |
| :-: |
| [**Page 11**]() |

Same function, different representations

-----

|  |
| :-: |
| [**Page 12**]() |

Loss functions

-----

|  |
| :-: |
| [**Page 13**]() |

The loss function defines success

• A neural network has no notion of correctness

• The loss function is the only signal used during training

• The optimiser will minimise it faithfully (… and blindly\!)

If the loss is misaligned, optimisation amplifies the mistake

-----

|  |
| :-: |
| [**Page 14**]() |

Properties of a good loss

• The purpose of a loss

function is to quantify how

well our model is

performing

• Properties of a good loss

function:

• Smooth and

differentiable

• Robust to noise/outliers

-----

|  |
| :-: |
| [**Page 15**]() |

Every loss encodes an assumption

• Loss functions correspond

to **noise models**

• L2 loss → Gaussian noise

• L1 loss → Laplace noise

• Cross-entropy →

categorical uncertainty

• Choosing a loss is choosing

which errors are plausible

-----

|  |
| :-: |
| [**Page 16**]() |

Why squared error is a modelling choice

MSE causes outliers to dominate learning.

-----

|  |
| :-: |
| [**Page 17**]() |

Standard losses (recap)

L1 (mean absolute error)

1

L2 (mean squared error)

2

Huber loss (smooth L1)

3

ℒ\! = ð¦\! − ðð½(ð¥\!)

ℒ\! = ð¦\! − ðð½ ð¥\!

&

ℒ\! =

1

2

ð¦\! − ð' ð¥\!

&

,

ð¦\! − ð' ð¥\!

\< ð¼

ð¦\! − ð' ð¥\!

−

1

2

,

ðð¡ℎððð¤ðð ð

**Always interrogate** whether their

**assumptions** match the data and task.

-----

|  |
| :-: |
| [**Page 18**]() |

Domain-specific losses in healthcare

-----

|  |
| :-: |
| [**Page 19**]() |

Segmentation in healthcare

• Connects perception to

action

• Important use cases:

• Quantify tumour burden

• Radiotherapy planning

• Measure disease

progression

• Extract meaningful

biomarkers

-----

|  |
| :-: |
| [**Page 20**]() |

Segmentation as overlap, not classification

• **Segmentation** is a pixel-wise classification problem

• We can use **pixel/voxel-wise cross entropy**

• Overlap-based losses have been proposed to address **class**

**imbalance**

Image

Ground Truth

Prediction

-----

|  |
| :-: |
| [**Page 21**]() |

From classification to overlap

-----

|  |
| :-: |
| [**Page 22**]() |

Dice Loss: What it optimises (and why)

**Canonical definition (set-based)**

For binary segmentation with ground truth ð¦$

∈ 0,1 and

prediction &ð¦$ ∈ 0,1 :

ð·ððð(ð¦, &ð¦) =

2ð∩=ð

ð + =ð

\=

2ðð

2ðð + ð¹ð + ð¹ð

**Differentiable (soft) Dice loss (used in practice)**

For probabilistic predictions &ð¦$ ∈ \[0,1\]

ℒ

3

4$5'

\=1−

2∑

$

6

ð¦$&ð¦$ + ð

∑

$

6

ð¦

$

\-

\+ ∑

$

6

&ð¦

$

\-

\+ ð

ð

\=ð

ð ∩=ð

Converts from a similarity index to

a **dissimilarity index** (the goal is to

*minimise* the loss)

**Note:** ð¦%, Fð¦% ∈ 0,1

ð = number of pixels/voxels

Foreground overlap matters more than pixel-wise correctness

-----

|  |
| :-: |
| [**Page 23**]() |

Multi-class Dice: Correcting for size bias

Errors on rare or small structures matter more

**Canonical formulation (Generalised Dice Loss)**

For ð¾ classes:

ℒIJ4

\=1−2

∑

K-%

L

ð¤K

∑

,

ð¦,K

Dð¦,K

∑

K-%

L

ð¤K

∑

,

(ð¦,K

\+ Dð¦,K

)

With class weights:

ð¤K

\=

%

∑

\!

N

\!"

\#

or sometimes

%

∑

\!

N\!"

ð

\=ð

ð∩=ð

Sudre, Carole H., et al. "Generalised dice overlap as a deep learning loss function for highly unbalanced segmentations." Deep learning in medical image analysis and

multimodal learning for clinical decision support. Springer, Cham, 2017. 240-248.

-----

|  |
| :-: |
| [**Page 24**]() |

Tversky Loss: Encoding Asymmetric Risk

Explicitly weights FPs and FNs asymmetrically

Weights false negatives (FN) higher than false positives (FP):

ℒOPQRSKN

\=1−

∑

,

.

ð¦,

Dð¦,

\+ ð

∑

,

. ð¦,

Dð¦,

\+ ð¼∑

,

.(1 − ð¦,

)Dð¦,

\+ ð½∑

,

. 1− Dð¦,

ð¦,

\+ ð

ð¼ and ð½ control the magnitude of penalties for FPs and FNs, respectively

Useful if the goal is to put emphasis on the network finding all the lesions

(potentially, at the expense of the overall segmentation)

Salehi, Seyed Sadegh Mohseni, Deniz Erdogmus, and Ali Gholipour. "Tversky loss function for image segmentation using 3D fully convolutional deep networks." International

Workshop on Machine Learning in Medical Imaging. Springer, Cham, 2017.

FP

FN

TP

-----

|  |
| :-: |
| [**Page 25**]() |

Beyond overlap: When not all errors are equal

• Dice and Tversky treat all

misclassifications as equally

bad

• This may not always be the

correct assumption

• Example: Brain tumour

segmentation

-----

|  |
| :-: |
| [**Page 26**]() |

Wasserstein-based Losses: Encoding Semantic Structure

Prefers predictions that are structurally meaningful

Takes into account the inter-class

relationships

Balances misclassifications to favour

predictions that are semantically

meaningful

Incorporates semantic similarity between

classes using a Wasserstein distance

Fidon, Lucas, et al. "Generalised Wasserstein Dice score for imbalanced multi-class segmentation using holistic convolutional networks." International MICCAI Brainlesion

Workshop. Springer, Cham, 2017.

-----

|  |
| :-: |
| [**Page 27**]() |

What these losses have in common

• During training, predictions .ð¦ are continuous probabilities

• Thresholding is applied only at inference

• Same underlying pattern

• All losses are about **task definition**

• The optimiser will enforce their definitions exactly

Tools for aligning **optimisation** with **clinical intent**

-----

|  |
| :-: |
| [**Page 28**]() |

Metrics and validation as

modelling decisions

-----

|  |
| :-: |
| [**Page 29**]() |

Loss ≠ metric ≠ deployment criterion

• Training loss: what the optimised minimises

• Shapes gradient

• Chosen for optimisation

• Validation metric:

• Shapes what we report as “performance”

• Chosen for interpretation

• Deployment criterion: how decisions are made in practice

• Triggers actions

• Encodes risk and responsibility

Misalignment here is a primary cause of failure in

healthcare DL

-----

|  |
| :-: |
| [**Page 30**]() |

Loss ≠ metric ≠ deployment criterion

• A model can train

perfectly, but still be unsafe

to deploy

• Metrics are modelling

decisions

• Optimisation does not “fix”

a bad objective

• If loss or metric is misaligned

with the clinical goal, errors

will be entrenched

• Failure of problem

formulation and

measurement

Why this distinction matters

Loss optimisation is faithful, not

corrective

-----

|  |
| :-: |
| [**Page 31**]() |

Why “good performance” can be meaningless

• Metrics are proxies, not truth

• Metrics measure ***something***

• They do not automatically measure ***what we care about***

• Poor metric choice is a major cause of translation failure

• When we report a metric, we are answering:

• Which errors are being counted?

• How are they weighted?

• Over which (sub-)population are they averaged?

Misalignment at any stage can lead to misleading conclusions.

-----

|  |
| :-: |
| [**Page 32**]() |

Common metric failure modes

Problem formulation is wrong\!

Maier-Hein et al. ”Metrics reloaded: recommendations for image analysis validation." *Nature Methods* 2024

-----

|  |
| :-: |
| [**Page 33**]() |

Common metric failure modes

Measurement is wrong\!

Maier-Hein et al. ”Metrics reloaded: recommendations for image analysis validation." *Nature Methods* 2024

-----

|  |
| :-: |
| [**Page 34**]() |

Common metric failure modes

Measurement has failed\!

Maier-Hein et al. ”Metrics reloaded: recommendations for image analysis validation." *Nature Methods* 2024

-----

|  |
| :-: |
| [**Page 35**]() |

Concrete metric pitfalls

• Why AUROC can be

misleading in clinical settings

• AUROC measures ranking quality

• Clinical decisions require

thresholds

• Thresholds encode asymmetric

risk

Pitfall 1: Threshold-free metrics vs. thresholded decisions

A high AUROC does not imply a safe

operating point

-----

|  |
| :-: |
| [**Page 36**]() |

Concrete metric pitfalls

• Operating points encode **risk**

Pitfall 1: Threshold-free metrics vs. thresholded decisions

Low

threshold

High

threshold

Who bears the harm changes with the threshold.

More false positives

More false negatives

False positives → unnecessary tests, anxiety, resource use

False negatives → missed disease, delayed treatment

-----

|  |
| :-: |
| [**Page 37**]() |

Concrete metric pitfalls

• Training and validation do not need the same metric

• Training loss chosen for optimisation properties

• Validation metric chosen for domain relevance

• Matching them by default is unjustified

Pitfall 2: Matching loss to metric “because it’s convenient”

-----

|  |
| :-: |
| [**Page 38**]() |

Validation is not neutral

• In healthcare,

consider:

• Which dataset you

validate on

• Which metric you

choose

• How you aggregate

performance

[Figure sourc](https://differ.blog/p/cross-validation-in-machine-learning-why-it-s-a-must-ab02e9)e

-----

|  |
| :-: |
| [**Page 39**]() |

What counts as a data sample?

[Image credit: https://doi.org/10.1016/j.neuroimage.2019.1163](https://doi.org/10.1016/j.neuroimage.2019.116324)24

1 3D brain MRI volume with 256 slices

≠ 256 data samples

Stack of

256 s
