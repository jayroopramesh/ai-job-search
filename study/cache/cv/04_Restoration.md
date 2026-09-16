# Computer Vision — Restoration
> Source: Google Drive file 1HVMJbeAoYzum37HtGpTL0tsJtFKJ_4sG · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Image Restoration

Computer Vision – Lecture 04

1

Practicals: weeks 3,4,6,7

2

Further Reading

• Slides from A Zisserman

• Slides from A Efros

• Slides from A Torralba and A Oliva

• Video from S Seitz: Fourier Transform in 5 minutes: The Case of the Splotched Van Gogh, Part 3

3

4

https://www.youtube.com/watch?v=Vxq9yj2pVWk

Image Restoration

• In contrast to image enhancement, in image restoration the degradation is modelled.

• This enables the effects of the degradation to be (largely) removed.

• The objective is to restore a degraded image to its original form.

5

Typical Degradations

6

Optical Blur Motion Blur

Spatial quantization Additive noise

Original

Modelling Degradation

We can model an observed image as:

ð ð¥,ð¦ = ׭ð ð¥ − ð¢,ð¦ − ð£ ð ð¢,ð£ ðð¢ ðð£ + ð(ð¥,ð¦)

This means the observed image ð is created from the true image ð through a convolution with ð and added noise ð.

ð ð¥,ð¦

ð ð¥,ð¦

\= ∗ +

7

ð ð¥,ð¦

ð ð¥,ð¦

Degradation Model

ð ð¥,ð¦ = ׭ð ð¥ − ð¢,ð¦ − ð£ ð ð¢,ð£ ðð¢ ðð£ + ð(ð¥,ð¦)

• This is only one way of modelling degradation. Others are possible too.

• ð ð¥,ð¦ is called the impulse response or point spread function of the imaging system.

8

Fourier Transforms

Image

Filter Filtered image

\* =

FT(Image) FT(Filter) FT(Filtered image)

× =

9

Fourier Transforms

• Ignoring additive noise for now.

• Instead of a convolution in image space, we can use multiplication in Fourier space.

ð = ð ∗ ð → ðº = ð· × ð¹ ðº = ð¹ð ð , ð· = ð¹ð ð· , ð¹ = ð¹ð(ð¹)

• Recover an estimate መð of the true image:

መð = ð¹ð−1 ðºð· = ð¹ð−1 ð¹ð(ð) ð¹ð(ð)

10

Filter Inversion

Blurred Image

Filter “deblurred” image

FT(Blurred Image) FT(Filter) FT(deblurred image)

/ =

11

What went wrong?

• The deblurred image is almost purely noise

• This is because we are dividing by small numbers

• The filter is almost 0 in the high- frequency regions

• We are amplifying the noise\!

12

Zoom into “deblurred image”

FT(Filter)

The Wiener Filter

• To avoid up-scaling the noise, add a second constraint

• Minimise: ð¼ ð − መð 2

• The reconstruction should be close to the observation

13

Norbert Wiener 1894-1964

The Wiener Filter

• In Fourier space we had

ðº ð¢,ð£ = ð· ð¢,ð£ ð¹ ð¢,ð£ + ð(ð¢,ð£)

• Bad solution (noise amplification):

෠ð¹ ð¢,ð£ = 1

ð·(ð¢,ð£) ðº ð¢,ð£

• Wiener Filter: ෠ð¹ ð¢,ð£ = ð(ð¢,ð£)ðº(ð¢,ð£)

14

The Wiener Filter

complex conjugate

ð ð¢,ð£ = ð· ð¢,ð£ ð·∗ ð¢,ð£

2ð(ð¢,ð£) + ð¾(ð¢,ð£)

• ð the ð¢,ð£ original = ð¼ signal ð¹ ð¢,ð£ 2 is the mean power spectral density of • ð¾ the ð¢,ð£ noise = ð¼ ð ð¢,ð£ 2 is the mean power spectral density of • Often: ð ð¢,ð£ = 1 and ð¾ ð¢,ð£ is a small (real) constant.

15

Energy Spectral Density

• Power spectrum: distribution of total energy across frequencies.

• This is the magnitude diagram that we have been looking at.16

imagemagnitude

Energy Spectral Density

17

Image from A Torralba and A Oliva

Interpretation

We can rewrite the filter as:

ð ð¢,ð£ = ð·(ð¢,ð£)

1

1 1 + 1

ð· ð¢,ð£ 2ððð(ð)

Filter inversion Scaling factor Signal-to-noise ratio

Intuition: expected we noise, invert so that the filter, we do but not scale end inversely up amplifying with the it.

18

Filter Inversion

Blurred Image

Filter “deblurred” image

FT(Blurred Image) FT(Filter) FT(deblurred image)

/ =

19

Deblurring

Blurred Image

FT(Blurred Image)

\* =

20

FT(Filter)

Wiener Filter

FT(deblurred image)

Deblurred Image

Deblurring with a WF

• Boundary artifacts because DFT assumes infinitely tiled image.

• In practice, we do not know the filter that degraded the image\!

21

Deblurring with WF

Blurred Image

Original

22

WF with varying ð

Finding WF Parameters

• It is difficult to find good parameters automatically, but easy for humans to see.

• Photoshop has a “strength” slider.

• Bayesian optimization:

23

Motion Blur and WFs

Motion blur can be modelled as a convolution with a line segment filter.

Algorithm to remove motion blur: 1. Rotate image so that blur is horizontal. 2. Estimate length of blur. 3. Construct line segment filter. 4. Compute and apply Wiener filter.

24

line segment filter

Simulated motion blur

Deblur Example

Needs guessing the blur that was “applied”:

My guess:

• Angle: 3 deg

• Blur: 18px

• Noise: 0.03

25

original deblurred

Generative Models

Instead of convolutions we can formulate the degradation as a linear operation on pixels.ð = ð´ð + ð

• For an image with ð pixels, the true image ð and the observed image ð can be written as ð-vectors.

• ð´ is an ð × ð matrix.

• ð is an ð-vector of noise.

26

Inverse Problem

We can estimate the true image by optimising a cost function:

መð = argminð ð − ð´ð 2 + ðð(ð)

• ð´ð is a generated image. We minimise the difference to ð.

• ð(ð) is a prior or regulariser for the optimisation.

• ð is a weight, controlling the influence of regularisation.

• For example: ð ð = ∇ð 2 (∇ð is the gradient image)

27

Inverse Problem

• ð´ can affect each pixel individually and is thus more flexible than convolution.

• ð´ needs to be manually defined and depends on the problem we are solving.

28

Inverse Problem: Super Resolution

If we register multiple images of the same scene (how: later), we get multiple samples per pixel\!

29

Image from A Zisserman

Super Resolution

• Pixels as samples.

• After registration, samples will not align perfectly.

• Can treat it as higher sampling rate (Shannon-Nyquist).

• Higher resolution estimate is possible.

• Construct ð´ matrix based on bi-linear interpolation weights.

⋅ ⋅ ⋅

⋅ ⋅ ⋅

⋅ ⋅ ⋅

⋅ ⋅ ⋅

⋅ ⋅ ⋅

⋅ ⋅ ⋅

multiple samples per pixel

30 ⋅ ⋅ ⋅

…

⋅ ⋅ ⋅

⋅ ⋅ ⋅

many images

Super Resolution

Images from Mars lander: rotating camera – capture the same frame multiple times

31

Image from A Zisserman

Super Resolution

• 2x super resolution from 25 JPEG images

• JPEG compression artefacts largely removed

32 Image from A Zisserman

Mirror Average Example

• A virus has corrupted our image\! It was blended with a mirrored version (40% old vs. 60% mirrored) and noise was added.

• መð = argminð ð − ð´ð 2 + ðð(ð)

• How does ð´ look like?

33

Mirror Matrix

• Construct a matrix ð that mirrors an image of size ð» × ð.

• We represent the image as a vector containing its pixels.

• How do we flip a row of pixels horizontally?

ð¾ =

0 ⋯ 1 ⋮ ⋰ ⋮ 1 ⋯ 0

, ð¾ ∈ ℝð×ð

• Now we can build ð as a block-diagonal ð = diagmatrix H ð=1 ð¾

of ð¾s.

ð =

ð¾ ⋯ 0 ⋮ ⋱ ⋮ 0 ⋯ ð¾

, ð ∈ ℝð»ð×ð»ð

34

Image Priors

• We only have noisy observations.

• Assume a prior (models what a reasonable image is):

• For example smoothness: ð ð = σð¥,ð¦ Δð¥ + Δð¦

• ∇ð ð¥,ð¦ = Δð¥Δð¦ is the image gradient. Can be computed with the Sobel Operator or finite differences.

35

Optimisation

• We assume that our image was made with ð´ = 410ð¼ + 610ð

• Find: መð = argminðð¸(ð)

• ð¸ ð = ð − ð´ð 2 + ðð(ð)

• Can be done with gradient descent on ð:

• Compute the gradient ∇ð¸ of ð − ð´ð 2 
