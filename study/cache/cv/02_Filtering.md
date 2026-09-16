# Computer Vision — Filtering
> Source: Google Drive file 1pufunNINbxn1S_RSuh7yk-fLvjcWXtLz · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Image Transformations and Enhancement

Computer Vision - Lecture 02

1

Further reading

• Some slides adapted from Alyosha Efros, Derek Hoiem, Svetlana Lazebnik

• Almost all examples on the slides today come from python code

2

By Scan, Fair use, https://en.wikipedia.org/w/index.php?curid=11751438

Code

https://colab.research.google.com/

3

4

Using Colab

• Cells separate code blocks.

• Cells can be run with the play button.

• A notebook is stateful\! Things might use outputs from previous cells.

• When you change things, make sure to run all necessary cells.

5

Using the code

• Can be helpful to understand the connection between the ideas and their implementation.

• Very useful for the practicals (and also for classes).

• The exam will not ask for implementation details.

6

Overview

• Images as functions

• Subsampling & upsampling

• Point-wise transformations

• Geometric transformations

• Image filtering

7

Why is Computer Vision hard?

What we see What a computer sees

import cv2 image = cv2.imread('02/image.jpg') print(image)

\[\[\[ 82 100 129\] \[ 83 101 130\] \[ 84 102 133\] ... \[ 23 34 54\] \[ 20 34 57\] \[ 17 33 56\]\] ...

8

Digital Images

red channel

green channel

blue channel

9

Images as Pixels

print(image.shape) gray = cv2.cvtColor(image, cv2.COLOR\_BGR2GRAY) print(gray.shape) print(gray)

height, width, channels (B, G, R)

(854, 1280, 3)

grayscale images have only one channel

(854, 1280)

top left pixel

\[\[107 108 109 ... 39 39 38\] \[112 113 114 ... 70 67 64\] \[117 118 120 ... 174 168 164\] ... \[184 183 182 ... 25 26 26\] \[184 183 182 ... 25 26 26\] \[184 183 182 ... 25 25 26\]\]

bottom right pixel

2D array of pixel intensities 10

Images as Functions

• We can interpret an image as samples from a continuous 2D function ð(ð¥,ð¦)

• ð maps from 2D coordinates to image intensities

• The functional representation is very useful to express operations on images (e.g. filtering, transformations, etc.)

11

Reconstruction: converting a sampled representation back into a continuous function by “guessing” what happens between the samples

Source: S. Marschner (via A. Efros)

Sampling and reconstruction

Sampling: recording the function’s values at a discrete set of locations

12

13 Source: S. Marschner (via A. Efros)

Sampling and reconstruction

• Simple example: a sine wave

14 Source: S. Marschner (via A. Efros)

Sampling and reconstruction

• Simple example: a sine wave

• What if we “missed” things between the samples?

• Unsurprising result: information is lost

15 Source: S. Marschner (via A. Efros)

Sampling and reconstruction

• Simple example: a sine wave

• What if we “missed” things between the samples?

• Unsurprising result: information is lost

• Surprising result: indistinguishable from lower frequencies

16 Source: S. Marschner (via A. Efros)

Sampling and reconstruction

• Simple example: a sine wave

• What if we “missed” things between the samples?

• Unsurprising result: information is lost

• Surprising result: indistinguishable from lower frequencies (or even higher frequencies)

Sampling and reconstruction

• Simple example: a sine wave

• What if we “missed” things between the samples?

• Unsurprising result: information is lost

• Surprising result: indistinguishable from lower frequencies (or even higher frequencies)

• Aliasing: signal “traveling in disguise” as other frequencies

17 Source: S. Marschner (via A. Efros)

good

https://en.wikipedia.org/wiki/Nyquist-Shannon\_sampling\_theorem

Nyquist-Shannon sampling theorem

When sampling a signal at discrete intervals, the sampling frequency must be at least twice the maximum frequency of the input signal to allow us to reconstruct the original perfectly from the sampled version

bad

18

Aliasing “in the wild”

Source

Disintegrating textures Moiré patterns, false color

Source

Source

19

Anti-aliasing

What are possible solutions?

• Sample more often (if you can)

• Before sampling: get rid of all frequencies that are greater than half the new sampling frequency

• Will lose information, but still better than aliasing

• How to get rid of high frequencies?

• Apply a smoothing or low-pass filter

20

Subsampling Images

• Goal: reduce the resolution of an image by a factor of 2ð

• Idea: multiple let’s of delete 2ð

every pixel with coordinates that are not a factor 4 factor 8 factor 16

• Aliasing problems in high-frequency regions\!

21

Subsampling Images

Idea: remove high-frequency details first (by blurring \[later\])

factor 4 factor 8 factor 16

beforeafter

22

Upsampling Images

How to increase the resolution by a factor of 2

upsample

how do we determine the colours of the missing pixels?

Interpolation\!

23

Interpolation

• We will express the image as a function ð(ð¥,ð¦) given at integer coordinates

• Upsampling by 2 means finding values for ð(ð¥ + ð¿ð¥,ð¦ + ð¿ð¦) with ð¿ð¥,ð¿ð¦ ∈ {0, 12}

• Define some shorthands: A ≔ ð 0,0 B ≔ ð 1,0 C ≔ ð 0,1 D ≔ ð 1,1

• Here: math will be with grayscale images only. In practice: process each channel separately

((0,0) 12,0)

(1,0) (2,0)

(0,12) (12,12) (0,1) (1,1) (2,1)

(0,2) (1,2) (2,2)

24

Bilinear Interpolation

• Intuition: new values should lie between existing ones: ð 12,0 = ð(0,0) + 2

ð(1,0)

• After filling in the middles between known points, centres between 4 pixels can be filled. Well defined:

ðµ + ð· 2

ð´ + 2 ðµ + 2 ð¶ + 2

ð· = ð´ + ðµ + 4 ð¶ + ð·

\=

ð´ + 2 ð¶ + ðµ + 2

ð· 2 25

ð´ ð´ + ðµ

2

ðµ

ð´ + ð¶ 2

ð¶ ð¶ + ð·

2

ð·

Intuition:

ð¥1,ð¦1 ð¥2,ð¦1

A B

Formalized: C D

ð ð¥,ð¦ = ð¤11ð´ + ð¤21ðµ +ð¤12 ð¶ + ð¤22ð·

ð¥1,ð¦2 ð¥2,ð¦2 ð¤11 = ð¤12 = adapted from from S. Lazebnik

ð¥2 − ð¥ ð¥ð¥2 2 − − ð¥ð¥ 1 ð¥2 − ð¥1 ð¦2 − ð¦ ð¦ð¦ 2 − − ð¦ð¦1

1

ð¦2 − ð¦1

ð¤21 = ð¤22 = ð¥ − ð¥1 ð¦2 − ð¦ ð¥(ð¥ 2 − − ð¥ð¥1 1) ð¦ð¦ 2 − − ð¦ð¦1

1

ð¥2 − ð¥1 ð¦2 − ð¦1

26

Generalized Bilinear Interpolation

http://en.wikipedia.org/wiki /Bilinear\_interpolation

1D Interpolation

2D Interpolation

27

Source: Wikipedia

Other Interpolation Schemes

Image source 28

Useful Interpolation Properties

• Nearest Neighbour Interpolation

• Does only use values already in the data

• (Bi-) Linear Interpolation

• Does not create samples outside of the range of interpolants

• (Bi-) Cubic Interpolation

• Is smooth (differentiable) everywhere

Image Transformations

• Images as functions can help formulating resampling.

• The functional representation allows us to do other transformations too\!

• A transformation creates a new image ð′ from ð.

• Point-wise transformation: ð′ ð¥,ð¦ = ð¡(ð ð¥,ð¦ )

• Geometric transformation: ð′ ð¥,ð¦ = ð(ð ð¥,ð¦ )

• Image filtering: ð′ ð¥,ð¦ = ð¹ ð(ð¥,ð¦) , for a neighbourhood ð ð¥,ð¦ = ð ð¢,ð£ “ ð¢,ð£ is a neighbour of (ð¥,ð¦)”}

29

Point-Wise Transformations

• ð′ ð¥,ð¦ = ð¡(ð ð¥,ð¦ )

• Changes the range of the image

• Negative: ð′ = 1 − ð

30

Point-Wise Transformations

• ð′ ð¥,ð¦ = ð¡(ð ð¥,ð¦ )

• Changes the range of the image

• Negative: ð′ = 1 − ð

• Contrast: ð′ = ðð + ð

31

Point-Wise Transformations

• ð′ ð¥,ð¦ = ð¡(ð ð¥,ð¦ )

• Changes the range of the image

• Negative: ð′ = 1 − ð

• Contrast: ð′ = ðð + ð

• Gamma correction: ð′ = ðð¾

32

Geometric Transformations

• ð′ ð¥,ð¦ = ð(ð ð¥,ð¦ )

• Changes the domain of the image

• Translation: ð ð¥,ð¦ = (ð¥ + ð¿ð¥,ð¦ + ð¿ð¦)

33

Geometric Transformations

• ð′ ð¥,ð¦ = ð(ð ð¥,ð¦ )

• Changes the domain of the image

• Translation: ð ð¥,ð¦ = (ð¥ + ð¿ð¥,ð¦ + ð¿ð¦)

• Scaling: ð ð¥,ð¦ = (ð ð¥,ð ð¦)

34

Geometric Transformations

• ð′ ð¥,ð¦ = ð(ð ð¥,ð¦ )

• Changes the domain of the image

• Translation: ð ð¥,ð¦ = (ð¥ + ð¿ð¥,ð¦ + ð¿ð¦)

• Scaling: ð ð¥,ð¦ = (ð ð¥,ð ð¦)

• Rotation: ð ð¥,ð¦ = cosð sinð −sinð

cosð

ð¥ð¦

35

General Geometric Transformations

• We in a can unified express manner these (and more) geometric transformations • Homogeneous coordinates: ð¥ð¦ →

ð¥ð¦1

• Affine transformations:

ð ð¥,ð¦ = ð´

ð¥ð¦1

\= ðð11 21 ðð12 22 ðð13 23

ð¥ð¦1

36

Affine Transformation Examples

• Translation: ð ð¥,ð¦ = ð¥ + ð¿ð¥,ð¦ + ð¿ð¦ = 1 0 0 ð¿ð¥ 1 ð¿ð¦

ð¥ð¦1

• Scaling: ð ð¥,ð¦ = ð ð¥,ð ð¦ = ð  0 0 0 ð  0

ð¥ð¦1

• Rotation: ð ð¥,ð¦ = cosð sinð −sinð cosð 0 0

ð¥ð¦1

37

Affine Transformation Examples

• Horizontal Shearing:

ð ð¥,ð¦ = 1 0 ð 1 0 0

ð¥• ð¦1

Vertical Shearing:

ð ð¥,ð¦ = 1 ð 0 0 1 0

ð¥ð¦1

38

Combining Transformations

• How can we chain transformations? E.g. rotation and translation.

• Same idea: Homogeneous coordinates.

• Add a row to the matrix to make it square.

ðð11 21 ðð12 22 ðð13 23 →

ðð11 21 ðð12 22 ðð13 23 0 0 1

39

Affine Transformation Matrix

ðð11 21 ðð12 22 ðð13 23 0 0 1

ð¥ð¦1

\=

ðð2111ð¥ ð¥ + + ðð1222ð¦ ð¦ + + ðð13 23 1

We can essentially ignore the additional row and 1. (for now\!)

An affine transformation preserves:

• Collinearity: points) continue three to be or more collinear points after which the transformation. lie on the same line (called collinear • Parallelism: after the transformation. two or more lines which are parallel, continue to be parallel • Convexity transformation.

of sets: a convex set continues to be convex after the 40

Combining Transformations

• Affine transformations in 2D are 3x3 matrices with 6 variables.

• It is a group under composition of functions:

ðð11 21 ðð12 22 ðð13 23 0 0 1

ð11 ð12 ð13 ð21 ð22 ð23 0 0 1

\=

ðð11 21 ðð12 22 ðð13 23 0 0 1

41

Combining Transformations

• Simply multiply transformation matrices.

• Order matters\! (Applied right-to-left because we multiply points right)

Example – Rotation & Translation:

R =

1 0 ð¿ð¥ 0 1 ð¿ð¦ 0 0 1

ðð =

cosð −sinð 0 sinð cosð 0 0 0 1

ð =

cosð −sinð ð¿ð¥ cosð − ð¿ysinð sinð cosð ð¿ð¥sinð + ð¿ð¦ cosð

0 0 1

cosð −sinð ð¿ð¥ ≠ ðð = sinð cosð ð¿ð¦ 0 0 1

42

Rotation and Translation

Animating rotation, fixed x-translation

ðð: rotate then translate

43

ðð: translate then rotate

How did I create these animations?

• Transformations define a forward warp.

• ð ð¥,ð¦ = ð¥′,ð¦′ maps source pixels to target locations

• A naïve implementation takes every source pixel and draws it at its new location.

• Problem: holes\!

44

Scaling 2 0 0 0 2 0 0 0 1

Backward Warps

• Iterating over source pixels and drawing them at the target location is called a forward warp.

• Often better: for every target-image pixel: look up where it comes from – this is a backwards warp.

• We can compute backwards warps with a matrix inverse:

ð−1 ð¥,ð¦ =

ðð11 21 ðð12 22 ðð13 23 0 0 1

−1 ð¥ð¦1

• If the source location is between pixels: use interpolation\!

45

Image Filtering

Idea for (ð¥,ð¦)”}

a of set filtering: ð ð¥,ð¦ = ð′ ð¥,ð¦ (ð¢,ð£) = “ ð¹ ð¢,ð£ ð(ð¥,ð¦) is neighbour of imageð¥,ð¦

• We computation replace each on its point neighbourhood.

with some ð

• Neighbours ð¦ − ð£ ≤ ð. (total often size in a is square: 2ð + 1 ð¥ 2 − pixels) ð¢ ≤ ð and • ð¹ is called a filter.

• Usually, the same filter is applied everywhere.

46

Averaging

• Earlier we removed high frequency details by blurring.

• The easiest way to blur an image is by averaging a neighbourhood.

• Simple blur: ð¹ ð = 1|ð|σ ð¢,ð£ ∈ðð(ð¢,ð£)

47

5x5 17x17 33x33

Gaussian Blur

• Averaging gives the same weight to every pixel in the neighbourhood. image• It is better to discount pixels when they are further away.

ð¥,ð¦

weight

ð ð¹ ð = σ ð¢,ð£ ∈ð 1

ð¤(ð¢,ð£) σ ð¢,ð£ ∈ðð¤(ð¢,ð£)ð(ð¢,ð£)

normalization Gaussian Blur: ð¤ ð¢,ð£ = ð− ð¥−ð¢ 2ð2+ 2

ð¦−ð£ 2

48

averagingGaussian Blur

Averaging vs. Gaussian Blur

49

Discrete Convolution

Given discrete functions ð:ℤ ↦ ℝ and ð:ℤ ↦ ℝ, their convolution is defined as

\+∞ ℎ\[ð¥\] = ð ∗ ð \[ð¥\] = ෍ð ð¢ ð\[ð¥ − ð¢\]

ð¢=−∞

50

Discrete Convolution

If ð has finite support in the set ℳ = 0,…,ð − 1 , i.e., ð ð = 0,∀ ð ∈ ℤ\ℳ, then:

ð−1ℎ\[ð¥\] = ð ∗ ð \[ð¥\] = ෍ð ð¢ ð¢=0

51 ð\[ð¥ − ð¢ + ð 2 − 1

\]

ð: Kernel or filter

ð: Input function

ð−1ð ð¢ ð\[ð¥ − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\]

∗ Example

ℎ\[ð¥\] = ð ∗ ð \[ð¥\] = ෍ð¢=0

1 0 1

ð\[0\] ð\[1\] ð\[2\]

1 2 0 1 1 3 0 2

ð\[0\] ð\[1\] ð\[2\] ð\[3\] ð\[4\] ð\[5\] ð\[6\] ð\[7\]

52

ℎ\[1\] 2 Example

\= ð ∗ ð \[1\] = ෍ð ð¢ ð\[1 − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\] ð¢=01

1 0 1 ℎ 1 = 1 ∙ 1 + 0 ∙ 2 + 1 ∙ 0 = 1

1 2 0 1 1 3 0 2

53

ℎ\[2\] 2 Example

\= ð ∗ ð \[2\] = ෍ð ð¢ ð\[2 − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\] ð¢=01 3

1 0 1 ℎ 2 = 1 ∙ 2 + 0 ∙ 0 + 1 ∙ 1 = 3

1 2 0 1 1 3 0 2

54

ℎ\[3\] 2 Example

\= ð ∗ ð \[3\] = ෍ð ð¢ ð\[3 − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\] ð¢=01 3 1

1 0 1

ℎ 3 = 1 ∙ 0 + 0 ∙ 1 + 1 ∙ 1 = 1

1 2 0 1 1 3 0 2

55

ℎ\[4\] 2 Example

\= ð ∗ ð \[4\] = ෍ð ð¢ ð\[4 − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\] ð¢=01 3 1 4

1 0 1

ℎ 4 = 1 ∙ 1 + 0 ∙ 1 + 1 ∙ 3 = 4

1 2 0 1 1 3 0 2

56

ℎ\[5\] 2 Example

\= ð ∗ ð \[5\] = ෍ð ð¢ ð\[5 − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\] ð¢=01 3 1 4 1

1 0 1

ℎ 5 = 1 ∙ 1 + 0 ∙ 3 + 1 ∙ 0 = 1

1 2 0 1 1 3 0 2

57

ℎ\[6\] 2 Example

\= ð ∗ ð \[6\] = ෍ð ð¢ ð\[6 − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\] ð¢=01 3 1 4 1 5

1 0 1

ℎ 6 = 1 ∙ 3 + 0 ∙ 0 + 1 ∙ 2 = 5

1 2 0 1 1 3 0 2

58

ℎ\[ð¥\] 2 Example

\= ð ∗ ð \[ð¥\] = ෍ð ð¢ ð\[ð¥ − ð¢ + 1\]

ð = 3,ð¥ ∈ \[0,7\] ð¢=02 1 3 1 4 1 5 0

1 0 1

ℎ 0 = 1 ∙ 0 + 0 ∙ 1 + 1 ∙ 2 = 2

ℎ 7 = 1 ∙ 0 + 0 ∙ 2 + 1 ∙ 0 = 0

0 1 2 0 1 1 3 0 2

0

Boundary case: zero-padding

59

Multidimensional Discrete Convolution

If ð:ℤ × ℤ ↦ ℝ and ð: 0,…,ð − 1 × {0,…,ð − 1} ↦ ℝ
