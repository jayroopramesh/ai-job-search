# Computer Vision — Introduction
> Source: Google Drive file 1IViZZ13KLs4oZNa3RuBeppf_RMR0a5Mc · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Computer Vision

Lecture 01 - Introduction

1

“a professor teaching a class in computer vision” – StableDiffusion Jan’24

Computer Vision

Lecture 01 - Introduction

2

“a professor teaching a class in computer vision” – FluxAI “Schnell” Jan’25

Computer Vision

Lecture 01 - Introduction

3

“a professor teaching a class in computer vision” – FluxAI “Schnell” Jan’25

Course Structure

• 20 lectures

• pptx on moodle the day before the lecture.

• 4 classes

• 3+1 practicals

• Sit-down (closed book) exam

4

Classes and Practicals

• 4 classes in 4 groups – please distribute\!

• Mostly maths and conceptual questions

• Will be similar to the exam questions

• 4 practicals with 3 sheets

• Mostly code

5

Practicals

1\. Image filtering and transformations 2. Image Classification & Interpretability 3. Object Detection & Diffusion 4. Coordinate Networks and Representation Learning (optional)

Signing off will normally happen in the last half hour of each session or at the beginning of the following one.

As usual, when checking your work, the demonstrator will want to see a working version of the program in action, as well as appropriate commenting of your code and sketches indicating the design steps. Try to make your report as concise as possible, perhaps in the form of appropriate comments to your code.

6

Books

• Multiple View Geometry in Computer Vision Richard Hartley and Andrew Zisserman, Cambridge University Press, link

• Deep Learning Ian Goodfellow, Yoshua Bengio and Aaron Courville. MIT Press 2016, link

• Pattern Recognition and Machine Learning Christopher M Bishop, Springer 2007, link

7

Python

• python 3 (typical packages: opencv-python, numpy, sci-py, matplotlib, pytorch, …)

• Everything runs inside Google Colab notebooks https://colab.research.google.com

• Alternative: you can run things locally on your laptop

• You will need to manage your environment yourself (use conda)

• Demonstrators will not have time to help you with setup problems

• Most lectures come with a Colab notebook containing code for the examples in the slides.

8

This Lecture Today

• Should give you a general understanding of what kind of problems we think about in CV.

• Will introduce some historical context and how things evolved to where we are.

• Might motivate why we will look at fundamentals before we dive into the flashy topics later in the course.

9

Computer Vision Now

10

Rapid progress

• arXiv/cs 200 submissions/day (2021)

• Keeping up is difficult

• Benchmarks evaluate progress for individual tasks

• Ideas translate between sub-fields

11

Progress in Computer Vision

• Currently: 4 main drivers of improvement:

• Data

• ML improvements (optimisers, architectures, etc.)

• Engineering/tuning (often task specific)

• Good ideas (rare compared to other factors)

• Papers often contain a mixture

• This course: (mostly) good ideas -\> easier to judge for older approaches

12

Where is Computer Vision now?

13 Slide credits: John Barron – Scholars and Big Models Workshop, CVPR 2023

Where is Computer Vision now?

14 Slide credits: John Barron – Scholars and Big Models Workshop, CVPR 2023

Rocket speed - 1953

• USAF prediction for rocket speed

• Time vs. fraction of light speed

• Vastly overestimates progress

• Nuclear rockets

• Interstellar travel

Slide credits: John Barron – Scholars and Big Models Workshop, CVPR 2023

15

Computer Graphics

Slide credits: John Barron – Scholars and Big Models Workshop, CVPR 2023

16

Computer Vision

Time

17

Progress

Are we here?

Are we here?

Computer Vision

• It is very difficult to predict where we are

• Towards the end of this curve progress transitions from academia to industry

• So far, we thought we are at the end many times and were wrong (AI, self-driving, CNNs, etc.)

• It might not be a sigmoid after all\!

18

(Recent) CV History Overview

• 1960-1970: Blocks, Edges and Model Fitting

• 1970-1981: Low-level vision: stereo, flow, shape-from-x

• 1985-1988: Neural Networks, backprop., self-driving

• 1990-2000: Dense stereo and multi-view stereo, MRFs

• 2000-2010: Features, descriptors, structure-from-motion

• 2010-20??: Learning, deep learning, large datasets, rapid growth

19 History slides credits: Andreas Geiger - History of Computer Vision 2021 & Svetlana Lazebnik – Computer Vision: Looking Back to Look Forward

Historical Context

20

1957: Stereo(photogrammetry)

• Gilbert Hobrough: analog implementation of stereo image correlation

• Used to create elevation maps (Photogrammetry, since 1840)

Louis, Hobrough Gilbert. "Methods and apparatus for correlating corresponding points in two images." U.S. Patent No. 2,964,642. 13 Dec. 1960

21

Wild B8 (721x produced 1961 -1972)

1958-1962: Rosenblatt’s Perceptron

• First algorithm and implementation for training single linear “threshold neuron”

• Perceptron ð¿ ð¤ = −σð∈ðcriterion: ð¤ðð¥ðð¦ð

• Convergence proof: Novikoff

Rosenblatt, Frank. "The perceptron: a probabilistic model for information storage and organization in the brain." Psychological review 65.6 (1958): 386.

22

1963: Larry Roberts – Blocks World

• Scene Understanding for Robotics

• Extracts edges

• Infers structure 3D structure of edges from topological • “It projection dimensional assumptions obtain dimensional information of process.” a is topological, assumed a reasonable, of… in description enable models… that a known mathematical photograph a a photograph three- computer three- These from by the means to is edge a Roberts, Lawrence G. Machine perception of three-dimensional solids. Diss. Massachusetts Institute of Technology, 1963.

23

Differentiable Blocks World: Qualitative 3D Decomposition by Rendering Primitives Tom Monnier, Jake Austin, Angjoo Kanazawa, Alexei A. Efros, Mathieu Aubry, NeurIPS 2023

Blocks World now

24

1966: MIT Summer Vision Project

• Solve computer vision as a summer project

• Committed to block world ideas

25

1969: Perceptrons book

• Minsky and Papert

• Several discouraging results

• Perceptrons cannot solve the XOR problem

• Largely contributed to the following “AI winter”

• 70s: mostly symbolic AI

26

1970: MIT Copy Demo

• Vision + Robotics

• Recover the structure of a scene

• Plan robot movement to copy the block arrangement

• Only works in ideal conditions

• Causes attention to robustness for low level vision tasks

Patrick Winston and the MIT AI Lab Copy Demo https://people.csail.mit.edu/bkph/phw\_copy\_demo.shtml

27

1980s: Advances in ML

• Neocognitron: Fukushima (1980)

• Back-propagation: Rumelhart, Hinton & Williams (1986)

• Origins in control theory and optimization: Kelley (1960), Dreyfus (1962), Bryson & Ho (1969), Linnainmaa (1970)

• Application to neural networks: Werbos (1974)

• Parallel Distributed Processing: Rumelhart et al. (1987)

• Neural networks for digit recognition: LeCun et al. (1989)

28

Fukushima (1980)

1990s Theme: Geometry

• Fundamental matrix: Faugeras (1992)

• Normalized 8-point algorithm: Hartley (1997)

• RANSAC for robust fundamental matrix estimation: Torr & Murray (1997)

• Bundle adjustment: Triggs et al. (1999)

• Hartley & Zisserman book (2000)

• Projective structure from motion: Faugeras and Luong (2001)

29

Tracking and Optical Flow

30

Visual Tracking

Visual tracking involves the identification of some characteristic of the scene in successive images.

2D tracking follow and perhaps control the image position of some entity as it moves from frame to frame over time.

3D (or pose) tracking use image measurements (possibly involving 2D tracking) to update the 6 degrees of freedom (3 translation + 3 rotation) which define 3D pose.

31

2D Visual Tracking

Both, 2D and 3D tracking require a model of appearance, sufficient to identify high cross-correlation between frames.

In 2D tracking, the appearance model might relate to

• a single point

• a small patch, possibly deformable

• a contour, possibly deformable

• a line element

• ...?

Let's start simply by tracking an image point ...

32

Point Tracking

• Using a bright spot detector

Not robust: we need to incorporate

• Stronger appearance/ measurement models;

• Image and/or scene dynamics

Points -\> patches

Sharkey, P., McLauchlan, P. F., Reid, I. D. and Murray, D. W. Real-time Control of a Reactive Stereo Head/Eye Platform. International Conference on Automation, Robotics and Computer Vision, 1992 33

w

h

Template ð

Image I

• Tracking by Detection (each frame processed individually)

• Very slow: (\#pixels\_image \* \#pixels\_template) comparisons

34

Template Tracking

Sum of squared differences between image I and template ð at every location (ð¢,ð£)

ð¸ ð¢,ð£ = ෍

ð¥,ð¦ ∈ −ð¤2,ð¤2 × −ℎ2,ℎ2

ð¼ ð¢ + ð¥,ð£ + ð¦ − ð ð¥,ð¦ 2

Energy E

1981: Lucas-Kanade Template Tracking

ð¸ ð¢,ð£ = ෍ð¼ ð¢ + ð¥,ð£ + ð¦ − ð ð¥,ð¦ 2

ð¥,ð¦

Improving the efficiency:

• Formulate search as an optimisation problem using brightness constancy as our objective function

• ð¸ is a non-convex function over the image ð¼

• Suppose frame

the starting point is ð¡ð¥,ð¡ð¦

ð e.g., detection in prev.

• LK searches for an update ð¿ð¥,ð¿ð¦

35 ð of the starting point

Generalised LK Tracking

• Simple update rule that iteratively refines the tracked position

• Any differentiable warp works

• Further optimization: pre-compute template gradients and warp “the other way”

• In-depth LK analysis:

Lucas-Kanade 20 Years On: A Unifying Framework Simon Baker and Iain Matthews

36

LK Tracker Insights

• A general difficulty with trackers relying too heavily on the spatial relationships between pixels is that they are prone to break due to partial occlusion and orientation changes in the scene.

• Appearance changes can be compensated by updating the template from frame to frame

• Can lead to “drift”:

• The template will gradually pick up the background and eventually “stick”.

• Can be avoided when background is simple, or

• With a segmentation mask

37

2010: Tracking by Detection

• Pure tracking can fail (occlusions, drift, blurry frames, etc…)

• Idea: integrate a detector into the tracking pipeline

• Tracking-Learning-Detection (TLD) Framework (Kalal et al, 2010)

• the target object is defined by a bounding box in a single frame.

• a template/patch-based tracker follows the object frame to frame.

• a random forest-based detector localizes the object and corrects the

• tracker if needed.

• learning is used to improve the detector.

38

Tracking by Detection

Kalal, Z., Mikolajczyk, K. and Matas, J., 2011. Tracking-learning-detection. IEEE transactions on pattern analysis and machine intelligence 39

Tracking by Detection

Benfold, B. and Reid, I., 2011, June. Stable multi-target tracking in real-time surveillance video. In CVPR 2011 40

2016: CNN Tracking

• Instead of comparing pixel intensities: compare features

• Learn features by comparing the score map to ground- truth detections from the same video

• Very simple and fast

Bertinetto, Luca, Jack Valmadre, Joao F. Henriques, Andrea Vedaldi, and Philip HS Torr. "Fully-convolutional siamese networks for object tracking." ECCV 2016 41

2016: CNN Tracking

• Instead of comparing pixel intensities: compare features

• Learn features by comparing the score map to ground- truth detections from the same video

• Very simple and fast

Bertinetto, Luca, Jack Valmadre, Joao F. Henriques, Andrea Vedaldi, and Philip HS Torr. "Fully-convolutional siamese networks for object tracking." ECCV 2016 42

Point Tracking Revival

43 Harley, Adam W., Zhaoyuan Fang, and Katerina Fragkiadaki. "Particle video revisited: Tracking through occlusions using point trajectories." ECCV, 2022.

Optical Flow

• How does every pixel move from one frame to another?

• “Tracking every pixel”

• Correspondence problem

• Some pixels can go missing (occlusion, image border, etc…)

• Some pixels can appear or change colour (e.g. traffic light)

• Ground-truth difficult to obtain

44

1981: Optical Flow

• Pattern of apparent motion: densely tracking pixels between frames

• Horn-Schunck algorithm

• 2D correspondence search: more difficult than stereo

45

Optical Flow – The Beginnings

Raw estimate Smoothed estimate

46

Optical Flow – The Beginnings

• Intensity based optical flow

• Problems with uniform-coloured regions

• Difficult to regularise

• Can be combined with LK tracking

• Smoothness constraints

• Difficult evaluation on very few scenes

• Synthetic with ground truth

• Qualitative on real scenes

47

Optical Flow – Flying Things

• Easier to create – automatic pipeline

• Generalises well to real data

\-\> optical flow is a low level vision problem and thus sim2real transfer works well

Mayer, Nikolaus, Eddy Ilg, Philip Hausser, Philipp Fischer, Daniel Cremers, Alexey Dosovitskiy, and Thomas Brox. "A large dataset to train convolutional networks for disparity, optical flow, and scene flow estimation.“, CVPR 2016 48

Optical Flow - Sintel

Butler, Daniel J., Jonas Wulff, Garrett B. Stanley, and Michael J. Black. "A naturalistic open source movie for optical flow evaluation.“ ECCV 2012 49

Optical Flow –Learned: FlowNet

• Again Siamese architecture

• Compute correlation volume inside network

• Trained on FlyingThings3D

50

Optical Flow –Learned: FlowNet

A. Dosovitskiy, P. Fischer, E. Ilg, P. Haeusser, C. Hazirbas, V. Golkov, P. van der Smagt, D. Cremers and T. Brox “FlowNet: Learning Optical Flow ith Convolutional Networks), ICCV 2015 51

Optical Flow –Now(ish): RAFT

Improvements (by RAFT and other papers):

• Better backbone architectures

• Multi-scale correlation volume

• Iterative refinements: predict and update the flow estimate through several iterations

Teed, Zachary, and Jia Deng. "Raft: Recurrent all-pairs field transforms for optical flow.“, ECCV 2020

52

Motion Estimation

Point Tracking Long-term tracking of individual points

PIPs

TAP-Net

Optical Flow Dense correspondences between a pair of frames

RAFT

Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022 TAP-Vid: A Benchmark for Tracking Any Point in a Video. Doersch et al., NeurIPS D\&B 2022

RAFT: Recurrent All-Pairs Field Transforms for Optical Flow. Teed et 53

al. , ECCV 2020

Shape-from-X

54

1970: Shape from Shading

• Recover 3D from a single 2D image

• Assume simple lighting and material (Lambertian with constant albedo)

• Strong smoothness assumptions

Shape-from-X • Shading: Horn (1970) • Contour: Guzman (1971), Waltz (1975), etc. • Texture: Bajczy & Lieberman (1976) • Stereo: Marr & Poggio (1976)

55

1978: Intrinsic Images

• Decompose images into its intrinsic 2D layers

• Reflectance

• Shading

• Shape

• Motion, etc.

• Useful for downstream tasks: e.g. removing lighting simplifies object detection

56

1978: Intrinsic Images

MIT Intrinsic Images dataset (2009)

57

Wu, Jiaye, et al. "Measured Albedo in the Wild: Filling the Gap in Intrinsics Evaluation." arXiv preprint arXiv:2306.15662 (2023)

1980: Photometric Stereo

• Recover 3D from multiple (\>2) 2D images with varying lighting

• Highly detailed and accurate

• Still Lambertian lighting assumption – relaxed later

58

Shape-from-X now(-ish)

Training Data Output

single-view images of a category

instance-specific 3D shapes 59

Unsup3D

Unsupervised Learning of Probably Symmetric Deformable 3D Objects from Images in the Wild S Wu, C Rupprecht, A Vedaldi CVPR 2020

Stereo

60

1981: Essential Matrix

• 2-view maps points Geometry: to epipolar a matrix lines that • Correspondence becomes a 1D problem search • Essential computed correspondences Matrix from 2D can be • Rediscovery \>100 years old of known ideas H. Christopher Longuet-Higgins (September 1981). "A computer algorithm for reconstructing a scene from two projections". Nature.

61

1992: Structure-from-motion

• Estimating the 3D structure from image collections of static scenes

• Static scenes require only a single (moving) camera

• Closed-form SVD solution: Tomasi-Kanade factorisation for orthographic projection.

• Later: non-linear least squares for projective cameras

Tomasi, Carlo, and Takeo Kanade. "Shape and motion from image streams under orthography: a factorization method." IJCV (1992)

62

1992: Iterative Closest Points

• Register two point clouds by minimizing the distance between closest points Uses:

• Align partial scans

• Estimate relative camera poses from point clouds

• Localization within 3D maps

https://github.com/yassram/iterative-closest-point

Besl, Paul J., and Neil D. McKay. "Method for registration of 3-D shapes." Sensor fusion IV: control paradigms and data structures. Vol. 1611. Spie, 1992.

63

1998: Multi-view stereo

• 3D reconstruction from multiple input images – this time with level-set methods

• Surfaces instead of points

• Modelling visibility

• Convergence proofs

64 Faugeras, Olivier, and Renaud Keriven. "Complete dense stereovision using level set methods." Computer Vision—ECCV'98

2000s: Large-scale SfM

• 2006: Photo Tourism (Snavely et al,, SIGGAPH’06)

• 3D reconstruction from internet images

• Large scale compute

• 2009: Building Rome in a Day (Agarwal et al. ICCV’09)

• Search “rome” on flickr

• Reconstruction: 150k images, 21h, 500CPUs

65

2016: COLMAP

• Open-source C++ framework

• Integrating the best features from prior work

• Defacto standard for SfM

Sparse model of central Rome using 21K photos produced by COLMAP’s SfM pipeline Schonberger, Johannes L., and Jan-Michael Frahm. "Structure-from-motion revisited." CVPR 2016.

66

Structure from Motion (still)

• Individual components have been enhanced with DL

• COLMAP pipeline remains mostly unchanged

67

Neural Radiance Fields

68

1850: Photosculpture

• 24 photographs of an object/person

• Cut contour from wood

• Assemble radial sculpture

69

1986: The Rendering Equation

How much light (of wavelength ð) is leaving a point ð¥ in the direction of ðð at time ð¡?

ð¿ð ð¥,ðð,ð,ð¡ = ð¿ð ð¥,ðð,ð,ð¡ + ð¿ð(ð¥,ðð,ð,ð¡)

emitted radiance

reflected radiance (glowing things)

Immel, David S.; Cohen, Michael F.; Greenberg, Donald P. "A radiosity method for non-diffuse environments”, SIGGRAPH 1986 Kajiya, James T."The rendering equation". Conference on Computer graphics and interactive techniques 1986

70

1986: The Rendering Equation

ð¿ð ð¥,ðð,ð,ð¡ = නΩ incoming radiance at ð¥

from direction ðð

ðð ð¥,ðð,ðð,ð,ð¡ ð¿ð ð¥,ðð,ð,ð¡ ðð ⋅ ð ððð

bidirectional reflectance

surface normal distribution function (BRDF)

71

ð

1965: The BRDF

ðð ðð,ðð = ðð¿ð(ðð)

ð¿ð ðð ðð ⋅ ð ððð

• Positivity: ðð ðð,ðð \> 0

• Reciprocity: ðð ðð,ðð = ðð ðð,ðð

• Energy conservation: ∀ðð,නΩ ðð ðð,ðð ðð ⋅ ð ððð ≤ 1

72 Nicodemus, Fred (1965). "Directional reflectance and emissivity of an opaque surface". Applied Optics

diffuse specular mirror

2000s: Lightfield camera arrays

• Use many synchronized cameras to capture a scene from many angle simlutaneously

• Film use: The Matrix (1999)

73

2020: Neural Radiance Fields

• Input: Image collection

• Learning: mapping coordinates (x,y,z) to color and occupancy

• Output: rendering from novel viewpoints

Mildenhall, Ben, et al. "Nerf: Representing scenes as neural radiance fields for view synthesis.“, ECCV 2020

74

NeRF now(-ish)

• Improvements in generalisation, speed, quality, etc.

• Dynamic scenes remain difficult – triangulation is ambiguousLi, Zhengqi, et al. "Dynibar: Neural dynamic image-based rendering." CVPR. 2023 (Best Paper Honourable Mention) 75

Gaussian Splatting

• Intuition: ray-casting through every pixel is wasteful (mostly empty space)

• Represent the scene as a collection of points with size: 3D Gaussians (mean & covariance)

• Projecting 3D Gaussians to the image plane results in approx. 2D Gaussians (Zwicker et al.,2002)

• Advantage: only spend time/memory on the surface of objects

76 Kerbl, B., Kopanas, G., Leimkühler, T., & Drettakis, G. (2023). 3d gaussian splatting for real-time radiance field rendering. ACM Transactions on Graphics (ToG)

Summary
