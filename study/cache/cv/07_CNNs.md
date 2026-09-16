# Computer Vision — CNNs
> Source: Google Drive file 1bmKzlH3qu7d8i7yFMQ4-mjWjNwqb4s2o · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Convolutional Neural Networks

Computer Vision – Lecture 07

1

Further Reading

• Slides from F Li and slides from M Niessner

• Slides from E Gavves

• Deep Learning Book, by G,B,C, Chapter 9

• Foundations of Computer Vision, Torralba, Isola, Freeman

2

Convolutional Filters

• We have seen many useful convolutional filters:

• Gaussian Blur

• Edge Filters

• Sharpening

• Laplacian of Gaussian

• Gradient Filters

• …

• They have been hand-crafted from equations and intuitions.

3

Image Classification in 2 Steps

1\. Compute image embeddings. 2. Learn a classifier on the training set.

Many different approaches Image embeddings: FFT, BoW, HOG, Fisher Vectors, etc… Classifiers: Linear Regression, SVMs, Kernel SVM, Random Forest, etc…

4

Biological Motivation

Receptive fields of single neurones in the cat's striate cortex, D. H. Hubel and T. N. Wiesel, 1959

• Measure single neuron excitement in the visual cortex.

• Neurons respond to oriented edges

5

Biological Motivation

6video source

Edge “Filters”

• A individual neuron responds to a quite precise angle of the edge.

• There are neurons for every angle.

• Remember: SIFT Descriptor.

7

Neocognitron

A neural network, inspired by Hubel and Wiesel (1959):

• Cascaded structures: hierarchical and multi-layer

Fukushima, K. "Neocognitron: A hierarchical neural network capable of visual pattern recognition." Neural networks 1.2 (1988): 119-130.

higher order features

8

Neocognitron

A neural network, inspired by Hubel and Wiesel (1959):

• Cascaded structures: hierarchical and multi-layer

• Different types of alternating “cells” • Simple extract (modifiable S-cells: local parameters) features • Complex shift-invariance C-cells: • Arrangement each i.e. shared local responding set connections of weights

in cell-planes, to a with feature, each cell with a local connection area

ensure tolerance to small shifts of feature in the connection area

Cells on one S-plane fire on the same feature Each C-plane is a blurred version

of its corresponding S-plane 9 Fukushima, K. "Neocognitron: A hierarchical neural network capable of visual pattern recognition." Neural networks 1.2 (1988): 119-130.

10 Fukushima, K. "Neocognitron: A hierarchical neural network capable of visual pattern recognition." Neural networks 1.2 (1988): 119-130.

Neocognitron

Local features are gradually integrated and classified in higher layers: • Basic features (edges, corners, etc.) in lower layers • Global patterns in higher layers

Self-organizing maps: • Initially no supervision (1980) • Trained layer wise (1988)

Towards CNNs

Convolutional Neural Networks (CNNs, LeCun 1989) are a category of multi-layer NNs with learnable weights and biases, designed such that they tackle common problems of ANNs.

• Observation: Inputs are structured, e.g. images

• Key idea: Invariance to shifts, scale and small distortions using

• local weighted connections, i.e. local receptive field

• shared weights across spatial locations

• spatial sub-sampling

• Main operations:

• Convolutions

• Non-linearities

• max ∙ functions

11

CNN Architecture

Network architecture generally composed by:

• “Filters” arranged in three dimensions: width, height and depth.

• Alternating convolutional (followed by a non-linear activation function) and sub-sampling layers to produce features at different levels of abstraction.

• Fully-connected layers that act as the final classifiers.

Input Output

Layer Layer . . . CNN

Prediction (e.g. dog)

12

CNN Architecture

• CNN architectures are generally composed of:

• “Filters” arranged in three dimensions: width, height and depth.

• Alternating convolutional (followed by a non-linear activation function) and sub-sampling layers to produce features at different levels of abstraction.

• Fully-connected layers that act as the final classifiers.

Sample CNN structure

Convolution

G

Subsample

Convolution

Subsample

Fully-connected

Prediction:

Dog

13

LeNet-5

• First successful modern CNN architecture

• Introduced in 1998 for handwritten digit recognition

• Trained with back-propagation and gradient descent

LeCun et al. "Gradient-based learning applied to document recognition." Proceedings of the IEEE 86.11 (1998): 2278-2324.

14

15

Convolutional Layer

Main operation of CNNs

• Local Connectivity

Each field) neuron and the of dot a layer product connects is performed only to between a local region this region of the and previous the learnable layer (receptive weights.

• Weight Sharing

The same weights are used for every spatial location in the input volume.

\+∞

\+∞ ð ð¥,ð¦ ∗ ð ð¥,ð¦ = ෍෍ð ð,ð ∙ ð ð¥ − ð,ð¦ − ð

ð=−∞

ð=−∞

• Before: apply the same filter to every channel.

• Now: filters will have separate weights for every channel.

16

Convolutional Layer

Input volume (e.g. image)

learnable weights

ð

(parameters)

ð¤13 ð¤23 ð¤33ð¤12 ð¤22 ð¤32ð¤63ð¤ð¤41 11 ð¤ð¤51 21 ð¤ð¤61 31

ð¤ð¤6922

ð¤93

ð¤71 ð¤81 ð¤91

convolutional filter ℎ × ð¤ × ð

17

Convolutional Layer

slide filter over inputlearnable weights

(parameters)

convolutional filter ℎ × ð¤ × ð Input volume (e.g. image)

ð × ð × ð

Output (feature map) ðð × ðð × ð

ð × ð × ð

The filter slides spatially but operates (dot product) on all dimensions

18

Convolutional Layer

Input volume (e.g. image)

zero-pad each border of the input by ℎ − 2 1

, ð¤ − 1

2 to retain the same size in the output

ðð × ðð × ð

convolutional filter ℎ × ð¤ × ð

ð × ð × ð

Output (feature map) ðð × ðð × ð

19

Convolutional Layer

set of filters

Output (feature maps)

learning multiple (different) filters → produce several feature maps → multitude of features

20

Input volume (e.g. image)

Output (feature map)

Convolutional Layer

Learnable parameters i.e. the weights of the filters biases added afterwards

Other hyperparameters

• spatial extend: width ð¤, height ℎ number of channels: depth ð • number of filters ð • Stride ð  (step size) stride \> 1 results in spatial sub- sampling of the feature maps • Padding ð on the input (on every side)

Each filter learns to activate on some sort of feature

Size of resulting feature maps:

ℎðð¢ð¡ = ℎðð − ð  ℎ + 2ð

\+ 1

ð¤ðð¢ð¡ = ð¤ðð − ð  ð¤ + 2ð

\+ 1

where height ℎand ðð,ð¤width ðð,ℎðð¢ð¡of input ,ð¤ðð¢ð¡ and

are the

expected output respectively

21

Practical Considerations

• Common filter sizes are 3 × 3, 5 × 5, etc. 1 × 1 is also possible because it operates in depth too.

• The third dimension ð is almost always the same as the number of channels in the input (but not necessarily).

• Padding does not need to be symmetric (but usually is).

• Stacking convolutions extracts features with a progressively higher level of abstraction.

22

First Layer Filters

First-layer filters from AlexNet (visualization of 96 \[11 × 11 × 3\] filters):

Krizhevsky, Sutskever, Hinton, "Imagenet classification with deep convolutional neural networks." NeurIPS 2012.

First-layer learned features include basic elements, such as edges, blobs, colors, etc.

Parameter sharing thus appears to be reasonable: detecting e.g. an edge is important at any position of the input image.

23

Activation Function

• Convolutions are linear operations

• Stacking them will still only give us a linear operation.

• Add a non-linear activation function in between.

Tanh: tanh(ð¥) = 2ð 2ð¥ − 1

Output range: \[-1,1\]

These functions saturate, making gradients very small → learning is very difficult.

Sigmoid: ð ð¥ = 1

1+ð−ð¥ Output range: \[0,1\]

24

Rectified Linear Unit (ReLU)

Rectified Linear Unit (ReLU)

• Simply thresholds at zero

ð ð¥ = max 0,ð¥

• Sparse activation

derivative = 1

• Computationally efficient

derivative = 0

• Non-saturating → speeds up convergence

25

Other Activation Functions

26 image source

Pooling Layers

• Idea: reduce the resolution to understand content at different scales.

• Idea: reduce the resolution to save computations.

• Performs an element-wise operation on the feature maps in a local region, on each channel independently.

• Usually: ð¦ðð± ∙ or ðð¯ð  ∙ .

27

Max-Pooling Example

max value within the window

Example: Max-pooling

The window size is 2 × 2, applied with a stride of 2 (common case)

28

Pooling Layer

• Parameter-free layer

• Used for feature map spatial sub-sampling (with stride \> 1).

• Controls the capacity of the network by reducing the resolution.

• Introduces because precise some spatial invariance information to small is transformations lost. of the input, • Hyperparameters:

• width ð¤ and height ℎ of window

• stride overlapping occurs ð  if ð  \< of ð¤ ðð sliding ð  \< ℎ

window Size of resulting pooled maps:

ℎðð¢ð¡ = ℎðð ð  − ℎ

\+ 1

ð¤ðð¢ð¡ = ð¤ðð ð  − ð¤

\+ 1

29

Fully Connected Layer

• Fully-connected layers follow the principle of the typical ANN weighted connections: each neuron in the output connects to all neurons of the input.

• Usually added as the last layers of the network / output layer.

• Implemented as a linear function, plus bias, followed by a non- linearity.

• Guarantee a full receptive field.

30

Fully Connected Layer

Input ℎ × ð¤ × ð (here: 5 × 5 × 1)

Can be also seen as a convolutional layer with a FC

set of filters of the same size as the input volume, i.e. ð filters of size ℎ × ð¤ × ð

Output 1 × 1 × ð ð being the only hyperparameter (here: ð = 6)

31

CONV 5x5x1 +ReLU8 filters/maps

size: 24x24

INPUT

(24x24)

Notice how feature maps activate on different basic structures, depending on the corresponding filter

32

Source A. Karpathy

8 filters/maps

size: 24x24

INPUT

CONV 5x5x1

\+ReLU

(24x24)

POOL 2x2

stride 2

(12x12)

spatial sub-sampling by 2

33 Source A. Karpathy

8 filters/maps

size: 24x24

INPUT

CONV

12 filters/maps

CONV

POOL 5x5x1

5x5x8

3x3

\+ReLU

\+ReLUstride 3

(24x24)

(12x12)

(12x12)

POOL 2x2

stride 2

FC can be also modeled as 4x4 convolutions (no padding, stride=1)

(4x4)

34 Source A. Karpathy

FC10 filters/ outputs

(1x1) 0123456789

Loss function

• A CNN can be learned for different problems (classification or regression ones) by minimizing a specified objective, i.e. the loss function.

• It simply measures how well the CNN performs on the task.

• To do this, a “loss layer” receives the output of the CNN (prediction) and compares it to the ground truth of the given input.

• Stochastic Gradient Descent: the loss over the entire dataset must be written as the mean of the individual losses of the samples.

InputTraining

ð¥ð ð¦ð = ð(ð¥ð,ð) pair

ð¦ð∗

Ground truth

Prediction

CNN estimator of function ð

ℒ(ð¦ð,ð¦ð∗)

Loss function 35

Loss function

• A CNN can be learned for different problems (classification or regression ones) by minimizing a specified objective, i.e. loss function.

• It simply measures how well the CNN performs on the task.

• To do this, a “loss layer” receives the output of the CNN (prediction) and compares it to the ground truth of the given input.

• The loss over the entire dataset is (most often) the mean of the individual losses of the samples.

• Example: If our task is image classification,

• the ground truth is the labeled category for the image • the prediction is a vector of scores, which represent the “probabilities” that the input belongs to each of the existing categories.

36

Loss function

• Classification: soft-max cross-entropy (Lecture 06)

• Regression:

• for tasks where the output is continuous.

• ℒ1 ð,ð∗ = ð − ð∗ 1 = 1ðσð=1 ð ð¦ð − ð¦ð∗

• ℒ2 ð,ð∗ = ð − ð∗ 2 = 1ðσð=1 ð ð¦ð − ð¦ð∗ 2

• Note that ð,ð∗ can have arbitrary dimensions depending on the task, e.g. vectors of regressed points or entire prediction maps. ð would then be the number of points or pixels respectively.

• Task-specific loss functions that model some known properties of the problem.

37

In an over-fitted model, the predicted curve is not “regular” Weights have very large or very small values

https://msdn.microsoft.com/en-us/magazine/dn904675.aspx

Regularization

Helps generalization to unseen data, i.e. preventing over- fitting to the training samples.

38

Regularization

• It over-fitting includes methods to the training for better samples. generalization to unseen data, i.e. preventing • L2 regularization

If ð is too large, the networks tries to keep weights too small

• Penalty term: ð is the regularization ð = 12ðð¤strength 2 (the squared (typically magnitude small, e.g. of οrder all parameters) of 10−4)

• Favors weight “diffusion”

• Weight (linear decay) update through gradient descent: ð¤ð¡+1 = ð¤ð¡ − ðð¤t • L1 regularization

• Penalty term: ð = ð ð¤

• Causes weight vector to become sparse and invariant to noisy inputs

39

Dropout

• Randomly (with probability “dropping ð, usually out” neurons 0.5) at each of a iteration layer of training

• This they effectively do not contribute means making in forward/backward them inactive passes (setting to zero) so that • Neurons do not learn to rely on the presence of other specific neurons

• Usually applied before the last fully-connected layer(s)

without dropout

Srivastava, Journal of Machine Hinton, Krizhevsky, Learning Research Sutskever, 15.1 Salakhutdinov, (2014)

"Dropout: a simple way to prevent neural networks from overfitting."

with dropout

dropout not applied to the final prediction\! 40

Optimization methods

For a training iteration ð¡ and the current state of parameters denoted as ð¤ð¡, an update is performed as: ð¤ð¡+1 = ð¤ð¡ + Δð¤t A variety of first-order solvers, popular for training CNNs:

• Stochastic Gradient Descent (SGD) Follow the negative gradient for a “mini-batch” of samples Δð¤ð¡ = −ððð¡

• Requires manual setting of learning

• Manual annealing: decrease learning rate, if validation curve “plateaus” to prevent parameters from oscillating near local minima

• SGD with momentum Keep in memory previous weight updates Δð¤ð¡ = ðΔð¤ð¡−1 − ððð¡

• → Accelerates SGD progress when gradient points in the same direction as before and dampens oscillations

Rumelhar, Hinton, Williams, "Learning representations by back-propagating errors." Nature 323 (1986): 533-536.

41

Adam (Adaptive Moment Estimation)

Additionally keep an exponentially decaying average of previous gradients:

ðð£ð¡ ð¡ = = ð½ð½21ð£ðð¡−1 ð¡−1 + + 1 1 − − ð½ð½1 2 ððð¡ ð¡2 → → ෞ ð£ෞðð¡ ð¡ = = ðð£ð¡ ð¡ Τ Τ 1 1 − − ð½ð½2ð¡ 1ð¡

Suggested decay: ð½1 = 0.9, ð½2 = 0.999. Initial averages: zeros

Kingma and Ba. "Adam: A method for stochastic optimization." ICLR‘15.

1st moment (mean) 2nd moment (variance)

Δð¤ð¡ = − ෝð£ð¡ ð+ ð ðð¡ bias correction

42

How to train your network

Looking for the right learning rate…

extremely high learning rate: training

“exploding” gradients objective (loss)

low learning rate:

As for the validation curve, if it “plateaus” then decrease the learning rate

may never reach optimum performance

high learning rate: big step down and then caught on local minimum

good learning rate

iterations (epochs)

43

How to train your network

Validation vs Training (when data comes from the same distribution)

objective

objective (loss)

(loss)

iterations (epochs)

44

Human performance

train val

overfitting the

training data\!

variance

bias

If bias is high: Train a bigger model or train longer

If variance is high: Try more data, augmentations, regularization (e.g. dropout)

If overfitting: Try more data or early stopping

How to train your network

When data comes from different distributions…

Distribution \#1 Train setVal set

Distribution \#2 Trainval set

Test set• If val error high: Get more data of distribution \#2 (similar to the test scenario)

• If val error low, but test error high: Get more validation data

45

Architecture Example: VGG

Very Deep Convolutional Networks for Large-Scale Image Recognition, Simonyan and Zisserman, 2014

• Different configurations: 11-19 layers

• 3x3 convolutions

• 3 large FC layers in the end

46

Architecture Example: ResNet

Deep Residual Learning for Image Recognition, K He et 
