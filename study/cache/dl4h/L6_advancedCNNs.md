# DL4H — L6: Advanced CNNs through Inductive Biases
> Source: Google Drive file 12uBjqLx9oHGGfbR5Dk5e6XX3L_7PAskQ · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L6\_advancedCNNs 

Deep Learning in Healthcare

Advanced CNNs through Inductive Biases

Ana Namburete Department of Computer Science University of Oxford

What inductive bias means

Any assumption that restricts the class of functions a model can represent in order to generalise from finite data.

Left ventricle

Recap: CNN inductive bias

• Convolution

• ⟹ translation equivariance

• Pooling

• ⟹ translation invariance

Inductive bias \#1: Appearance matters, location does not

CNN evolution ≠ timeline CNN evolution

CNN evolution = assumptions

Architecture Year Inductive bias

LeNet 1998 Locality and weight-sharing

AlexNet 2012 Hierarchical features via depth + non-

linearity

VGG-Net 2014 Compositionality via small, repeated

kernels

GoogLeNet / Inception

2014 Multi-scale feature representations

ResNet 2015 Identity preservation by default

Multi-scale inductive bias

Example: Adult brain MRI

Example: Histopathology

Punctate microbleeds

Brain tumours

• The idea behind GoogLeNet (or InceptionNet) is not having to choose between these options

• This offers feature diversification

Parallel filters as a modelling assumption

• When an activation map is passed to 1

the next layer, there are a few options of operations to choose from:

i. Max-pooling layer ii. Or, 1 x 1 convolution iii. Or, 3 x 3 convolution iv. Or, 5 x 5 convolution v. Or, all of the above\!

5x5 CONV

1

3x3 CONV

1

1x1 CONV

1

MAX-POOL

Credit: Mitesh Khapra

W

H

ð¹

Can we reduce the number of computations?

D

1

5x5 CONV

1

3x3 CONV

1

1x1 CONV

1

MAX-POOL

Naïve Inception is expensive

• Naïve solution results in a large number of computations

• Let ð=0 and ð=1

• Each CONV of a W x H x D input with a ð¹ × ð¹ × ð· filter results in an output of size

ð −ð¹+1 ð» −ð¹+1

• Each element of the output, ð ð,ð , requires

ð¹×ð¹×ð· computations

Credit: Mitesh Khapra

H

W1 ×1 × ð· D

1 x 1 CONV

D

Dimensionality Reduction

• Using 1 x 1 convolutions reduces the number of computations

• It aggregates along the depth

H

W

• Convolving a W x H x D input with D1 1 x 1filters will result in a W x H x D1 output

(ð=1,ð=0)

• If D1 \< D, this effectively reduces the dimension of the input, and hence the number of computations

• This results in (ð¹ × ð¹ × ð·&) computations per ð(ð, ð)

• We can then apply subsequent 3 x 3 or 5 x 5 CONVs to this reduced output D1

Credit: Mitesh Khapra

H

W 1 x 1

CONV

• We the can 3x3 and use 5x5 D1 and filters, D2 respectively 1x1 filters before 1 x 1

3 x 3 CONV

CONV

• We can then add the MAX-POOL layer followed by the 1x1 dimensionality Filter

reduction

1 x 1

5 x 5

concatenation • Have a separate 1x1 CONV CONV

CONV

• Concatenate these together at the end

MAX-

1 x 1 POOL

CONV

This is called the Inception Module

D

Inception Module

• We may wish to implement different dimensionality reduction techniques prior to the applying 3x3 or 5x5 CONVs

Credit: Mitesh Khapra

GoogLeNet or InceptionNet (2014)

• Inceptionv1:

• 22 layers in total (9 Inception Modules)

• 5M parameters (compared to 60 M in AlexNet)

• Built parameters

with many small convolutions so as to reduce the number of Convolution

Pooling Softmax Concat/Normalisation

Identity bias and optimisation geometry

Why deeper networks fail without help

3 x 3 CONV, 256

3 x 3 CONV, 256

3 x 3 CONV, 256

• Suppose train network

a good we have shallow been neural able to 3 x 3 CONV, 64 3 x 3 CONV, 64

3 x 3 CONV, 64

3 x 3 CONV, 256

• Then, an more even layers suppose deeper (---)

we network are able with to train 3 x 3 CONV, 64 3 x 3 CONV, 64

3 x 3 CONV, 64

pool, /2

3 x 3 CONV, 128 , /2

3 x 3 CONV, 256

Intuition

3 x 3 CONV, 128

3 x 3 CONV, 256

If the shallow network performs well, then the deep

3 x 3 CONV, 128

3 x 3 CONV, 256

network should also work well by simply learning to

3 x 3 CONV, 128

3 x 3 CONV, 256

compute the identity functions in the new layers

3 x 3 CONV, 128

The solution space of the shallow network is a subset

3 x 3 CONV, 128

of the solution space of the deeper network

3 x 3 CONV, 128

3 x 3 CONV, 128

Credit: Mitesh Khapra

Deeper networks yield high errors

• Deep vanilla CNNs have high training and test error

• Shattered gradients

Prince, S. Understanding Deep Learning (Ch. 11)

Needle-in-haystack

Can we bias the architecture so that preserving representations is the default behaviour?

Loss landscape intuition

Residual connections as a structural fix

• Residual networks change the computation graph

Vanilla CNN

Residual network

• Each block computes an additive update

ℎ 012 = ℎ 0 + ð 0 ℎ 0

Residual connections as a structural fix

Example:

“Unravelling” the network reveals that the output is a sum of the input plus 4 smaller networks

Residual connections as an inductive bias

ð¥

ð¥

• Consider two layers stacked in a CNN

• They are each learning some Layer 1

Layer 1

function of the input ððð¿ð

ððð¿ð

Layer 2

ððð¿ð

Layer 2

ð(ð¥) ððð¿ð• But, what if we enable them to learn only a residual ℎ(ð¥)

\+

Identity function of the input?

ℎð¥ =ðð¥ +ð¥

Why residual learning helps

ð¥

Layer 1

ð¥

Layer 1

• Why does this help?

• A network learned transformations deeper the would version identity perform in of the just shallow fine if it the new layers

ððð¿ð

Layer 2

ððð¿ð

ððð¿ð

Layer 2

ððð¿ð• The connection) a input ResNet identity to connection retain from the a copy input (or of allows skip the ℎ(ð¥)

Skip connection ℎð¥ =ðð¥ +ð¥ +

• This very idea deep made networks it possible to train ResNet encodes the belief that normal anatomy should pass through the network largely unchanged. Only deviations from the norm need to be modelled explicitly.

Why residuals help gradients

• In a plain network, the gradient w.r.t. early layers is a long product of Jacobians

• In a ResNet, the gradient contains an identity term:

Gradients never depend only on long unstable paths Short, well-behaved paths always contribute

Very deep ResNets

• 152-layer “ultra-deep” network

• Won almost every challenge

• Surpassed human-level performance

Very deep ResNets

• 152-layer “ultra-deep” network

• Won almost every challenge

• Surpassed human-level performance

• Bag of tricks:

• Batch normalization after every CONV layer

• SGD + Momentum (0.9)

• Learning rate: 0.1, divided by 10 when the validation error plateaus

• Mini-batch size: 256

DenseNet: Feature reuse as a prior

Huang, Gao, et al. "Densely connected convolutional networks." CVPR. 2017 (https://arxiv.org/abs/1608.06993)

Collective knowledge across layers

• In DenseNet, each layer obtains additional inputs from all preceding layers

• Allows generation of thinner networks

• Channels per unit (ð) is much lower than for ResNet

• Utilises bottlenecks

• 1x1 then 3x3 convolutional residual units

• Preceded by BatchNorm and ReLU (as ResNet 2016)

ResNet

DenseNet

softmax classifier

Huang, Gao, et al. "Densely connected convolutional networks." CVPR. 2017 (https://arxiv.org/abs/1608.06993)

global average pooling

Why this works

• Dense units are interspersed with 1×1 CONV followed by 2×2 average pooling

• Finishes with global average pooling and softmax classifier

• Outperforms ResNet

CNN architectures for semantic segmentation

Segmentation tasks

Classification

Semantic Segmentation Instance Segmentation

Output:

Output:

Output: One label per image

One (category) label per pixel

Category and instance labels for each pixel (Grouping together similar pixels)

(Distinguishes between different instances of an object)

Image credit: Chen et al. 2016. https://arxiv.org/pdf/1604.02677.pdf

Semantic Segmentation

• Goal: implement a pixel-level classifier

• High-resolution prediction

• Preserve the image dimensions at the output

• Requires an encode-decoder network

Where

Image credit What (bottleneck)

Fully Convolutional Network (FCN)

• FCN’s replaced fully connected layers with CONV layers

• Converted FC layers into 1x1 CONV layers

• To obtain classification for each pixel, another 1x1 CONV layer is appended with channel dimension ð¶+1 (where ð¶ is the number of classes)

• Classification architectures perform downsampling as they go deeper.

Upsampling Strategies

One approach:

1 Nearest Neighbour

• Upsampling followed by convolution

1 1 2 2

1 2

1 1 2 2

3 4

3 3 4 4

Input: 2 x 2

3 3 4 4

Output: 4 x 4

Take an input pixel value and copy it to the ð- nearest neighbours, where ð depends on the expected output dimensions.

Source

Upsampling Strategies

2 “Bed of nails”

3 Bilinear interpolation

1 0 2 0

10 12 17 20

1 2

0 0 0 0

10 20

2x

15 17 22 25

3 4

3 0 4 0

30 40

25 27 32 35

Input: 2 x 2

0 0 0 0

Input: 2 x 2 30 32 37 40 (low-res activation)

Output: 4 x 4

Output: 4 x 4

Copy the value of the input pixel at the

Take the 4 nearest pixels, perform weighted corresponding position in the output image,

averaging based on the distance of the four and fill the remaining positions with zeros.

nearest cell. This smooths the output.

Source

Source

4 (Max-)Unpooling

Upsampling Strategies

Upsampling Strategies

5 Transpose convolutions (or ‘deconvolutions’)

Also known as:

• Fractionally strided convolution

• Backward strided convolution Take each element (pixel) of the input feature map Multiply it with every element of the kernel Project it into the corresponding 2 x 2 section of the output grid

0 1

0 1

0 1

0 1

2 3

2 3

1

2 3

2 3 0

2

3

0 0 1 0 0

0 1

0 0

2 30 2

4 6

0 3 6 90 4 6

4 12 9

Note that the kernel weights are learnable. Doing this for each input pixel creates overlapping blocks in the resulting map Add these together to get the upsampled result.

Target Output: 3 x 3 (upsampled grid)

Source

Upsampling Strategies

Problems with Transpose convolutions

Can lead to checkerboard artifacts

Source

UNet

Input Output

• Symmetric encoder-decoder architecture

• Paired layers with matching spatial and channel dimensions

• Designed (i.e. mitochondria for semantic segmentation) segmentation in biomedical imaging task • Encoder network localises

Image tiling at the input

Only a few CONV filters in early layers

Max-pooling increasingly aggregating more contextual information

Upsampling of deepest layers take global information back to individual pixel-level predictions

Bottleneck is the lowest- resolution, global representation

Skip connections concatenate feature maps from the encoder to those in the decoder Combine high-level information with low-level (local) information. This provides sharper segmentation boundaries

Concatenate same-resolution feature maps (crop + concat)

Skip connections concatenate feature maps

Train with classification loss (e.g. from the encoder to those in the decoder

binary cross-entropy) on every pixel Combine high-level information with low-level (local) information. This provides sharper segmentation boundaries

Sum over all pixels to get total loss

Concatenate same-resolution feature maps (crop + concat)

Output is an image Width x Height x (1+ \# Classes)

Note: Output image is smaller than the input image due to convolutions without padding

Why U-Net works well in medicine

• Originally applied to cell segmentation

• Small dataset

• Overfitting discouraged through

• Data augmentation (through elastic deformations)

• Image tiling

• Only ReLU and POOL

• Now more common to see:

• BatchNorm

• Dropout (in bottleneck)

• Strided downsampling (if enough data)

• Residual connections for each convolutional block (Res-UNet)

Credit: Emma Robinson

Overlap-tile strategy for seamless segmentation of arbitrary large images

Attention U-Net

• Proposes novel attention gate (AG) network to learn soft mask with attention coefficients ð¼

• ð¼ is high for salient image regions

• Used to prune incorrect predictions from noisy regions • Implemented with additive attention:

• Linear transforms implemented from 1x1 convolutions

• Output of AGs is element-wise multiplication of input feature- maps and attention coefficients

Attention Gate (AG)

Credit: Emma Robinson

Spatial Transformer Networks: Learned invariance

Input image

Spatial Transformer Networks

• Inductive biases in CNNs: • Translation equivariance through convolution operation • (Limited) scale invariance through pooling operation • Not fully rotationally invariant…

Output: region of interest (sampled from the input)

Input imageA small localization network

predicts the transform, ð

Spatial Transformer Networks

• CNNs are not rotation-invariant

Output: region of interest (sampled from the input)

Spatial Transformer Networks

• CNNs are not rotation-invariant

Grid generator: uses ð to compute the sampling grid

ð¦ð¥--.. = ð// ð0/ ð/0 ð/1 ð00 ð01

ð¥-2ð¦-21

Spatial Transformer Networks

• CNNs are not rotation-invariant

Sampler uses bilinear interpolation to produce the output

Vigneault et al, Ω-Net (Omega-Net): Fully automatic, multi-view cardiac MR detection, orientation, and segmentation with deep neural networks, MedIA, 2018

Spatial Transformer Networks

Architectures as inductive bias

Architecture What it assumes about the world

CNNs Appearance matters, position does not

Inception / GoogLeNet Relevant scale is uncertain

ResNet Representations should be preserved

U-Net Spatial detail must not be discarded

STN Invariances should be learned, not fixed

References + Slide Credits

• http://cs231n.stanford.edu/slides/

• http://introtodeeplearning.com/

• http://ufldl.stanford.edu/tutorial/

• http://playground.tensorflow.org/

• http://vision.stanford.edu/teaching/cs231n-demos/linear-classify/

• Vigneault, D. M., Xie, W., Ho, C.Y., Bluemke, D.A., Noble, J.A., Ω-Net (Omega-Net): Fully automatic, multi-view cardiac MR detection, orientation, and segmentation with deep neural networks, Medical Image Analysis, 48, pp. 95-106, 2018

• Ronneberger, O., Fischer, P., Brox, T., U-Net: Convolutional Networks for Biomedical Image Segmentation, MICCAI, 9351, pp. 234-241, 2015

• Gurovich, Y., Hanani, Y., Bar, O., Nadav, G., et al. Identifying facial phenotypes of genetic disorders using deep learning. Nature Medicine Letters, 25, pp. 60-64, 2019

• Krizhevsky, A., Sutskever, I., Hinton, G.E., ImageNet Classification with Deep Convolutional Neural Networks, NIPS, 2012

• Rajpurkar, P., Irvin, J., Zhu, K., Yang, B., Mehta, H., et al. CheXNet: Radiologist-Level Pneumonia Detection on Chest X-Rays with Deep Learning. https://arxiv.org/abs/1711.05225, 2017

<https://arxiv.org/abs/1608.06993>   
<https://arxiv.org/abs/1608.06993>   
<http://cvlab.postech.ac.kr/research/deconvnet/>   
<https://towardsdatascience.com/transposed-convolution-demystified-84ca81b4baba>   
<https://towardsdatascience.com/transposed-convolution-demystified-84ca81b4baba>   
<https://towardsdatascience.com/transposed-convolution-demystified-84ca81b4baba>   
<https://towardsdatascience.com/transposed-convolution-demystified-84ca81b4baba>   
<https://towardsdatascience.com/transposed-convolution-demystified-84ca81b4baba>   
<http://cs231n.stanford.edu/slides/>   
<http://cs231n.stanford.edu/slides/>   
<http://introtodeeplearning.com/>   
<http://introtodeeplearning.com/>   
<http://ufldl.stanford.edu/tutorial/>   
<http://ufldl.stanford.edu/tutorial/>   
<http://playground.tensorflow.org/>   
<http://playground.tensorflow.org/>   
<http://vision.stanford.edu/teaching/cs231n-demos/linear-classify/>   
<http://vision.stanford.edu/teaching/cs231n-demos/linear-classify/>   
<htt
