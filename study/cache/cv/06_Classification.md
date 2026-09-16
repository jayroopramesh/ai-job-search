# Computer Vision — Classification
> Source: Google Drive file 1YBlwPehFgMH6fVQ-2kLCpnzQas_4HKZ5 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Image Classification

Computer Vision – Lecture 06

1

Further Reading

• Slides from A Zisserman and A Vedaldi

• Pattern Recognition and Machine Learning, C Bishop

• Deep Learning, Goodfellow, Bengio, Courville

2

So far

• We know a/one way to compare images:

• Compute a BoW descriptor for each image.

• This allows finding similar images: compute descriptor similarities

• Does this tell us if the image contains a cat?

• How do we know if the image contains a cat?

3

Image Embeddings

• Formally, we define a feature extractor ð: ℝð»×ð×3 → ℝð for images.

• ð maps images to d-dimensional descriptor vectors.

• A good ð maps similar images close-by in the feature space, while different image have large distances.

• BoW is an image embedding.

• Allows retrieval and many other applications.

4

Supervised Learning Summary

Dataset ð· = ð¥ð,ð¦ð 1 ≤ ð ≤ ð} Inputs ð¥ð Outputs ð¦ð Training/Validation/Testing ð· = ð·ð ∪ ð·ð ∪ ð·∗

Learn ð ð¥ = ð¦ by minimizing σ ð¥ð,ð¦ð ∈ð·ð ℒ(ð ð¥ð ,ð¦ð)

Hoping to generalise: σ ð¥ð,ð¦ð ∈ð·∗ ℒ(ð ð¥ð ,ð¦ð)

5

Supervised Learning - Data

CIFAR-10 dataset (Alex Krizhevsky, 2009)

• 60000 32x32 colour images

• 10 classes

• 6000 images per class

• 50000 training images

• 10000 test images

6

Image Embeddings

ð( )

7

ð( )

ð( )

ð( )

ð( )

ð( )

ð( )

ð( )

ð( )

ð( )

Nearest Neighbour Classification

• Embed a new sample with ð.

• Look up nearest neighbours in the embedding space.

• Predicted class is the majority vote of the neighbourhood.

• Can also return class distribution.

ð( )

8

Image Embeddings

ð( )

9

ð( )

ð( )

ð( )

ð( ) ð( )

ð( )

ð( )

ð( )

ð( )

ð( )

Nearest Neighbour Classification

3-NN Classification:

• ð ð¼,truck = 23

ð( )

• ð ð¼,car = 13

• ð ð¼,other classes = 0

10

ð( )

ð( )

ð( )

Nearest Neighbour Classification

Algorithm

Training:

• Precompute embedding samples. of the all feature training • Optional: lookup kd-trees).

data use structure a fast NN- (e.g. Testing:

• Compute the new image. the embedding for • Look class up histogram. k-NN and compute 11

Embedding Function Example

• We count the number of blue and green pixels.

• ð: ℝð»×ð×3 → ℝ2 is easy to visualise.

• We classify boats vs deer.

• How do we measure the quality of a classifier?

12

Green pixels

Blue pixels

Accuracy

We compute the number of samples the classifier ð predicts correctly.

Acc ð = |ð·1

∗| ð¥,ð¦∈ð·෍∗

ð¦ = ð ð¥

When expected the accuracy:

classifier predicts probabilities, EAcc ð we = |ð·1

∗| ð¥,ð¦∈ð·෍∗can also compute the ðð¦ ð¥ Where ðð¦ ð¥ is the predicted probability for class ð¦.

13

Precision and Recall

• Accuracy can be misleading when the label distribution is skewed.

• In a dataset where 90% of samples are of class 0, you can obtain 90% accuracy by always predicting 0.

• Precision: TP/(TP+FP)

• Recall: TP/(TP+FN)

14

Image source

ð-NN Classification

As ð increases:

• Classification boundary becomes smoother.

• Might improve or worsen performance.

Choose optimal ð on the validation set\!

15

Boats vs. Deer

ð-NN Summary

• ð -NN is simple but effective.

• Applies to multi-class classification.

• Decision surfaces are non-linear.

• Quality of predictions automatically improves with more “training” data.

• Only a single parameter, ð; easily tuned by cross-validation.

• Often used as a baseline classifier.

16

Image Classification in 2 Steps

1\. Compute image embeddings. 2. Learn a classifier on the training set.

Two directions for improvements:

• Find a better embedding function.

• Find a better classifier.

17

Linear Separability

Linearly separable Not linearly separable

18

Decision Boundaries

• Even if our data is linearly separable, we might have many choices to place the decision boundary.

Intuitions

good boundary – but why?

19

Maximum Margin

• If we assume some noise, tight boundaries can easily lead to miss-classifications.

• Both classifiers on the right have 100% accuracy.

• Maximum margin idea: place the decision boundary as far away from the samples as possible.

20

Maximum Margin

• Data points become support vectors for the decision boundary margins.

• We want to maximise the margin.

margin

21

Maximum Margin

• Data points become support vectors for the decision boundary margins.

• We want to maximise the margin.

smaller margin

22

Linear Support Vector Machine

• Binary classification dataset: ð¥ð,ð¦ð , 1 ≤ ð ≤ ð, ð¦ð ∈ {−1,1}

Two objectives:

• Classification accuracy

• Maximising margins

• Linear classifier: ð ð¥ = ð¤ðð¥ + ð

Margin: 2ð¤

23 Decision boundary: ð¤ðð¥ + ð = 0

Linear Support Vector Machine

Classification criterion:

෍ð

ð¦ðð(ð¥ð) = ෍ð¦ð ð¥ððð¤ + ð ≥ 1

ð This means and ð ð¥ð ≥ that 1 pushes ð¦ð and points ð(ð¥ð) should beyond have the the same sign (=class)

margin. Margin maximisation:

min ð¤ 2 Quadratic optimization problem with linear constraints. In general: there is a unique solution.

24

Training SVMs

Constraint: σðð¦ð ð¥ððð¤ + ð ≥ 1 Maximum margin: min ð¤ 2

Training loss: n1σðmax(0,1 − ð¦ð ð¥ððð¤ + ð ) + ð ð¤ 2

Hinge-loss

Hinge loss: gradient of -1 until constraint is fulfilled.

25

SVM Summary

• SVMs are good linear classifiers: maximum margin decision boundaries.

• Performance depends on the linear separability of the samples, thus on the image embedding function\!

• Kernel SVM: non-linear decision boundaries.

• Intuition: learn a non-linear mapping to a space where classes are linearly separable together with the SVM

26

vs ( & ) Multi-Class Classification

vs ( & )

• Setting: ð¾ \> 2 classes.

• Idea: each is train a binary ð¾ classifiers 1-vs-all ðð(ð¥), classifier.

• Classification: choose the class with the highest score

argmax

vs ( & ) ð ?

?

?

ðð(ð¥)

?

27

Multi-Class Classification

• Setting: ð¾ \> 2 classes.

• Idea: train ð¾ classifiers ðð(ð¥), each is a binary 1-vs-all classifier.

• Classification: choose the class with the highest score

argmax

ð ðð(ð¥)

28

Multi-Class Classification

Linear classifiers

ðð ð¥ = ð¤ððð¥ + ð

Vector form:

ð ð¥ =

ð¤⋮1ðð¤ð¾ð ð¥ +

ð⋮1ðð¾

\= ðð¥ + ðµ =

ð1 ⋮

ð¥= ð ෠ðð¾ ð¥

How prediction?

to we turn the class scores ෠ð into a single class 29

The soft-max Function

argmax

ð ෠ðð is not differentiable.

Idea: convert ෠ð into a probability distribution. All elements in (0, 1) and sum to 1.

softmaxð ෠ð = exp ෠ðð

σðexp ෠ðð

30

The soft-max Function

softmaxð ෠ð = exp ෠ðð

σðexp ෠ðð

• Result sums to 1.

• All values between 0 and 1.

• Works for any input in ℝð¾ (positive and negative).

• If one ෠ðð ≫ ෠ðð than all others, softmax “selects” this element: softmaxð ෠ð ≈ 1 and softmaxð ෠ð ≈ 0.

31

Temperature

Often a temperature parameter softmaxð ð,ð ෠= σexp ðð exp is ð෠ð

added ð෠ðð ðto the softmax function = softmaxð(ðð෠)

• Regulates the sharpness of the output distribution.

• Keeps relative ordering:

softmaxð ෠ð,ð1 \< softmaxð ෠ð,ð1 ⇒ softmaxð ෠ð,ð2 \< softmaxð ෠ð,ð2

• As ð → ∞ softmax becomes a uniform distribution

• As ð → 0 softmax becomes argmax (in a vector representation).

32

Temperature

The temperature controls the entropy of the resulting probability distribution.

33

Cross-entropy loss

Soft-max classifier for ð¾ classes ð¶ð:

ð ð¶ð ð¥ = softmaxð ð(ð¥) = expðð(ð¥) σðexpðð ð¥

Loss function:

• Idea: maximise the probability of the ground-truth class.

• Minimise cross-entropy between ground-truth probability distribution (one-hot) and the predicted distribution.

−෍ðð¾

ððºð(ð¶ð,ð¥)log ð ð¶ð ð¥

34

Cross-entropy loss

ð¾ −෍ððºð(ð¶ð,ð¥)log ð ð¶ð ð¥ ðSince this simplifies all ððºð(ð¶ðto

|ð¥) are zero, except the target class −log ð ð¶ðºð ð¥ = −log σexpððexpððºð ð ð¥

ð¥ = −ððºð ð¥ ð¶ðºð,i.e. ððºð ð¶ðºð,ð¥ ð¾ + log෍exp ðð ð¥ ð= 1 , ððºð ð¶ðºð ð¥
