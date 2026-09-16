# DL4H — L9-10: Low-Data Regimes, Transfer Learning & Domain Adaptation
> Source: Google Drive file 10nKxRSfg45Axf2xBl0ks5Mu_t2I2mZ2i · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Low-data regimes: Self-Supervised Learning, Transfer Learning, and Domain Adaptation 

|  |
| :-: |
| [**Page 1**]() |

Ana Namburete

Department of Computer Science

University of Oxford

**Deep Learning in Healthcare**

Low-data regimes:

Self-Supervised Learning, Transfer

Learning, and Domain Adaptation

-----

|  |
| :-: |
| [**Page 2**]() |

What if…

• … we could reuse what we learned?

• … we could be less dependent on the dataset size?

• … we could extrapolate to unseen pathologies and

phenotypes?

• … we could extrapolate to unseen image properties and

modalities?

• … we could do all of the above with **limited training data**?

Slide credit: Jorge Cardoso, Emma Robinson

-----

|  |
| :-: |
| [**Page 3**]() |

Hierarchical Feature Representation

Low-level features

Mid-level features

High-level features

**Initial layers** learn simple, generic

features (e.g. edges, blobs)

**Deeper layers** learn more specialised

features, and are generally more

*dataset-specific*

-----

|  |
| :-: |
| [**Page 4**]() |

Self-supervised learning:

Labels from structure

-----

|  |
| :-: |
| [**Page 5**]() |

Learning labels from structure

• In medical imaging settings:

• Manual annotation is

expensive

• Labels are scarce or

unavailable

• Two broad approaches:

• Unsupervised learning

• Provides weak training signal

• Self-supervised learning

• Labels generated from the

data itself

-----

|  |
| :-: |
| [**Page 6**]() |

Learning labels from structure

• Self-supervised learning (**SSL**):

• A form of representation learning

• Supervision is created from the structure of the data

• No manual annotation is required

Key idea:

1\. Define a pretext task whose labels

are known by construction

2\. Train a neural network to solve this

task

3\. Discard the task, keep the learned

representation

ðð½

Encoder

ðð½

Transfer

-----

|  |
| :-: |
| [**Page 7**]() |

Pretext Tasks

• **Pretext task:** an artificial task designed to force the

network to learn meaningful structures in the data

Solving the jigsaw

Image rotation

Relative positioning

-----

|  |
| :-: |
| [**Page 8**]() |

Masked autoencoding for MRI

• Randomly remove or mask regions of an MRI volume

• Train the network to reconstruct the missing voxels

Forces the model to learn:

• Global anatomical structure

• Long-range spatial dependencies

• Modality-specific intensity patterns

Particularly effective for:

• 3D medical imaging

• Small labelled datasets

Example

-----

|  |
| :-: |
| [**Page 9**]() |

Contrastive learning for CT

• Generate multiple views of the same scan using augmentations

• Train the network to bring these representations closer together

• Push representations of different scans apart

Example

Encourages:

• Scanner-invariant features

• Robust representations

• Improved transfer across tasks and sites

Particularly effective for:

• Large unlabelled CT archives

• Multi-centre datasets

https://www.sciencedirect.c

0031320321000352

-----

|  |
| :-: |
| [**Page 10**]() |

Autoencoders: Generative SSL

Learn by reconstructing input

• **No labels required**

• **Forces encoder to capture**

**structure**

\!ð¥∈ℝ

\!

ð¥∈ℝ

\!

ð§∈ℝ

"

Encoder, ð¸\! ð¥ =ð§

ℒ(ð¥, )ð¥)

e.g.,

Decoder, ð·" ð§ = 'ð¥

Training objective:

min

\#,%

ð¼&\~ð

ð¥ − ð·%

ð¸\#

ð¥

)

)

-----

|  |
| :-: |
| [**Page 11**]() |

The Bottleneck Forces Structures

• Bottleneck forces compression

• Compression forces structure

• Keep the encoder, discard the

decoder

Key structural constraint:

dim ð§ =ð ≪dim ð¥ =ð

\!ð¥∈ℝ

\!

ð¥∈ℝ

\!

ð§∈ℝ

"

Encoder, ð¸\! ð¥ =ð§

ℒ(ð¥, )ð¥)

e.g.,

Decoder, ð·" ð§ = 'ð¥

-----

|  |
| :-: |
| [**Page 12**]() |

Autoencoders for Representation Learning

• After training, discard

decoder

ð§∈ℝ

"

Encoder, ð¸\! ð¥ =ð§

Decoder, ð·" ð§ = 'ð¥

-----

|  |
| :-: |
| [**Page 13**]() |

Autoencoders for Representation Learning

ð

ð¾, ð

\!ð¦

ð¦

ℒ(ð¦, )ð¦)

Cla

ssifie

r

En

c

o

d

e

r

• After training, discard

decoder

• User encoder as feature

extractor

• Fine-tune with small labelled

dataset

-----

|  |
| :-: |
| [**Page 14**]() |

Contrastive Representation

Learning

-----

|  |
| :-: |
| [**Page 15**]() |

Contrastive Learning

• Given a pre-selected **similarity function**, ð ( ⋅ , ⋅), we wish to

learn an encoder function ð that yields:

• A high score for positive pairs (ð, ð

()

• A low score for negative pairs (ð, ð

)) such that:

ð  ð ð ,ð(ð() ≫ ð  ð ð ,ð(ð))

-----

|  |
| :-: |
| [**Page 16**]() |

ðð½

ð  ℎ\*,ℎ(

ð  ℎ\*,ℎ)

**minimise**

**maximise**

ℎ\! = ð"(ð\!)

ℎ\# = ð"

(ð\#)

ℎ$ = ð"

(ð$)

Encoder

Positive:

ð

\*

Anchor:

ð

\+

Negative:

ð

,

-----

|  |
| :-: |
| [**Page 17**]() |

Triplet Loss

• Triplet loss:

ℒ-./012-

ð, ð

\*

,ð

,

\= \<

&∈ð³

max 0, ð ð −ð ð

\*

)

)

− ð ð − ð ð

,

)

)

\+ ð

Schroff et al. FaceNet: A Unified Embedding for Face Recognition and Clustering. *CVPR* 2015 [(](https://arxiv.org/abs/1503.03832)[https://arxiv.org/abs/1503.038](https://arxiv.org/abs/1503.03832)32)

-----

|  |
| :-: |
| [**Page 18**]() |

Contrastive Learning

• Given:

ð³= ð,

ð(,

ð+

),…,ð,)+

)

1 “anchor” sample

1 positive sample (ð − 1) negative samples

• Compute this **multi-class cross-entropy loss**:

• More commonly known as **InfoNCE loss**\*

ℒ = −ð¼ð³ log

exp ð  ð ð ,ð ð$

exp ð  ð ð ,ð ð$

\+ ∑

%&'

()' exp ð  ð ð ,ð ð

%

)

\= −ð¼ð³ log

exp ð  ð ð ,ð ð$

∑

%&'

(

exp ð  ð ð ,ð ð%

• Its negative is a lower bound on the mutual information between ð ð and ð(ð$)

ðð¼ ð ð ,ð ð$

≥ log ð −ℒ

\* Also known as:

• Contrastive loss

• N-pair loss

• Consistency loss

• Ranking-based NCE

Oord, Li and Vinyals: Representation Learning with Contrastive Predictive Coding. Arxiv, 2018.

-----

|  |
| :-: |
| [**Page 19**]() |

SimCLR

Apply two random

augmentations to the input

image:

ð\! = ð\! ð

ð" = ð"(ð)

Image embeddings

Projection network projects the

image embeddings into a space

where contrastive learning is applied

Loss enforces

similar

embeddings for

augmented

images (i.e.

coming from the

same input

image)

Chen et al: A Simple Framework for Contrastive Learning of Visual Representations. ICML, 2020. [(](https://arxiv.org/abs/2002.05709)[https://arxiv.org/abs/2002.057](https://arxiv.org/abs/2002.05709)09)

ℎ%

ℎ&

Contrastive

loss

[Image credi](https://medium.com/mlearning-ai/self-supervised-pre-training-with-simclr-79830997be34)t

-----

|  |
| :-: |
| [**Page 20**]() |

SimCLR

Chen et al: A Simple Framework for Contrastive Learning of Visual Representations. ICML, 2020. [(](https://arxiv.org/abs/2002.05709)[https://arxiv.org/abs/2002.057](https://arxiv.org/abs/2002.05709)09)

-----

|  |
| :-: |
| [**Page 21**]() |

Learning representations with

limited labels

-----

|  |
| :-: |
| [**Page 22**]() |

Learning new tasks relies on previous task(s)

Single-task learning

Credit: A survey on Transfer Learning

Learning

system 1

Learning

system 2

Learning

system 3

Learning

system 1

Learning

system 2

**Knowledge**

**Different tasks**

**Source task(s)**

Traditional ML

Transfer Learning

**Target task**

-----

|  |
| :-: |
| [**Page 23**]() |

Hierarchical Transferability

*Earlier layers → more generic*

≈ basis functions

*Later layers → task-specific*

≈ tightly coupled with

source task’s objective

NN representations

are hierarchical

Transferability decreases with depth

-----

|  |
| :-: |
| [**Page 24**]() |

Fine-tuning and freezing layers

• Start with a **pretrained model** that produces good results

• Initialise a model with the pretrained model weights and **fine-**

**tune**

Figure credit: Dive into Deep Learning

• Only train (or fine-tune) a subset of

layers

Advantages:

• Reduce training time

• Limited hyperparameter tuning

-----

|  |
| :-: |
| [**Page 25**]() |

Freezing/Fine-tuning as Bias-Variance Trade-off

• Freezing layers

• Higher bias

• Lower variance

• Fine-tuning layers

• Lower bias

• Higher variance

Input

FC

Output

Input

FC

Output

Input

FC

Output

ð¥

Fine-tune

ð¥

ð¥

Freeze

❄

Freeze

❄

Fine-tune

ð¥

ð¥

Strategy depends on:

• Size of the target dataset

• Similarity between source and target tasks

-----

|  |
| :-: |
| [**Page 26**]() |

Representation Mismatch

• ImageNet pre-training

• Optimised for object

category separation

• High semantic diversity

• Medical imaging

• Low inter-class diversity

• Strong anatomical priors

(within each modality)

• Subtle intensity

differences matter

Representation mismatch motivates medical pre-training

-----

|  |
| :-: |
| [**Page 27**]() |

Transfer as Representation Specialisation

• SSL learns generic

structure

• Transfer learning

specialises it

• Adapts

representation to

solve a task

ð¥

ð"(ð¥)

ð"(ð¥)

-----

|  |
| :-: |
| [**Page 28**]() |

Medical Example: Med3D

Example: **Med3D**

Transfer knowledge from 8 tasks to the segmentation of a lung nodule dataset

Chen et al. Med3D: Transfer learning for 3D medical image analysis. *arXiv* 2019 [(](https://arxiv.org/pdf/1904.00625.pdf)[https://arxiv.org/pdf/1904.00625.](https://arxiv.org/pdf/1904.00625.pdf)pdf)

-----

|  |
| :-: |
| [**Page 29**]() |

Practical Strategy

• Strategy depends on target dataset size

Large labelled target set

⟹ Fine-tune entire network

Very small labelled target set

⟹ Freeze most layers

⟹ Train task head

Moderate labelled target set

⟹ Freeze early layers

⟹ Fine-tune deeper layers

Input

FC

Output

Input

FC

Output

Input

FC

Output

ð¥

Fine-tune

ð¥

ð¥

Freeze

❄

Freeze

❄

Fine-tune

ð¥

ð¥

-----

|  |
| :-: |
| [**Page 30**]() |

Domain Adaptation

The **task stays the same**, but the **data distribution changes**.

-----

|  |
| :-: |
| [**Page 31**]() |

Domain Shift

Credit: Kamnitsas et al., Deep Learning Tutorial, IEEE NPSS (2019)

T1-w

T1-w

T2-w

T2-w

**Distribution shift** occurs when the training and test distributions are different

That is, ð\*+, ð¥,ð¦ ≠ ð\*-.\*(ð¥, ð¦)

The most common causes are: (1) sample selection bias, or (2) methodological differences (e.g.

scanner type, imaging protocol)

-----

|  |
| :-: |
| [**Page 32**]() |

Domain Adaptation

• The size of the shift is often measured by the distance between source and target subspaces

• A typical approach is to learn a feature space transformation to align the source and target

representations (reduce domain divergence)

Credit: Jorge Cardoso, Emma Robinson

**Goal:**

Train a NN on a source dataset, and achieve good accuracy on a target dataset that is

significantly different from the source

-----

|  |
| :-: |
| [**Page 33**]() |

Adversarial Domain Adaptation

ð½"

Feature extractor

(domain)

ð½"

Feature extractor

(network)

**Source**

**domain**

**Target**

**domain**

Credit: Hung-Yi Lee

\* Learn to ignore intensity differences

-----

|  |
| :-: |
| [**Page 34**]() |

Adversarial Domain Adaptation

ð½"

Feature extractor

(domain)

ð½"

Feature extractor

(network)

Different

**Source**

**domain**

**Target**

**domain**

Same distribution

Credit: Hung-Yi Lee

\* Learn to ignore intensity differences

-----

|  |
| :-: |
| [**Page 35**]() |

Architecture Split

ð½"

Feature extractor

Credit: Hung-Yi Lee

ð½\#

Label predictor

**45 yo**

ℒ$%&'

-----

|  |
| :-: |
| [**Page 36**]() |

Training Setup

ð½"

Feature extractor

Credit: Hung-Yi Lee

ð½\#

Label predictor

**45 yo**

**Source**

**domain**

**(labelled)**

**Target**

**domain**

**(unlabelled)**

ℒ$%&'

-----

|  |
| :-: |
| [**Page 37**]() |

Embedding Inspection

ð½"

Feature extractor

Credit: Hung-Yi Lee

Separable by scanner and sex

ð½\#

Label predictor

**Class distribution:**

**45 yo**

ℒ$%&'

-----

|  |
| :-: |
| [**Page 38**]() |

Domain Classifier

ð½(

Domain classifier

Credit: Hung-Yi Lee

ð½"

Feature extractor

ð½\#

Label predictor

**45 yo**

**Source**

**or**

**target?**

ℒ$%&'

ℒ()\*%+\!

-----

|  |
| :-: |
| [**Page 39**]() |

Adversarial Domain Adaptation

ð½(

Domain classifier

Credit: Hung-Yi Lee

ð½

(

∗

\= min

ð½\!

ℒ+,-.

− ðℒ/01,23

ð½4

∗ = min

ð½ð

ℒ+,-.

ð½"

Feature extractor

ð½\#

Label predictor

**45 yo**

ℒ$%&'

ð½/

∗ = min

ð½\#

ℒ/01,23

ℒ()\*%+\!

**Source**

**or**

**target?**

min

5\!,5$

max

5\#

ℒ+,-.

− ðℒ/01,23

-----

|  |
| :-: |
| [**Page 40**]() |

Adversarial DA Objective

min

,\!

, ,"

max

,\#

ℒ$%&'

ð"

,ð\#

− ð ℒ()\*%+\!

ð"

,ð(

• **Feature extractor & label predictor:**

• Minimise task loss, ℒ'\!()

• Maximise domain confusion, ℒ\*+,\!%-

• **Domain classifier:**

• Minimise domain loss, ℒ\*+,\!%-

• ð controls **task-invariance trade-off**

-----

|  |
| :-: |
| [**Page 41**]() |

Adversarial Domain Adaptation

B

e

fo

re

A

fte

r

Scanner and Sex

Age

[Dinsdale, Jenkinson, Namburete](https://doi.org/10.1016/j.neuroimage.2020.117689).

*[NeuroImag](https://doi.org/10.1016/j.neuroimage.2020.117689)e*[, 20](https://doi.org/10.1016/j.neuroimage.2020.117689)21

Source 1

Source 2

Source 3

Whitehall II

-----

|  |
| :-: |
| [**Page 42**]() |

Example: DA for Brain segmentation

Source model

**applied** to

Target data

Source model

**transferred** to

Target data

Model

**trained** on

Target data

(from scratch)

Ground Truth

T1-w

FLAIR

Train: T1; Test: FLAIR

Train: FLAIR; Test: T1

T1→FLAIR

FLAIR→T1

T1→T1

FLAIR→FLAIR

Karani et al. 2018 https://arxiv.org/pdf/1805.10170.pdf

-----

|  |
| :-: |
| [**Page 43**]() |

When domain adaptation fails

**Small domain gap**

**Large domain gap**

**Same label distribution**

✅ DA works well

⚠ DA may help;

Diminishing returns

**Different label distribution**

⚠ Label shift:

DA alone insufficient

❌ DA likely to fail

(negative transfer)

-----

|  |
| :-: |
| [**Page 44**]() |

Learning Strategies in Low-Data Regimes

**Source Data**

**Target Data**

**Strategy**

✅ Labelled

✅ Labelled

Fine-tuning

Multi-task learning

❌ Unlabelled

✅ Labelled

Self-supervised pre-

training + fine-tuning

❌ Unlabelled

❌ Unlabelled

Contrastive learning,

clustering

✅ Labelled

❌ Unlabelled

Adversarial domain

adaptation

-----

|  |
| :-: |
| [**Page 45**]() |

Appendix

-----

|  |
| :-: |
| [**Page 46**]() |

Families of Self-Supervised Learning

**Family**

**Core idea**

**Example**

Predictive

Predict part of the data from other parts

Context prediction,

inpainting, jigsaw puzzles

Generative

Reconstruct the input data

Autoencoders, masked

autoencoding

Contrastive

Bring similar representations closer

together

Push dissimilar representations apart

SimCLR

These categories are not mutually exclusive.

-----

|  |
| :-: |
| [**Page 47**]() |

How transferable are features?

• Source: 500 classes from ImageNet

• Target: another 500 classes from ImageNet

Yosinki et al. How transferable are features in deep neural networks. NIPS 2014. https://arxiv.org/abs/1411.1792

-----

|  |
| :-: |
| [**Page 48**]() |

Freezing too many layers

• Source: 500 classes from ImageNet

• Target: another 500 classes from ImageNet

Yosinki et al. How transferable are features in deep neural networks. NIPS 2014. https://arxiv.org/abs/1411.1792

Layer transfer = 0

(training from scratch)

Train the remaining layers on

target data from scratch

• Copy **first** ð **layers** from

source network

• **Freeze** copied layers

• Train remaining layers on

target data

**Observation (red curve):**

• Copying early layers helps

slightly

• Copying too many layers

**hurts performance**

**Key point:**

• Early layers are generic

• Later layers are task-specific

-----

|  |
| :-: |
| [**Page 49**]() |

Fine-tuning helps

• Source: 500 classes from ImageNet

• Target: another 500 classes from ImageNet

Yosinki et al. How transferable are features in deep neural networks. NIPS 2014. https://arxiv.org/abs/1411.1792

Layer transfer = 0

(training from scratch)

Fine-tune the whole network

(incl. copied layers)

Train the remaining layers on

target data from scratch

• Copy layers from source

network

• **Fine-tune all layers,**

including copied ones

**Observation (pink curve):**

• Consistent performance

improvements

• Outperforms layer freezing

**Key point:**

• Transfer + fine-tuning \>

transfer + freezing

• Adaptation matters

-----

|  |
| :-: |
| [**Page 50**]() |

Effect of source-target dissimilarity

Yosinki et al. How transferable are features in deep neural networks. NIPS 2014.

https://arxiv.org/abs/1411.1792

• Source and target tasks increasingly

different

**Observation:**

• Early layers remain transferable

(orange curve)

• Transferred weights \> random

initialisation (green curve)

**Key point:**

• Generic features transfer even across

distant tasks

• Prior structure is bett
