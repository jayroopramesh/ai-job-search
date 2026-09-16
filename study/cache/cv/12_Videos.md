# Computer Vision — Videos
> Source: Google Drive file 1fMwFJIk3CjQY-q1Up_mfrYdGR0j-DAYe · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Video

Computer Vision – Lecture 12

1

Further Reading

• Slides from L Fei-Fei

• Slides from J Johnson

• Slides from M Niessner & L Leal-Taixé (2nd part)

2

Videos

• Sequence of frames: T x 3 x H x W

• Frame rate: \~30 FPS (frames per second)

• Temporal coherence

• Sometimes: shot changes/skips

3

Video source

Video Tasks

• Activity Classification

• Temporal/Spatial Action Localisation

• Event Dense Captioning

• Active Speaker Recognition

• Sign Language Transcription

• …

4

Videos

Problem: videos are big\!

• HD (1080x1920):

• 60\*30\*3\*1080\*1920 bytes = 11.2GB / minute

• This is just the data, we still need to compute things.

• Use short, low-res clips: T=16, FPS=5, H=W=112: (60MB/min)

5

Windowed Video Processing

Raw Video: long, high resolution, high FPS

Training: short clips, low resolution, low FPS

Testing: run model on overlapping clips, average predictions

6

Windowed Video Processing

Familiar ideas:

• Subsampling (now in time and space)

• Sliding window (now mostly in time)

• Share as much computation as possible to increase the efficiency

7

Task: Video Classification

• Action recognition: running, knitting, basketball, etc.

• Simple idea: classify frames independently

running

8

CNN CNN CNN CNN CNN CNN

averagerunning

Per-Frame Models

• Predict for each frame independently with an image model.

• Average probabilities (mathematically questionable but works much better than multiplication).

• Often a very strong baseline\!

• Intuition:

• Only one frame is needed to differentiate between “running” and “swimming”.

• This is often called: object-bias of action recognition.

• Depends on task: “sitting down” vs. “standing up” needs motion.

9

Sharing Computation

• Per-frame model cannot reason about time: we only average predictions.

• Add layers that have access across time.

TxDx1x1 MLP

concatenate

each:1xDx1x1

CNN CNN CNN CNN CNN CNN

Tx3xHxW

10

Late Fusion

• Here we decided to include temporal information “late” in the computation.

• Intuition: get per-frame high-level understanding, then combine them across time.

• Fusion mechanisms: concatenation, pooling, etc.

• Problem: low-level motion often lost after “compressing” a frame into a feature vector.

11

Early Fusion

• Fuse frames at the input level: Tx3xHxW -\> T3xHxW

• Treat input as an image with many channels.

Tx3xHxW

12

T3xHxW

CNN

Early Fusion

• First layer takes as input the whole video stacked in the channel dimension.

• Problem: effectively only the first layer has access to temporal information

• First 2D convolution collapses all temporal information: 3TxHxW -\> DxH’xW’

• Remaining network is a standard 2D network.

13

2D Convolution

14

Input C x H x W

N convolutional filters C x h x w

Output N x H x W (with appropriate padding)

3D Convolution

\* =

Input C x D x H x W

15 N Filters C x d x h x w

Output N x D x H x W

Not shown: channel dimension

3D Convolution

• The convolution now slides along 3 directions: width, height, and depth.

• There is still a channel dimension: each feature in the 3D feature map has C dimensions.

• The output is also a 3D feature map.

• Naming: we ignore the channel dimension. Input and output are actually 4D tensors. (weights: 5D)

16

Other operations

• 3D Pooling: works the same way. Filter size e.g. 2x2x2

• Activation: works element-wise. (no change)

• Fully connected layer: same as in 2D. Reshape into a vector before applying it. (or use a convolution that has the same size as the feature map)

• 3D CNN: swap 2D operations with 3D operations.

17

First Layer Filters

• Filters span space and time.

• We can visualise them by animating them through time.

• Moving edge filters.

• Not all filters change with time.

18

Large-scale Video Classification with Convolutional Neural Networks, Karpathy et al., 2014

3D CNNs for Video Understanding

• Slow Fusion: slowly fuse temporal information over the course of the network

• Adds shift invariance in time (same motion at a different time).

• Subsampling in space and time gives larger and larger context to each successive layer.

19

Large-scale Video Classification with Convolutional Neural Networks, Karpathy et al., 2014

Fusion Approaches

20

Video Classification Example

GT

pred

21 Large-scale Video Classification with Convolutional Neural Networks, Karpathy et al., 2014

Video Classification Example

Single frame is very good and even better with a multi-resolution approach

Slow fusion works better than early and late fusion

22 Large-scale Video Classification with Convolutional Neural Networks, Karpathy et al., 2014

Motion

23

source

Johansson, “Visual perception of biological motion and a model for its analysis.” 1973

24

source

Johansson, “Visual perception of biological motion and a model for its analysis.” 1973

25

Recap: Optical Flow

26

Slide from J Johnson

Action Recognition with Optical Flow

27 Simonyan and Zisserman, “Two-stream convolutional networks for action recognition in videos”, NeurIPS 2014

Slide from J Johnson

Simonyan and Zisserman, “Two-stream convolutional networks for action recognition in videos”, NeurIPS 2014 Slide from J Johnson

Two Stream Networks

28

Two Stream Networks

• Can be used to fuse different modalities:

• RGB and optical flow

• Image and Audio

• Image and Text

• …

• Typically late(-ish) fusion: process each modality separately before fusing.

29

Longer Temporal Context

• Use a sequence model (e.g. Transformer) across time.

• Can capture temporal changes.

MLP

Transformer

each:1xDx1x1 + pos. enc.

CNN CNN CNN CNN CNN CNN

CLS-Token

Tx3xHxW

30

Longer Temporal Context

• Encoder can be per frame, or other architectures e.g. 3D CNN: produce temporal features.

• Sequence model reasons across time.

• Hybrid architecture: CNN for processing clips, transformer for processing video (composed of clips).

• Pure transformer architectures?

31

Transformer for Video Understanding

32 Arnab et al, “ViViT: A Video Vision Transformer”, ICCV 2021

Video Vision Transformers

• Spatio-temporal tokens: each token comes from a “patch” in space and time.

• Attention is expensive ðª ð2 .

• Factorised attention: alternate spatial and temporal attention.

33

Factorised Attention

• Attention: input/output B x N x D (batch, tokens, channels)

• Samples in batch dimension are processed separately.

• Our input: B x T x D x H x W

• Idea: use batch dimension to process dimensions we do not want to include in the attention.

34

Temporal Attention

• Process each sample in the batch separately

• Process each spatial location separately

• Input B x T x D x H x W

• Permute: B x H x W x T x D

• Flatten: BHW x T x D

• Attention: BHW x T x D -\> BHW x T x D

• Unflatten: B x H x W x T x D

• Permute: B x T x D x H x W

35

Spatial Attention

• Process each sample in the batch separately

• Process each time step separately

• Input B x T x D x H x W

• Permute: B x T x H x W x D

• Flatten: BT x HW x D

• Attention: BT x HW x D -\> BT x HW x D

• Unflatten: B x T x H x W x D

• Permute: B x T x D x H x W

36

Factorised Attention

W

W

T

T

H

H

Spatial AttentionTemporal Attention37

Factorised Attention

• Alternating spatial and temporal attention layers.

• Allows propagating information across time and space.

• Complexity:

• Full attention: ðª (ðð»ð)2

• Factorised attention: ðª ð2ð»ð + ð(ð»ð)2

38

Task: Spatio-Temporal Detection

• Detect objects in a video and predict their actions.

• Tubelets: bounding box with time.

39

Image source

40 Sub-word Level Lip Reading With Visual Attention, Prajwal et al., 2022

Task: Lip Reading

Sub-word Level Lip Reading With Visual Attention, Prajwal et al., 2022

Lip Reading with Attention

41

Task: Audio Description

• Multi-modal task: audio-visual input -\> text

• Difficult: long-range context understanding

42 AutoAD: Movie Description in Context, Han et al., 2021

Multi-Modal Learning

• Often, we have multiple modalities: image, audio, text, sensor signal, 3D, temperature, etc.

• Fusion-based architectures are good to combine different input types.

• Process each modality separately into a common shape.

• Fuse and process jointly.

43

Processing Videos

• Expensive task even after all the subsampling.

• High compute and memory cost.

• Many tasks: image models work surprisingly well.

• Architectures: combine image and time understanding.

44

<http://cs231n.stanford.edu/slides/2023/lecture_10.pdf>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/WI2022/598_WI2022_lecture24.pdf>   
<https://kaldir.vc.in.tum.de/adl4cv/ws2122/7-Videos-Autoreg.pdf>   
<https://commons.wikimedia.org/wiki/File:Running.gif>   
<https://www.youtube.com/watch?v=1F5ICP9SYLU>   
<https://www.youtube.com/watch?v=1F5ICP9SYLU>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/WI2022/598_WI2022_lecture24.pdf>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/WI2022/598_WI2022_lecture24.pdf>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/WI2022/598_WI2022_lecture24.pdf>   
<htt
