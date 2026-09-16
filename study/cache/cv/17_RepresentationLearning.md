# Computer Vision — Representation Learning
> Source: Google Drive file 1lA3iDfdQUaHNrECY_MOzlQeAfLM_B151 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Representation Learning

Computer Vision – Lecture 17

1

Further Reading

• Slides from S Savarese, A Zamir

• Slides from F Li

• Slides from A Geiger

2

So far: Task Learning

• Learn a function from input to task output.

3

“Transcript”

Macbeth was guilty.Slide adapted from S Savarese

Cat

So far: Task Learning

• Learn a function from input to task output.

• Representation Learning: general representation + task head4

Representation Mathematical Model

(e.g., classifier)

\[ 81 20 84 64 58 39 17 54 72 15\]

“Transcript”

Macbeth was guilty.Slide adapted from S Savarese

Cat

Representations

5 Slide adapted from S Savarese

\~5.4 kg

\~3.6 kg

X XXX X XXX X XX X X XXX X XX XXX X

XX X 0 3 5

7 +10 ð¤

Representation Mathematical Model

(Classifier)

Type A Weight (ð¤)

ð¤\>5

Type B

Representation Learning

Supervised

• Given a task, learn a representation for it.

• Representation is often constrained to task(s).

• today

Unsupervised

• Given only data, find a representation for it.

• Representation often does not align exactly with tasks.

• Part of Lecture 18

6

Handcrafting Representations

• Was the only way for a long time.

• (almost) Worked for many important applications: • Image Retrieval • Structure-from-motion • Face detection • etc.

• Why alternatives? • Can’t quite find the discriminative signature for a problem. • Discriminative signature can be found, but hard to approach programmatically. • Too many contributing factors to the problem.

• Fusion non-trivial. Rule-based fusion outruled.

• Fusion of contributing factors itself a comparably complex representation problem.

7

Correspondences

Point correspondences estimated by a classic algorithm: SIFT

8

Recall: SIFT Descriptor

• Compute edge orientations and global orientation.

• Rotate all edges so that the global orientation is “up”.

• Split the local area around the keypoint into 4x4=16 regions.

• Compute edge histograms (8 directions) for each region.

• Concatenate histograms: descriptor 128 dimensional vector.

9

Learning a Keypoint Descriptor

• Use a dataset with point correspondences.

• Extract patches around keypoints.

• Positives from matching keypoints.

• Negatives from random keypoints.

• Train a model to predict the similarity between two patches.

Zagoruyko & Komodakis. 2015.

10

Local Feature Learning Dataset

11

Brown, Hua, Winder, Discriminative Learning of Local Features, 2011

Zagoruyko & Komodakis. 2015.

Low-level matching architectures

12

Zagoruyko & Komodakis. 2015.

Low-level matching: qualitative results

13

Zamir et al. 2016.

Handcrafted vs Learned features

14

K. M. Yi, E. Trulls, V. Lepetit, P. Fua, LIFT, 2016

LIFT: Learned Invariant Feature Transform

● Learn a keypoint detector.

● Learn a keypoint orientation predictor.

● Learn a keypoint descriptor.

15

LIFT

● Works well in domains close to the training data.

● Slower than SIFT.

16

Representation Learning Losses

● Given a set of samples ð¥ð we learn a function that maps each sample into an embedding space ð ð¥ð = ðð ∈ ℝð.

● To learn ð we need a loss function that acts on representations.

● Training data comes with positive ð¥ð,ð+ and negative examples ð¥ð,ð− for each sample ð¥ð (or you can construct them easily).

17

ð¥ð ð¥ð,ð+ ð¥ð,ð−

Cosine Similarity

● Cosine similarity: cosine of the angle between embedding vectors.

● Cosine is 1 if the embeddings align, 0 if orthogonal, -1 if opposite.

ð ð¥ = ð ෠ð = ðð

ð®cos ðð,ðð = ෠ððð ෠ðð

18

Cosine Similarity

● For each sample, we maximise the similarity with its positives, and minimise similarity with its negatives.

ℒcos ðð = − ð½1ð ð½ð

෍ð®cos ðð,ðð,ð+ ð=1

\+ ð¾1ð ð¾ð

෍ð®cos ðð,ðð,ð− ð=1

● Often select one random positive and one random negative for faster loss approximation.

ℒcos ðð = −ð®cos ðð,ðð+ + ð®cos ðð,ðð−

19

Negatives

● Why do we need negatives?

● Degenerate solution: ð ð¥ = ð predicts a constant for all ð¥.

ℒcos ð(ð¥ð),ð(ð¥ð) = −ð®cos ð,ð = −1

● This minimises the loss for all training samples

● But: the representation is useless.

20

Triplet Loss

● Cosine similarity forces positive pairs to be almost identical (colinear) and negatives to be fully dissimilar.

● Often: select one random positive and one random negative for faster loss approximation.

● Triplet: anchor, positive, negative (ð,ð+,ð−)

● Idea: relative loss.

● Similarity between positive pair should be greater than similarity of negative pair.

21

Triplet Loss

Similarity between positive pair should be greater than similarity of negative pair.

ð

ð−

ℒtriplet ð,ð+,ð− = max 0,ð® ð,ð− − ð® ð,ð+ + ð

ð+

Minimum: if ð® ð,ð+ \> ℒtriplet ð® ð,ð= − 0

\+ ð for a margin ð \> 0.

training

Can use any similarity/distance metric :

ð− max 0, ð − ð+ − ð − ð− + ð

ð

ð+

22

Similarity vs. Distance

● Similarity

○ Cosine similarity, correlation

○ Intersection over Union

○ …

● Distance

○ Euclidian distance (L1, L2, …)

○ Manhattan distance

● Remember: minimise distance, maximise similarity.

23

Efficiency Considerations

● The triplet loss uses three function evaluations for each loss ð(ð¥),ð(ð¥+),ð(ð¥−).

● Can we do better?

● ð ð¥ = ð is slow, while ℒ ⋅ is much faster in comparison.

● Find a way to use each ð multiple times.

● Idea: in a training batch, we can use most other samples as negatives too.

24

Efficiency

● Construct a training batch such that

○ each sample ð¥ð has exactly one positive pair ð¥ð+

○ all other samples ð¥ð (and ð¥ð+) are negatives to ð¥ð (and ð¥ð+)

○ Example: include exactly two images of each class.

● Now we can reuse the computed embeddings for every sample

෍ð≠ð

ℒtriplet ðð,ðð+,ðð + ℒtriplet ðð,ðð+,ðð+

● Batch of 6ð samples. Before: 2ð loss evals . Now: 4ð(2ð − 1) 25

Contrastive Loss

● Simplify notation: ð+ is the index of the positive pair to ð.

−log exp ð® ðð,ðð+

σð=1 ðµ exp ð® ðð,ðð

● Minimised by large numerator and small denominator.

● Same ides: maximise ð® ðð,ðð+ and minimise all other similarities.

26

Recall: Softmax Cross-entropy loss

Soft-max classifier for ð¾ classes ð¶ð:

ð ð¶ð ð¥ = softmaxð ð(ð¥) = expðð(ð¥) σðexpðð ð¥ Cross-entropy:

−෍ðð¾

ððºð(ð¶ð,ð¥)log ð ð¶ð ð¥

Since all ððºð(ð¶ð|ð¥) are zero, except the target class ð¶ðºð,i.e. ððºð ð¶ðºð,ð¥ = 1 , this simplifies to −log ð ð¶ðºð ð¥ = −log expððºð ð¥ σð expðð ð¥

27

Contrastive Loss

−log exp ð® ðð,ðð+

σð=1 ðµ exp ð® ðð,ðð

• Classifier where the logits are replaced by similarities.

• ðµ-way classifier with one positive target per sample.

• Find the positive sample among all others.

28

Contrastive Loss

● Naming is confusing and inconsistent.

● Noise Contrastive Estimation (Gutmann, Hyvarinen, 2010)

○ Learn to separate data and noise with logistic regression.

● Proper name: InfoNCE (“CPC”, van den Oord, et al., 2018)

○ Use soft-max crossentropy to find positive sample within the batch.

● Popular loss: now often simply called contrastive loss.

29

Multi-Modal Representation Learning

● Goal: learn a common embedding space for different modalities.

● Typical setup:

○ one encoder per modality.

○ Train contrastively using matching pairs across modalities.

● Strong representations as they relate information from multiple sources.

30

Radford et al., Learning Transferable Visual Models From Natural Language Supervision, 2021

CLIP: Contrastive Language-Image Pre-Training

● Learn a joint embedding space of images and text

● Double Contrastive loss: across text and images

● Trained on 400M Image-Text pairs.

31

CLIP Implementation

\# image\_encoder - ResNet or Vision Transformer \# text\_encoder - CBOW or Text Transformer \# I\[n, h, w, c\] - minibatch of aligned images \# T\[n, l\] - minibatch of aligned texts \# t - learned temperature parameter

\# extract feature representations of each modality I\_f = image\_encoder(I) \#\[n, d\_e\] T\_f = text\_encoder(T) \#\[n, d\_e\]

\# scaled pairwise cosine similarities \[n, n\] logits = dot(I\_e, T\_e.T) \* exp(t)

\# symmetric loss function labels = arange(n) loss\_i = cross\_entropy\_loss(logits, labels, axis=0) loss\_t = cross\_entropy\_loss(logits, labels, axis=1) loss = (loss\_i + loss\_t)/2

32

SigLIP

• Zhai et al., ICCV’23 (SigLIP2, arxiv’25)

• Possible improvement over CLIP (hard to tell)

• Focused on efficiency, multi-GPU training

• Back to negatives and positives instead of contrastive training

• Each entry in the matrix is a binary classifier

33

SigLIP implementation

\# img\_emb : image model embedding \[n, dim\] \# txt\_emb : text model embedding \[n, dim\] \# t\_prime, b : learnable temperature and bias \# n : mini-batch size

t = exp(t\_prime) zimg = l2\_normalize(img\_emb) ztxt = l2\_normalize(txt\_emb) logits = dot(zimg, ztxt.T) \* t + b labels = 2 \* eye(n) - ones(n) \# -1 with diagonal 1 l = -sum(log\_sigmoid(labels \* logits)) / n

34

Models learn to read

• Many examples of images containing text in the training data

• Models “learn to read”

• Easy adversarial examples

35

from SigLIP2 colab notebook

A Owens et al., Visually Indicated Sounds, 2015 Video source

Video and Sound

36

A Owens et al., Ambient Sound Provides Supervision for Visual Learning, 2016

Vision and Sound

37

Asano et al., Labelling unlabelled videos from scratch with multi-modal self-supervision, 2020

Multi-Modal Retrieval

● Combine multi-modal representation learning with clustering.

● Learn an audio-visual embedding from videos with sound.

Demo link

38

Asano et al., Labelling unlabelled videos from scratch with multi-modal self-supervision, 2020

Multi-Modal Retrieval

39

Ranking Loss

● What if we have multiple positives?

● We want the similarities of all positives to be greater than to all negatives.

● Sometimes, there is a ranking between positives.

● Ranking losses can be built from pairwise losses (e.g. triplet).

● Ranking useful to learn retrieval problems.

40

Brown, et al., Smooth-AP: Smoothing the Path Towards Large-Scale Image Retrieval, 2020

Representation Learning for Retrieval

41

www.inaturalist.org

Representation Learning for Retrieval

● Representation learning is very useful for retrieval problems.

● This is because there is usually not 
