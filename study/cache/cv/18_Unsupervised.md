# Computer Vision — Unsupervised Learning
> Source: Google Drive file 1IAk3rFzOgeohLEyFoce4A8xdqWgsUXsk · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Unsupervised Learning

Computer Vision – Lecture 18

1

Further Reading

• Slides from S Savarese, A Zamir

• Slides from F Li

• Slides from Y Asano

2

Basics: Supervised Learning

Dataset ð· = ð¥ð,ð¦ð 1 ≤ ð ≤ ð} Inputs ð¥ð Outputs ð¦ð Training/Validation/Testing ð· = ð·ð ∪ ð·ð ∪ ð·∗

Learn ð ð¥ = ð¦ by minimizing σ ð¥ð,ð¦ð ∈ð·ð ℒ(ð ð¥ð ,ð¦ð)

Hope to generalise: σ ð¥ð,ð¦ð ∈ð·∗ ℒ(ð ð¥ð ,ð¦ð)

3

Basics: Unsupervised Learning

Dataset ð· = ð¥ð 1 ≤ ð ≤ ð} Inputs ð¥ð Outputs ð¦ð Training/Validation/Testing ð· = ð·ð ∪ ð·ð Testing on downstream task ð = ðð,ðð 1 ≤ ð ≤ ð}

Learn ð ð¥ = ? by minimizing ??

Hope to generalise to another task σ ðð,ðð ∈ðℒ(ð ðð ,ðð)

4

What we need to do

• Trick the model to learn the downstream task without labels

• Build inductive biases into the model

• Find a learning signal for the training scheme

• Often: prevent trivial solutions and cheating

5

Learning Signal Toolbox

• Learning signals are general ideas to incorporate priors

• Priors model general assumptions about the world/task

This lecture contains a wide set of tools for learning from priors

• Can be used in all settings un/weakly/fully-supervised

• Not specific to tasks, apply to many areas

• For free\*\! (no annotations needed)

\*you still need to cite some papers 6

Learning Signal Toolbox

• Recovery: ð ð ð¥ \<-\> ð¥

• Bottleneck: ð ð ð¥ \<-\> ð¥ with restriction on ð(ð¥)

• Dataset: ð(ð¥1) \<-\> ð(ð¥2)

• Invariance: ð ð ð¥ \<-\> ð ð¥

• Equivariance: ð ð ð¥ \<-\> ð′ ð ð¥ often ð ≡ ð′ but not always

• Transformation estimation: ð ð ð¥,ð \<-\> ð

• Generative: ð(ð§) \<-\> ð·

• Task-specific: ð(ð¥) \<-\> priors

• Uncertainty: ð(ð¥) \<-\> own error

• Many more\!

7

Learning Signal Toolbox

Reconstruction

ð

8

Learning Signal Toolbox

Recovery

ð or

(Context autoencoder \[Pathak et al.; CVPR ‘17\], denoising autoencoder \[Vincent et al.; ICML ‘08\], Diffusion models \[Sohl-Dickstein et al., ICML ‘15\], etc.)

9

D. Pathak, P. Krahenbuhl, J. Donahue, T. Darrell, A. Efros. Context Encoders: Feature Learning by Inpainting. CVPR 2016

Rcovery: Inpainting

10

Recovery: Colorization

R. Zhang, P. Isola, and A. Efros, Colorful Image Colorization, ECCV 2016

11

R. Zhang, P. Isola, and A. Efros, Colorful Image Colorization, ECCV 2016

Colorization: Architecture

12

Failure Cases

Source: A. Efros, 13

R. Zhang

Inherent Ambiguity

Grayscale

14 Source: A. Efros, R. Zhang

Inherent Ambiguity

Prediction Ground Truth

15 Source: A. Efros, R. Zhang

Biases

Source: A. Efros, 16

R. Zhang

Biases

Source: A. Efros, R. Zhang

17

Learning Signal Toolbox

Bottleneck

ð ðLow dimensionality Sparsity Dictionary Task-specific …

18

Learning Signal Toolbox

Equivariance

ðð

ð

\* Often ð ≡ ð′

ð ð ð¥ = ð′ ð ð¥

ð′

ð′−1 ð ð ð¥ = ð(ð¥) is often more difficult because inverse is hard 19

Learning Signal Toolbox

Transformation Estimation

Rotation \[Gidaris et al.; ICLR ‘18\]

Jigsaw puzzle \[Noroozi & Favaro; ECCV ‘16\]

ð ?

ð ?

90o 180o 270o 0o

20

• Pretext task: randomly sample a patch and one of 8 neighbors

• Guess the spatial relationship between the patches

C. Doersch, A. Gupta, A. Efros. Unsupervised Visual Representation Learning by Context Prediction. ICCV 2015

Context prediction

A: Bottom right A: Top center

21

AlexNet-like architecture

softmax

shared weights

C. Doersch, A. Gupta, A. Efros. Unsupervised Visual Representation Learning by Context Prediction. ICCV 2015

Prevent “cheating”: sample patches with gaps, pre-process to overcome chromatic aberration

Context prediction: Details

22

Jigsaw puzzle solving

M. Noroozi and P. Favaro. Unsupervised Learning of Visual Representations by Solving Jigsaw Puzzles. ECCV 2016

Crop out tiles Shuffle Pretext task: reassemble

Claim: jigsaw solving is easier than context prediction, trains faster, transfers better

23

Predetermined set of 1000 permutations (out of 362,880 possible)

M. Noroozi and P. Favaro. Unsupervised Learning of Visual Representations by Solving Jigsaw Puzzles. ECCV 2016

Jigsaw puzzle solving: Details

24

Learning Signal Toolbox

Generative

GANs Variational Autoencoder

ð§

sampling ð§ ∼ ð ð,ð

ðº ð· ð¸ ððð· \[Goodfellow et al.; NeurIPS ‘14\]

\[Kingma et al.; ICLR ‘14\] Autoregressive

\[van den Oord et al.; ICML ’16, NeurIPS ‘16\]

real/fake?

ð¸

ð· 25

Diffusion Model

\[Sohl-Dickstein et al.; ICML ‘15\]

Learning Signal Toolbox

Dataset

\* Different definitions of “related” and “unrelated” samples exist

related

unrelated

ð

ð

ð

pullpush

“Contrastive”

26

ð

ð

• Introduce nonlinear projection (ð) between representation (ℎ) and feature used for computing contrastive loss (ð§).

• Use large mini-batch size.

27

T. Chen, S. Kornblith, M. Norouzi, and G. Hinton. A Simple Framework for Contrastive Learning of Visual Representations. ICML 2020

SimCLR

Learning Signal Toolbox

Invariance

ðð11Views Views

ðð2 2

\* Often with strong augmentations, but without changing the identity of the image

ððð ð

ð ð1 ð¥ = ð ð2 ð¥

28

SimCLR: Augmentations

T. Chen, S. Kornblith, M. Norouzi, and G. Hinton. A Simple Framework for Contrastive Learning of Visual Representations. ICML 2020

29

DINO: Self-Distillation with No Labels

• Student-Teacher training.

• Teacher’s weights are exponential moving average ð(EMA) of the student.

• Teacher sees global view.

• Student sees local view.

ð

• Student tries to predict teacher’s distribution.

30

EMA Loss

backprop

DINO – sharpening and centring

• Collapse: same prediction for all samples.

• Centring: ðð ð¥ð − 1ðσð=1 ð ðð(ð¥ð)

• Sharpening: low temperature for teacher softmax.

• Loss: Entropy between student and teacher distributions.

31

DINO features are popular

\[Tumanyan et al.; CVPR ‘22\]

\[Amir et al.; CVPR ‘22\]

\[Wang et al.; CVPR ‘22\]

32

Evaluation

• Occasionally simple: when training aligns fully with the task

• Often: some processing is needed

• Bridging the final gap between model and task

• In a practical setting: unsupervised learning is just the beginning

• In research: how far do we get with as little supervision as possible?

33

Unsupervised vs. Self-Supervised?

There is no common definition (and someone will always complain)\!

34

Unsupervised vs. Weakly Supervised

Weak supervision means supervision but for a different task

• Segmentation from bounding boxes/captions/classes

• (Dense) depth from stereo

• Captioning from object labels

• Human in the loop annotations

• Objects from sound

• …

35

Unsupervised Image Classification

? ð

36

Unsupervised Image Classification

ððð

Grouping Semantics

Class 42

Horse Assignments found with supervision

Cat

Class 27

Butterfly

Class 1 = Cat … Class 27 = Butterfly

Dog

Class 42

… Class 42 = Dog

Cow …

37

Hungarian Matching

• Find the lowest cost 1-to-1 assignments between ð clusters and ð labels.

• Cost: a ð × ð matrix ð¶ that contains the errors we induce when we match cluster ð to label ð.

• Find a row permutation matrix ð that minimizes the diagonal. minð Tr(ðð¶)

• Complexity: ðª(ð3)

38

Classifying Images without Labels

• Learn a self-supervised representation

• Loss: Neighbouring images same class + all classes have equal size

• Even better with self-training

\[Gansbeke et al.; ECCV ‘20\]

39

Labelling

\[Asano et al.; ICLR ‘20\]

Self-labelling by Clustering

Learning

CNN

“class 37”

update label alternate optimisation steps

assignment

update CNN

with

weights with

minð ð»(ð,ð) minð ð»(ð,ð)

(optimal

Cross-Entropy: ð» ð,ð = − ð1෍ð=1ð

෍ð¦

q(y|xi)logð(ð¦|ð¥ð,Θ)

transport problem)

“class 37”

40

Clusters are interpretable

cluster 1908, purity: 0.952 cluster 393, purity: 0.668 cluster 503, purity: 0.930

41

Clusters are interpretable

cluster 406, purity: 0.455

cluster 0, purity: 0.558 cluster 2568, purity: 0.377

42

GAN-based Segmentation

• ReDo: Layer-wise generative models for unsupervised object discovery

• Advantage: You get segmentation for free\!

• Drawbacks: fragile training, difficulty scaling due to custom architecture

Unsupervised object segmentation by redrawing M Chen, T Artières, L Denoyer, NeurIPS 2019

Chen et al. 2019

43

3D from a single image

3D ground truth or shape models

keypoints silhouettes

multi-view

camera viewpoint

depth maps

3D from a single image

3D ground truth or shape models

keypoints silhouettes

multi-view

camera viewpoint

depth maps

Unsup3D

Unsupervised Learning of Probably Symmetric Deformable 3D Objects from Images in the Wild, S Wu et al., CVPR 2020

Unsupervised Learning of 3D Objects

Training Data Output

instance-specific 3D shapes single-view images of a category

NO other supervision\!

Observation I

• Symmetry is a strong constraint\!

input

canonical view

flipped

47

Photometric method for determining surface orientation from multiple images Robert J Woodham, Optical engineering, 1980

Observation II

• Shading is a strong constraint\! (Shape from shading)

Photo-Geometric Autoencoding

input ð

Reconstruction Loss

reconstruction ð መ

encoder

decoder

encoder

view ð¤ texture

Renderer

encoder

decoder

depth ð

Photo-Geometric Autoencoding

input ð

Renderer

reconstruction ð

መencoder

encoder

encoder

decoder

decoder

view ð¤ depth ð

texture

Reconstruction Loss

Photo-Geometric Autoencoding

: input ð horizontal flip Reconstruction

Loss

reconstruction ð መ

encoder encoder

decoder

view ð¤ texture

flipped

encoder

decoder

depth ð

depth ð′

Renderer

flip switch

Photo-Geometric Autoencoding

: horizontal flip input ð

encoder encoder

decoder

view ð¤ texture

flipped

encoder

decoder

depth ð

depth ð′

Photo-Geometric Autoencoding

input ð

encoder

decoder

view ð¤ light ð albedo ð

Reconstruction Loss

reconstruction ð

መcanonical view ð

Renderer shading

encoder encoder

encoder

decoder

depth ð

depth ð′

: horizontal flip

flip switch

albedo ð′

Photo-Geometric Autoencoding

input ð

encoder

decoder

view ð¤ light ð albedo ð

Reconstruction Loss

reconstruction ð

መcanonical view ð

Renderer shading

encoder encoder

albedo ð′

encoder

decoder

depth ð

depth ð′

: horizontal flip

flip switch

Photo-Geometric Q3: Non-symmetric albedo, deformation, etc? Autoencoding

A3: Predict uncertainty

input ð

conf. ð

conf. ð′ view ð¤ light ð albedo ð

Reconstruction

flip switch

Loss

reconstruction ð

መcanonical view ð

Renderer shading

encoder

decoder

encoder encoder

albedo ð′

encoder

decoder

depth ð

depth ð′

encoder

decoder

: horizontal flip

Photo-Geometric Autoencoding

input ð

conf. ð

conf. ð′ view ð¤ light ð albedo ð

Reconstruction Loss

reconstruction ð

መcanonical view ð

Renderer shading

encoder

decoder

encoder encoder

albedo ð′

encoder

decoder

depth ð

depth ð′

encoder

decoder

: horizontal flip

flip switch

input reconstruction input reconstruction

<https://web.stanford.edu/class/cs331b/20
