# Computer Vision — Segmentation
> Source: Google Drive file 19eL--6Grni542C_W0semx5TAueBSj5Yj · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Segmentation

Computer Vision – Lecture 11

1

Further Reading

• Slides from S Lazebnik

• Slides from J Johnson

• Slides from A Geiger

2

Granularity

Image classification

Image-scale

Object detection

Localization

Spatial (Regions)

Labelling

Pixel-level Segmentation

3

“cat”

Semantic Segmentation

• Label each pixel in the image with a category label

• Do not differentiate instances, only care about pixels

4

Slide: J Johnson

Evaluation

• Per-class IoU.

• Since there are no instances, evaluation is much easier than detection.

• Compare the binary masks of prediction and GT for each class.

• Average over classes.

• Note: IoU is favourable to large objects. (harder to intersect small objects)

5

Sliding Window

Similar to detection:

• Slide a window over the whole image.

• Classify the centre pixel of the window.

Classifier dog

Classifier tree

Classifier snow

Classifier sky

Farabet et al, “Learning Hierarchical Features for Scene Labeling,” TPAMI 2013

6 Pinheiro and Collobert, “Recurrent Convolutional Neural Networks for Scene Labeling”, ICML 2014

Sliding Window Segmentation

• Very inefficient\!

• Very noisy: independent decision for each patch.

• Observation: we are recomputing the same features for overlapping patches.

• How can we share computation?

• Convolutions\!

7

Fully Convolutional Networks

If we do not down-sample (and always pad appropriately) we can design a network with convolutions that has the same input and output size.

8

Source: Stanford CS231n

Fully Convolutional Networks

If we do not down-sample (and always pad appropriately) we can design a network with convolutions that has the same input and output size.

9

Source: Stanford CS231n

FCN: Fully Convolutional Networks

If we do not down-sample (and always pad appropriately) we can design a network with convolutions that has the same input and output size. Very costly at full resolution. Down-sample, then up-sample\!

10 J. Long, E. Shelhamer, and T. Darrell, Fully Convolutional Networks for Semantic Segmentation, CVPR 2015

Source: Stanford CS231n

Upsampling: Unpooling

• “Inverse” max/avg-pooling operation.

• Pooling is not an invertible function: information is lost and cannot be recovered.

• Several options to approximate it.

11

Unpooling: Nearest Neighbour

1 1 2 2

1 2

1 1 2 2

3 4

3 3 4 4

3 3 4 4

Input

Output C x H x W

C x 2H x 2W

12

Unpooling: Bed of Nails

1 0 2 0

1 2

0 0 0 0

3 4

3 0 4 0

0 0 0 0

Input

Output C x H x W

C x 2H x 2W

13

Unpooling: Bilinear Interpolation

1 1.25 1.75 2

1 2

1.50 1.75 2.25 2.50

3 4

2.50 2.75 3.25 3.50

3 3.25 3.75 5

Input

Output C x H x W

C x 2H x 2W

14

Max-Unpooling

While down-sampling:

While up-sampling: use remember locations

remembered locations

1 2 6 3

3 5 2 1

5 6

Other

1 2

layers 4 5 6 2

7 8

3 4

7 1 4 8

15 Noh et al, “Learning Deconvolution Network for Semantic Segmentation”, ICCV 2015 Slide: J Johnson

0 0 2 0

0 1 0 0

0 0 0 0

3 0 0 4

Convolution with Stride

3x3 Convolution with stride 2

16

Transposed Convolution

3x3 convolution transpose, stride 2

• 9 weights

• Scale by input value

• Sum in overlapping regions

17

Transposed Convolution

ð1ð¤1 ð1ð¤2 ðð12ð¤ð¤3 1

\+

ð1ð¤4 ð1ð¤5 ðð12ð¤ð¤4

6 +

ð1 ð2 ðð13ð3 ð4

ð¤ð¤7 1

\+

ðððð1234ð¤ð¤ð¤ð¤9 1

7 3 + ðð13ð¤ð¤8 2

\+

\+ +

18

Transposed Convolution

• Learnable upsampling.

• Outputs are the sum of 1-4 values: often grid pattern in output. Add normal convolution to learn smoothing.

Other names (can be confusing)

• Deconvolution

• Upconvolution

• Fractionally strided convolution

• Backward strided convolution

19

U-Net

• Skip-connections.

• Concatenate higher-level with feature higher-res, maps. feature upsampled lower-level maps • Low-level details. feature maps: • High-level semantics.

feature maps: 20 O. Ronneberger, P. Fischer, T. Brox, U-Net: Convolutional Networks for Biomedical Image Segmentation, MICCAI 2015

Dense Prediction Architectures

Figure source 21

Transformer Architectures

Cheng, Schwing, Kirillov, “MaskFormer: Per-Pixel Classification is Not All You Need for Semantic Segmentation”, NeurIPS 2021

22

Interactive Segmentation

• User specifies what to segment.

• Input:

• Seed points

• Scribbles

• Bounding box

• Text

• …

• Model segments corresponding object(s).

23

Image source

SAM: Segment Anything Model

Kirilliov et al., 2023

• Trained a model on various input modalities.

• Large scale supervision

• 1B masks

• 11M images

24

Training with Humans in the Loop

1\. Annotate data. 2. Train model. 3. Label more data with the model. 4. Humans fix, improve labels. 5. Goto 2.

25

Large-Scale Annotations

26

Image source

Interactive Segmentation

• User centric.

• SAM: no class labels, just binary segmentation.

Other types:

• Foreground/background segmentation

• Referring expressions segmentation (“The man with the blue hat”)

• Saliency segmentation (what stands out in the image)

27

Things and Stuff

Thing: An object with a specific size and shape. Stuff: Material defined by a homogeneous or repetitive pattern of fine-scale properties, but has no specific or distinctive spatial extent or shape

• Object detection: things (instances)

• Semantic segmentation: things and stuff (but no instances)

28

Things:

• Dog

• Tree

• Lantern

• …

Stuff:

• Sky

• Snow

• …

Instance Segmentation

• Semantic segmentation does not separate objects of the same class.

• Object detection finds individual objects (instances).

• Instance segmentation: segmentation at instance-level.

29

Semantic segmentationInstance segmentation

Instance Segmentation

• Detect all objects in the image, and identify the pixels that belong to each object (only things, not stuff)

• Intuitive approach:

• Detect objects

• predict a segmentation mask for each object

• Practice: add another branch to your detector that predicts a mask for each box.

30

K. He, G. Gkioxari, P. Dollar, and R. Girshick, Mask R-CNN, ICCV 2017 (Best Paper Award)

Mask R-CNN

Faster R-CNN + FCN on RoIs

Classification+ regression branch

Mask branch: separately predict segmentation for each possible class

31

RoIPool

Nearest neighbor quantization results in small errors

Slide: R Girshick

RoIAlign vs. RoIPool

RoIPool: nearest neighbor quantization RoIAlign: bilinear interpolation

Mask R-CNN

From RoIAlign features, predict class label, bounding box, and segmentation mask

Classification head

Regression head

Separately predict binary mask (28x28) for each class with per- pixel sigmoids, use average binary cross-entropy loss (80 classes)

Mask R-CNN Prediction

28x28 soft prediction

Resized soft prediction Final mask

35 Slide: R Girshick

Mask R-CNN Prediction

28x28 soft prediction

Resized Soft prediction

Final mask

36 Slide: R Girshick

37 Slide: R Girshick

38 Slide: R Girshick

Panoptic Segmentation

• Combine semantic segmentation for stuff,

• with instance segmentation for things.

• Can be solved separately.

• More efficient: share some computation between tasks.

39

Image source

Keypoints

Instead of predicting masks, we can predict other things such as keypoints.

Keypoints here: object-specific landmarks, e.g. joints.

40

x17

keypoints

Human Pose

17 keypoint “mask” predictions shown as heatmaps

41

Keypoint Classification Loss

• Turn the GT location into a class.

• As many classes as pixels in the heatmap.

• Train with softmax cross-entropy loss.

• Output resolution limited to heatmap resolution (28x28 for Mask R-CNN)

42

Differentiable Keypoint Regression

• We can use softmax to formulate the keypoint regression task as a heatmap prediction problem.

• Compute softmax over heatmap: ð» = softmax(ℎ)

ðð¥,ðð¦

ð = ෍ð¢ð£ ð»(ð¢,ð£)

ð¢,ð£

• Output location is the weighted sum of pixel locations.

• Use temperature to make it sharper.

43

Combining Tasks

Heads can be combined to solve multiple tasks simultaneously with minimal overhead.

44

Dense Captioning

Add a text-output head: predict captions.

46 Johnson, Karpathy, and Fei-Fei, “DenseCap: Fully Convolutional Localization Networks for Dense Captioning”, CVPR 2016

3D Shape

Add a mesh prediction head.

Gkioxari, Malik, and Johnson, “Mesh R-CNN”, ICCV 2019

47

<https://slazebni.cs.illinois.edu/spring23/>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/WI2022/598_WI2022_lecture15.pdf>   
<https://uni-tuebingen.de/fakultaeten/mathematisch-naturwissenschaftliche-fakultaet/fachbereiche/informatik/lehrstuehle/autonomous-vision/lectures/computer-vision/>   
<http://cs231n.stanford.edu/slides/2018/cs231n_2018_lecture11.pdf>   
<http://cs231n.stanford.edu/slides/2018/cs231n_2018_lecture11.pdf>   
<http://cs231n.stanford.edu/slides/2018/cs231n_2018_lecture11.pdf>   
<http://arxiv.org/pdf/1411.4038.pdf>   
<https://arxiv.org/pdf/1505.04597.pdf>   
<https://phillipi.github.io/pix2pix/>   
<https://arxiv.org/pdf/2304.02643.pdf>   
<https://arxiv.org/pdf/2
