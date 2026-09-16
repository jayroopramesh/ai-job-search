# DL4H — L5: Convolutional Neural Networks
> Source: Google Drive file 1SFWkvmcqKOuzSf9hR77CUNXjeI_H0BHy · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L5\_CNNs 

Deep Learning in Healthcare

Convolutional Neural Networks

Ana Namburete Department of Computer Science University of Oxford

Convolutional Fully-connected neural networks

neural networks (suitable for vectorised inputs)

(convolutional layers; suitable for image inputs)

ð¥\!ð¥"ð¥\#

Recurrent neural networks (model sequential relations; suitable for temporal inputs)

\!ð¦0

…

Input sequence

Output sequence

Different Classes of Neural Networks

Same pixel values, same intensity histogram, destroyed spatial structure

Why (medical) images are special

From Fully-connected NNs to CNNs

Pixel intensity ∈ \[0, 255\]

Most medical images are grayscale images, i.e. single channel

4 x 4 x 1

\[16 x 1\]

The problem with naïve modelling

Training a regular feed-forward network to predict if the input image is from one of 4 classes

4 classes (e.g. brain, heart, lungs, liver)

\[4 x 1\]

4 x 4 x 1

\[16 x 1\]

Dense connectivity

ð¾\[\!\]

ℎ\!\!

\[10 x 1\]

• All 16 input neurons are contributing to the computation of ℎ\!\! • ð¾\[\!\] will have 16×1×10 parameters to learn

• Becomes problematic when we have much larger images (typically \>200pix)

4 classes (e.g. brain, heart, lungs, liver)

\[4 x 1\]

FC will produce many dense connections

Why this is more than a scaling problem

• FC’s have no built-in notion of:• Spatial proximity

• Locality

• Repeated patterns

4 x 4 x 1

\[16 x 1\]

ð¾\[\!\]

ℎ\!\!

\[10 x 1\]

Key observations about images

• Two key ideas that simplify the way we process images with NNs

ℎ\!\!

First observation: We look for component features (e.g. skull, brain fold, ventricle) belonging to objects of a given class, regardless of their location in the image. We do not need to see the entire object to make a conjecture

Skull

Brain fold

Ventricle

4 x 4 x 1

\[16 x 1\]

Spatial Connectivity

ð¾(\!)

ℎ\!\!

• Take advantage of the spatial structure of an image

• Strong interactions with neighbouring pixels

• Only a few local nodes need to participate in the computation of ℎ\!\!

• E.g. for the edge of the skull, only pixels 1, 2, 5, and 6 need to be involved

\[10 x 1\]

• Sparser connectivity leads to fewer parameters in the model

Sparse Connectivity

Image credit: Goodfellow et al, 2016. Chapter 9

• It appears that we are losing information by dropping the connections

• E.g. Neurons ð¥- and x5 do not interact in layer 1

• BUT they contribute to ð., and so they do interact indirectly

Key Observations about Images Second observation: The same patterns may appear in different parts of an image

Left ventricle

It is unnecessary for every receptive field to have its own “left ventricle” detector

Image 2

Image 1

Weight-Sharing

\[16 x 1\]

1ð¾\[\!\] • Take advantage of the spatial structure 2of an image

• Strong interactions with neighbouring pixels

56• Only a few local nodes need to

participate in the computation of ℎ- -

• Ideally, filter should respond to the 11object in the same way, irrespective of where it is located in the image 12⇒ translation equivariance

1516

ℎ\!\!

\[10 x 1\]

• Sparser connectivity leads to fewer parameters in the model

Output does not change under a transformation of the input:

ð\! ð¡ ð¥ =ð\!(ð¥)

Desired for image-level tasks

Example: Chest X-ray disease classification

• Diagnosis should be unchanged if the image shifts slightly

Invariance vs Equivariance

Translation invariance Translation equivariance

Output transforms in the same way as the input

ð\! ð¡ ð¥ =ð¡ ð\! ð¥

Desired for pixel-level tasks

Example: Brain MRI segmentation

• If the image shifts, the segmentation mask should shift identically

• Fully-connected NNs use all pixels as a vector

• Structural information lost

• Fully-connected

ðð×ðð×ð

FCs CNNs

ðððð×ð

Why CNNs exist

• CNNs preserve the spatial structure

• Sliding window-based filters

• Invariant to translation, flipping, scaling, …

The Convolution Operation

• Convolution applies the same local linear operator across space

• Extracts local features via a sliding window

Input (feature) map

For a 2D input feature map, ð∈ℝ\!×\# and a

Filter

filter ð∈ℝ$×$:

$() $()ð ð,ð = ++ð¿ ð+ð,ð+ð ð¾ ð,ð

Output %&'

\*&'

(feature) map

Note: this is technically cross-correlation; the kernel is not flipped.

The Convolution Operation

• Slide the filter (kernel) over the input (raster scan)

• Each time, compute the dot-product between the filter (weight) values and the image region (i.e. receptive field)

⟹ one scalar value in the output

• The resulting output is called a feature map

Filter ð∈ℝ'×'

Input ð∈ℝ$×$

Output ð∈ℝ&×&

Stacked together, these form the feature volume of the 1st CONV layer

ð¿

ð¨ðð ð¨ðð ð¨ðð ð¨ðð

Input

CONV Layer is for Feature Extraction

1 ððððð

ð

ðð

\-1 0 1

\-1 -2 -1

\-2 1

ððð ð

\-2 0 2

0 0 0

\-2 4 -2 -1 0 1

1 2 1

1 -2 1 ðð ððð

ðð

ððð Smooth Edge detect Edge detect ‘Strong’ edge detect

Hyperparameters as design decisions

Input/output dimensions (1st constraint)

• Input dimensions

• Width (ð-) × Heigth (ð»-) × Depth (ð·-)

• Spatial extent of each filter: ð¹

• depth of each filter = depth of input

• Output dimensions

• Width (ð.) × Heigth (ð».) × Depth (ð·.)

• Stride: ð

• Number of filters: ð¾

ð(

ð¹

ð¹

Input ð∈ℝ)\!×\*\!×+\!

ð·\!

ð·\!

ð·(

Output ð∈ℝ)"×\*"×+"

Credit: Mitesh Khapra

ð»\!

ð\!

\*

ð»(

\=

Filter size F: Locality vs compute

• Consider a convolution between an image ð∈ℝ\!/×\#/ and a filter ð∈ℝ$×$

• Suppose we wish to compute the dimensions of the resulting feature map, ð∈ℝ\!0×\#0

Image credit: \[1\], Credit: Mitesh Khapra

Filter ð∈ℝ'×'

The output dimensions are:

ð1 = ð) −ð¹+1

ð»1 = ð») −ð¹+1

\* These formulas will be further refined

Input ð∈ℝ$×$ Output ð∈ℝ&×&

Stride S: Resolution vs information loss

• Stride: defines the interval at which the filter is applied

• ð denotes the number of pixels by which the window moves after each operation

• If (ð = 2), skip every 2nd pixel. This will produce a smaller output

The final formulas are given by:

ð1 = ð) −ð¹+2ð

ð + 1

ð»1 = ð») −ð¹+2ð

ð + 1

Credit: Mitesh Khapra

Padding P: Geometry and boundary effects

• Padding allows the output feature map to be the same size as the input

• Pad the inputs with an appropriately sized border so that the filter kernel can be applied to the corners of the image

Credit: Mitesh Khapra

The output dimensions are:

ð1 = ð) −ð¹+2ð+1

ð»1 = ð») −ð¹+2ð+1

\* These formulas will be further refined

Budget-aware design

Memory Footprint

• Activations (not parameters) dominate memory

• Feature maps stored for backpropagation

• Scales as:

• ðª ð⋅ð»⋅ð· in 2D

• ðª ð⋅ð»⋅ð⋅ð· in 3D

Training Stability

• Memory constraints → optimisation constraints

• Small batch sizes

• Noisy gradients

• Unstable BatchNorm

• ⇒ GroupNorm, InstanceNorm, careful LR schedules

Clinical feasibility

Can the model be used in the clinic?

• Clinical feasibility depends • Successful medical on:

imaging models:

• Available hardware and • Look conservative energy constraints

• Use simple, well-understood • Inference latency

building blocks

• Robustness to distribution shift

• Avoid unnecessary • Reproducibility across sites

complexity

• Maintainability over time

Favour alignment with clinical constraints over architectural novelty.

NOT suitable for CNN inference

DSPs / FPGAs / ASICs

Scanner (CT / MRI / US)

Typical NHS Compute Budgets

(Figures are order-of-magnitude; availability varies by Trust.)

\~10–50 GFLOP/s (CPU)

8–16 CPU cores, 16–32 GB RAM, no discrete GPU

PACS Workstation

\~8–30 TFLOP/s (FP16)

1× GPU (e.g. NVIDIA T4 / A10), 64–128 GB RAM

Departmental AI server

Central hospital server

Elastic 2–4× GPUs

GPU (A100 / A40 class)

instances

\~100+ TFLOP/s Scales, but latency

\+ cost constrained

Cloud inference (NHS)

Inference latency

• Inference time is governed by:

• Number of floating-point operations

• Memory access patterns

• Degree of parallelism

For a 2D convolutional layer, FLOPs scale approximately as:

and as ð¹'in 3D.

ðª ð⋅ð»⋅ð·\! ⋅ ð·( ⋅ ð¹(

Inference latency

Time delay

Start time (ð¡=0) Trained model End time (ð¡ = Latency)

Implication

• large kernels

• early high-resolution layers

• excessive channel widths all directly increase latency.

Left ventricle

Rule:

Do not downsample until the receptive field is at least as large as the smallest clinically relevant structure.

\* Downsampling is irreversible. Delay it until you’ve seen enough.

Design philosophy

Hyperparameters as capacity controls

• Kernel size, stride, padding, channels

• ⟹ define where and how much capacity is allocated

• Compute and memory constraints

• ⟹ restrict feasible architectures

• Low-data regimes

• ⟹ effective capacity ≠ nominal parameter count

Nominal ≠ effective capacity

• CNNs are typically over-parameterised

• Optimisation + regularisation

• Solutions lie in a much lower-dimensional subspace

• Small models trained from scratch

• Higher bias, poor conditioning

Let

ð = ð¥4,ð¦4 45- 6 , ð ≪ ð

Optimise min7 ℒ ð | ð Subject to implicit constraints from:

• Architecture

• Optimisation dynamics

• Regularisation

Capacity allocation as part of learning

• Over-parametrisation can aid optimisation

• Constraints during training

• ⇒ reduce variance, improve generalisation

• Capacity should emerge from data, not be fixed a priori

Key takeaway: CNN design in healthcare is budget-aware optimisation, not architecture minimisation.

Image source Variants of Convolution

1 Dilated (or atrous) convolutions • Introduces parameter rate an called additional the dilation • Dilation between rate values controls in a filter the spacing • Dilation convolution rate of 1 = standard • Subtly convolution different with from stride standard \>1

Examples: 3x3 filter kernel

Image source Variants of Convolution

2

3D Convolutions Slide the filters along 3 directions

Filter ð 3 x 3 x 3

(x, y, z)

3D volume

Input map

Filter 1 3 x 3 x 3

Feature map

(native volumetric reasoning)

1D Convolutions 3

Variants of Convolution

Depthwise Separable Convolutions 4

• Each filter processes a single input channel

• E.g. 3-channel input:

• Break the image into 3 different channels

• Apply a CONV to each channel

• Stack them together

Image source

Receptive Field + Pooling

Standard CNN architecture

• Alternating convolutional and pooling layers

• Architectural design was shaped by significant computational constraints

Input

S=1, F=5, K=6, P=0, Params = 150

What does a pooling (POOL) layer do?

S=1, F=2, K=6, P=0,

Params = 0 S=1, F=5, K=16, P=0,

Params = 2400

S=1, F=2, K=16, P=0, Params = 0

LeNet-5 (1998)

AlexNet (2012)

\*

Input

The Pooling Operation

1 1 2 4

\=

5 6 7 8

3 2 1 0

1 filter

1 2 3 4

Feature map (after convolution)

6 \*

8

3 4

Input

• Filters out details

• Introduces invariance to local minor modifications

• Makes the representations smaller

• Operates over each feature map independently

• Makes the features translation and scale-invariant

Alternatives to max-pooling, e.g.: - Average pooling - L2 pooling - Global pooling - Mixed pooling

The Pooling Operation

1 1 2 4

\=

5 6 7 8

max-pool

With 2x2 filters, 3 2 1 0

stride=2

1 filter

1 2 3 4

Size of resulting feature map:

ð,-. = ð/0 − ð¹

ð + 1

ð/0: width of input ð¹: filter width ð: stride

\*

Input

The Pooling Operation

1 1 2 4

\=

5 6 7 8

max-pool

6 8

With 2x2 filters, 3 2 1 0

stride=2

3 4

1 filter

1 2 3 4

1 1 2 4

5 6 7 8

3 2 1 0

1 2 3 4

max-pool

6 7 8

With 2x2 filters,

6 7 8

stride=1

3 3 4

where ð¹1: Filter width of layer ð ð/: Stride of layer ð

Example: ð\! = ð( = 3 and ð\! = ð( = 1 The receptive field of each element in layer 3 is ð' =1+ 2⋅1 + 2⋅1 =5 Source

Receptive Field

• The receptive field at layer ð is the region of pixel the of input the ð-th (denoted activation ð\>× ðmap \>) that each can 'see’.

\>

?B- ð\> =1+ B(ð¹?−1) Eð@

?5-@5A

How do we train a CNN?

Input Filter

a b c

w x

d e f

y z

j k m n

g h i

a b c d e f g h i

• A CNN can be implemented as a feedforward neural network but with sparse connections

• Only a few of the weights are active at a given time (in colour)

• The rest of the weights are set to zero (in gray)

How do we train a CNN?

Input Filter

a b c

w x

d e f

y z

j k m n

g h i

Output ja b c d e f g h i

• A CNN can be implemented as a feedforward neural network but with sparse connections

How do we train a CNN?

Input Filter

a b c

w x

d e f

y z

j k m n

g h i

Output

j k

a b c d e f g h i

• A CNN can be implemented as a feedforward neural network but with sparse connections

How do we train a CNN?

Input Filter

a b c

w x

d e f

y z

j k m n

g h i

Output

j k

a b c d e f g h i

m• A CNN can be implemented as a feedforward neural network but with sparse connections

How do we train a CNN?

Input Filter

a b c

w x

d e f

y z

j k m n

g h i

Output

j k

a b c d e f g h i

m n

• A but CNN with can sparse be implemented connections as a feedforward neural network • Can use backpropagation in the same way

ððð¥ðððð¿ ððð¿ð ð¶ððð ð =ððð¿ð ððð¥ðððð¿ ð¶ððð ð

max ð ð¥\! ,…,ð ð¥0 = ð max ð¥\!,…,ð¥0

Note: The order of pooling and activation layers technically does not matter.

Which order of layers should I use?

1 With MAXPOOL layer

CNN Architecture Design

Dt uoporððð¥ðððð¿ ððð¿ð ð¶ððð ð =ððð¿ð ððð¥ðððð¿ ð¶ððð ð

max ð ð¥\! ,…,ð ð¥0 = ð max ð¥\!,…,ð¥0

Note: The order of pooling and activation layers technically does not matter.

Which order of layers should I use?

1 With MAXPOOL layer

CNN Architecture Design

2 Replace POOL with

strided CONV

CONV / FC

BatchNorm

ReLU

3 With BatchNorm between

activation layer and Dropout

Normalisation without large batches

Batch Normalisation

• Normalises activations using mini-batch statistics

• Improves optimisation stability

• Enables higher learning rates

• Small batches lead to:

• Noisy gradient estimates

• Unreliable batch statistics

• Instability during training

What problem is BatchNorm trying to solve, at a high level?

Normalisation without batches

• Normalise across over the features/channels 1

Layer Norm (2016) ð = number of samples

\[ð, ð»\] = spatial dimensions ð¶ = number of channels

Note: More commonly used in training recurrent neural networks.

Source

Normalisation without batches

2 Instance Norm (2016) • Normalise across the activations in each channel

Source

Normalisation without batches

3 Group Norm (2018) • Computes the mean and standard deviation over groups of channels

• Does not assume that all channels equal importance

Outperforms BatchNorm on small batch sizes

Source

ðº = number of groups ⁄2 3 = number of channels per group

Normalisation

• Normalisation is NOT about fixing distributions

• It is about making optimisation feasible under real constraints.

Summary

• Modern CNNs follow a consistent pattern

• Decreasing resolution

• Increasing channels

• Growing receptive field

• Increasing invariance

References + Resources

• Textbooks:

• Goodfellow et al. Deep Learning: Chapter 9

• Resources:

• http://cs231n.stanford.edu/slides/

• http://introtodeeplearning.com/

• http://ufldl.stanford.edu/tutorial/

• http://playground.tensorflow.org/

• http://vision.stanford.edu/teaching/cs231n-demos/linear-classify/

Appendix

Backpropagation in CNNs

This is for conceptual completeness; you will not be examined on these derivations.

Backpropagation in a CONV Layer

• Suppose we have a grayscale image

• For simplicity, let :

• the number of CONV filters be 1

• ReLU activation function, ð ð¥ = max 0,ð¥

ð\!

\*

Input ð∈ℝ4\!×4"

ð\!

1 1 CONV filter

1

1 Input

Output ð∈ℝ4\!×4"

ð

\=

Credit: Dhruv Batra

ð\!

ð\!

ð(

ð¾\!ð¾(

Output ð∈ℝ5\!×5"

We can write an element of the output at position (ð, ð) as \*

ðð,ð = +%&'

Input ð∈ℝ4\!×4"

$\!() $"()ð\!

\+ð¿ ð−ð,ð−ð ð¾ ð,ð \*&'

Recall: Convolution Operation

• Consider a single CONV filter, ð∈ℝ./×.0

• Apply the filter to an image input, ð∈ℝ//×/0

• The output will be ð∈ℝ0/×00

1 filter

\=

(ð, ð)

Credit: Dhruv Batra

ð\!

ð\!

ð(

ð¾\!ð¾(

Output ð∈ℝ5\!×5"

Given a loss function ℒ(ð½), the goal is to calculate two gradients:

\!ℒð\!

\!\# and \* \!ℒ\!$ Input ð∈ℝ4\!×4"

Backpropagation in the CONV layer

• Consider a single CONV filter, ð∈ℝ./×.0

• Apply the filter to an image input, ð∈ℝ//×/0

• The output will be ð∈ℝ0/×00

1 filter

\=

(ð, ð)

Credit: Dhruv Batra

\* ð\!

Input ð∈ℝ4\!×4"

ð\!

ð\!

• The gradient of the loss wrt. a single weight in the CONV filter

ðℒ ðð¾ ð1, ð1

ð(

ð¾\!ð¾(

Output ð∈ℝ5\!×5"

(ð6,ð6)

\=

Gradient wrt. weights ðℒ ðð

Question: How many pixels in the output (ð) are affected by this weight?

ℎ 78\!

ℎ 7

ðℒðð

known unknown

Input ð¿∈ℝ4\!×4" ð\!

Output ð∈ℝ5\!×5"

ð\!

ð\!

• Assume that (ℒ(ð is known

• Because we compute gradients backwards from the last layer

\*

ð(

ð¾\!ð¾(

(ð6,ð6)

\=

By the chain rule, we can write 2ℒ

2ð¾(%\#,\*\#) as

ðℒ ðð¾(ð8, ð′) = :+9&' \!()

:+;&' "() ðð(ð, ðℒ

ð)

ðð(ð, ð) ðð¾(ð8, ð′)

Gradient wrt. weights

ðℒ ðð

ðℒðð

Input ð∈ℝ4\!×4" ð\!

Output ð∈ℝ5\!×5"

ð\!

ð\!

• Compute the unknown (ð(+,-)

(ð¾(/\!, 1\!)

\*

ð(

ð¾\!ð¾(

(ð6,ð6)

\=

Recall that

$\!() $"()ðð,ð = ++ð¿ ð−ð,ð−ð ð¾ ð,ð

%&'

\*&'

(by definition of the convolution operation)

So we can compute

ðð(ð, ð) ðð¾(ð8, ð′) = ð ∑$%&'

\!()∑$\*&'

"()ð¿ ð−ð,ð−ð ðð¾(ð8, ð′)

ð¾ ð,ð

\= ðð¾ð8,ð′ ð¿ ð−ð8,ð−ð′

ðð¾(ð8, ð′) =ð¿ ð−ð8,ð−ð′

Gradient wrt. weights

ðℒ ðð

ðℒðð

Input ð∈ℝ4\!×4" ð\!

Output ð∈ℝ5\!×5"

Full expression:

ðℒ ðð¾(ð8, ð′) = :+9&' \!()

:+;&' "() ðð(ð, ðℒ

ð)

ð\!

ð\!

ð(

ð¾\!ð¾( \*

ðð(ð, ð) ðð¾(ð8, ð′)

(ð6,ð6)

\=

We can hence write the gradient of ℒ wrt. weights as:

ðℒ ðð¾(ð8, ð′) = :+9&' \!()

:+;&' "() ðð(ð, ðℒ

ð)ð¿ ð−ð8,ð−ð′

\= ð¿ ∗ ðð ðℒ

Gradient wrt. weights

ðℒ ðð

ðℒðð

Input ð∈ℝ4\!×4" ð\!

Output ð∈ℝ5\!×5"

Full expression:

ðℒ ðð¾(ð8, ð′) = :+9&' \!()

:+;&' "() ðð(ð, ðℒ

ð)

ð\!

ð\!

ð(

ð¾\!ð¾( \*

ðð(ð, ð) ðð¾(ð8, ð′)

(ð6,ð6)

\=

We can hence write the gradient of ℒ wrt. weights as:

ðℒ ðð¾(ð8, ð′) = :+9&' \!()

:+;&' "() ðð(ð, ðℒ

ð)ð¿ ð−ð8,ð−ð′

\= ð¿ ∗ ðð ðℒThis is a convolution operation\!

Gradient wrt. weights

ðℒ ðð

ðℒðð

Input ð∈ℝ4\!×4" ð\!

Output ð∈ℝ5\!×5"

Full expression:

ðℒ ðð¾(ð8, ð′) = :+9&' \!()

:+;&' "() ðð(ð, ðℒ

ð)

ð\!

ð\!

ð(

ð¾\!ð¾( \*

ðð(ð, ð) ðð¾(ð8, ð′)

(ð6,ð6)

\=

Gradient wrt. weights

ðℒ ðð

We can hence write the gradient of ℒ wrt. weights as:

ðℒ ðð¾(ð8, ð′) = :+9&' \!()

:+;&' "() ðð(ð, ðℒ

ð)ð¿ ð−ð8,ð−ð′

\= ð¿ ∗ ðð ðℒThis is a convolution operation\!

Note, the gradient wrt. input feature map is ðℒ

ðð¿(ð6, ð′) = ðℒðð ∗ jlip\!9:° ð¾

Credit: Vineeth Balasubramian

Backpropagation in a POOL layer

• No weights to be learned in a pooling layer

• Simply need to propagate the gradients

• Max-pooling:

• Backpropagated gradient is assigned only to the winning pixel

• Average-pooling:

• Backpropagated assigned to all pixels gradient in the block

is divided by the area of the pooling block (ð×ð) and equally Forward propagation

Backpropagation

1 1 2 4

0 0 0 0

5 6 7 8

6 8

0 ððð¢ð¡ 0 ððð¢ð¡

backprop

3 2 1 0

3 4

ððð¢ð¡ 0 0 0

1 2 3 4

0 0 0 ððð¢ð¡ max-pool

6 8

With 2x2 filters, stride=2

3 4

Variants of Convolution

Depthwise Separable Convolutions 5

1x1x3 filter

Image source

• Depth and spatial dimensions of a filter can be separated

Variants of Convolution

Depthwise Separable Convolutions 5

1D Gaussian filterð¥-derivative

ð¦-derivative

1x1x3 filter

1D Gaussian filter

Image source

• Depth and spatial dimensions of a filter can be separated

Example: Sobel filter

\-1 0 +1 +1Sobel ð¥

\-2 0 +2

\-
