# Computer Vision — Fourier Transforms
> Source: Google Drive file 1bFSD34LJjIUZ9y14ed6VcpzzJw_-KGNh · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Fourier Analysis

Computer Vision - Lecture 03

1

Further Reading

• Slides borrowed and adapted from S. Lazebnik, S. Seitz, A. Efros, D. Hoiem, B. Freeman, A. Zisserman

• Code for the examples in the slides is on the course website.

2

Observation 1

• From lecture 02: down-sampling leads to aliasing

3

Original: 512x512

64x64

16x16

Observation 2

• From lecture 02: Gaussian Blur is smoother than average filtering

4

Averaging in a square Gaussian Blur

Observation 3

• Hybrid Images (A. Oliva, A. Torralba, P.G. Schyns, Hybrid Images, SIGGRAPH 2006)

5 Source: twitter.com/NerdyRodent Sep 24,’23

Fourier Analysis

• Intuition: all these phenomena relate to fast and slow changing components of the image.

• To understand these better, we need a tool to analyse the frequency components of an image.

• For better understanding, we will start with 1D signals before moving to 2D.

6

Fourier Transform

Any(\*\*) univariate function can be expressed as a weighted sum of sinusoids of different frequencies (1807)

7 Jean-Baptiste Joseph Fourier (1768-1830)

Example: series for a square wave

∞ ෍

ð=1,3,5,…

ð 1sin(ðð¡)Slide credit: S. Lazebnik

Fourier analysis

Our building block:

Frequency

ð´sin(ðð¡ +ð)

Amplitude

Phase

Add enough of these to get any signal you want\!

Phase shift ð

Amplitude ð´

Period 2ðð

ð¡

Slide credit: S. Lazebnik

Complex Exponentials

9 Animation vs. Math, https://www.youtube.com/watch?v=B1J6Ou4q8vE

Complex Exponentials

• Euler’s Identity: ððð + 1 = 0

• Euler’s Formula: ððð = cosð + ð sinð

• Identity: ððð = cosð + ð sinð = −1 + 0

10

Image source

Basis Functions

Define a set of functions to use as a basis:

ðð¢ ð¡ = ðð2ðð¢ð¡, ð¢ ∈ (−∞,∞)

Given a signal ð(ð¡), we can represent it as a weighted combination of the basis functions with weights ð¹(ð¢):

ð ð¡ = න−∞∞ð¹(ð¢)ðð2ðð¢ð¡ðð¢

11

Basis functions

Inner product for complex functions ∞is:

ð,ℎ = නð ð¡ ℎ∗ ð¡ ðð¡

−∞Complex conjugate:

real part stays the same, imaginary part is flipped ð + ðð ∗ = ð − ðð

Our basis is orthonormal:

ðð¢1,ðð¢2 = ቊ1 0 if ð¢1 = ð¢2 otherwise

12

Finding the weights

ð ð¡ = න−∞∞ð¹(ð¢)ðð2ðð¢ð¡ðð¢

To express ð with the basis functions ðð¢, we need to find the weights ð¹(ð¢).

ð¹ ð¢ = ð,ðð¢ = න−∞∞ð(ð¡)ð−ð2ðð¢ð¡ðð¡

13

Fourier Transform

• Analysis process, decomposing a complex-valued function ð ð¡ into its constituent frequencies ð¹(ð¢).

• The inverse process is synthesis, which recreates ð ð¡ from ð¹(ð¢).

14

Fourier Transform

For each ð¢, ð¹(ð¢) is a complex number that encodes both the amplitude ð´ and phase ð of the sinusoid ð´sin(2ðð¢ð¡ +ð) in the decomposition of ð(ð¡): ð¹ ð¢ = Re ð¹(ð¢) + ð Im ð¹(ð¢)

ð´ = ð¹ ð¢ = Re(ð¹(ð¢))2 + Im(ð¹(ð¢))2, ð = tan−1 Im(ð¹(ð¢)) Re(ð¹(ð¢))

If ð(ð¡) is real, then Re ð¹(ð¢) = Re ð¹(−ð¢) Im ð¹(ð¢) = −Im ð¹(−ð¢)

15

Discrete Fourier Transform

When we only have ð discrete (evenly spaced) samples from a signal, we also only need a discrete set of ð basis functions.

16

Discrete Fourier Transform

ð¹ ð = ð,ðð = ð−1෍ð ð ð−ð2ððð ð

ð=0

• For each ð we compute the dot-product between the discrete signal ð and a discrete basis function ðð.

• This is just a matrix-vector multiplication\!

ð¹ = ∗ ( +ð )

ðð

17

Basis

Inverse DFT

We will use ð for the basis matrix.

• Forward DFT:

ð¹(ð) = σð=0 ð−1ð ð exp −ð 2ðð ðð , or ð¹ = ðð

• Inverse DFT:

ð(ð) = 1ðσð=0 ð¾−1ð¹ ð exp ð 2ðð ðð , or ð = 1ðð−1ð¹

ð−1 is the transpose of the complex conjugate of ð

18

Periodicity of DFT and inverse DFT

The result of DFT is periodic: because ð¹(ð) is obtained as a sum of complex exponentials with ð−1a common ð¹ ð + ðð = ෍ð ð exp ð−1ð=0

period of ð samples: −ð 2ðð ð ð + ðð

\= ෍ð ð exp ð=0

−ð 2ððð ð exp −ð2ððð = ð¹(ð)

Likewise, the result of the inverse DFT is a periodic signal: ð(ð¡ + ðð) = ð(ð¡) for any integer ð.

2D Fourier Analysis

First, we need 2D basis functions:

ðð¢,ð£ ð¥,ð¦ = ðð2ðð¢ð¥ðð2ðð£ð¦

\= ðð2ð(ð¢ð¥+ð£ð¦) = cos2ð ð¢ð¥ + ð£ð¦ + ð sin 2ð(ð¢ð¥ + ð£ð¦)

20

ð¢ ð£real

2D Basis Functions

ðð¢,ð£ ð¥,ð¦ = ðð2ð(ð¢ð¥+ð£ð¦)

21

ð¢ ð£imaginary

2D Basis Functions

ðð¢,ð£ ð¥,ð¦ = ðð2ð(ð¢ð¥+ð£ð¦)

22

Examples – Image Transformations

What happens when we scale the image?

Inverse effect for the magnitude

23

image

magnitude

Examples – Image Transformations

What happens when we rotate the image?

Rotates the same way.

24

image

magnitude

Examples – Image Transformations

What happens when we translate the image?

Translation does not affect the magnitude (only the phase).

25

image

magnitude

Real Images

image magnitude phase

26

imagemagnitude

Examples

27

Interpreting DFTs

28

image magnitude

horizontal (\!) lines

vertical (\!) lines

Interpreting DFTs

Away from the centre: high-frequency details

29

Close to the centre: low frequencies

Convolution theorem

Convolution in the spatial domain translates to multiplication in the frequency domain (and vice versa)

The Fourier transform of the convolution of two functions is the product of their Fourier transforms:

ℱ{ð ∗ ð} = ℱ{ð} ℱ{ð}

The inverse Fourier transform of the product of two Fourier transforms is the convolution of the two inverse Fourier transforms: ℱ−1{ð¹ðº} = ℱ−1{ð¹} ∗ ℱ−1{ðº}

2D convolution theorem example

Image Filter Filtered image

\*

\=

× FT(Image) FT(Filter)

FT(Filtered image)

\=

Slide: A Zisserman

Convolution theorem

Suppose ð and ð both consist of ð pixels

• What is the complexity of computing ð ∗ ð in the spatial domain? ð(ð2)

• And what is the complexity of computing ℱ−1 ℱ ð ℱ ð ?

ð(ðlog
