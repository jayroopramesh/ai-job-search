# Computer Vision — Generative Models
> Source: Google Drive file 16aWhF8e4OKEQp645gnvGp_bB8SUbQBdR · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Generative Models

Computer Vision - Lecture 14

1

Further Reading

• Slides from J Johnson

• Slides from R Gao

• Slides from B Wang

• CVPR 2022 Tutorial

• Course from P Holderrieth and E Erives

2

Basics: Generative Models

Dataset ð· = ð¥ð 1 ≤ ð ≤ ð} Inputs ð¥ð Outputs ð¦ð

Learn a generator that generates samples from the same distribution as the dataset: Training data: ðdata(x) Generated samples: ðmodel(x)

Learn generator such that ðmodel(x) similar to ðdata(x)

3

Discriminative vs. Generative

• Discriminative model: learn ð ð¦ ð¥

• Generative model: learn ð ð¥

• Conditional generative model: learn ð ð¥|ð¦

Density function: ð ð¥ ≥ 0, ׬ð ð ð¥ ðð¥ = 1

Different values of ð¥ compete for density.

4

Generative Models

Learn a probability distribution ð ð¥ over the domain ð¥ ∈ ð. “How likely will we find this image in the data?”

ð( ) ð( ) ð( ) ð( )

5

Recall: Bayes’ Rule

Bayes’ Rule lets us build generative models from other components.

Discriminative model

Conditional generative model

ð ð¥ ð¦ = ð ð ð¦ ð¦ ð¥

ð(ð¥)

Prior over labels

Generative model

6

Basics: Generative Models

• Explicit: define and solve for the density ð(ð¥)

• Implicit: sample from ð(ð¥) without estimating the density for samples

7

Generative Models

Explicit Models can compute ð(ð¥)

• Tractable Density

• Autoregressive models (MADE, NADE, PixelRNN, etc.)

• Approximate Density

• Variational Autoencoders

• Markov Chain

Implicit Models can only sample from ð(ð¥)

• Direct

• GANs

• Diffusion Models

• Markov Chain

• GSN

8 Updated from Ian Goodfellow, Tutorial on GANs 2017

Autoregressive Models

• Explicit model: fully visible belief network

• Chain distributions rule decomposes of pixel intensities

the likelihood of an image into ð ð ð¥ = ෑð(ð¥ð|ð¥1,…,ð¥ð−1) ð=1• Train by maximizing likelihood of training data.

• Main generative model in NLP.

9 Updated from Ian Goodfellow, Tutorial on GANs 2017

Goal: Learning a distribution

• Potentially very complex and high dimensional\!

• What is the probability that ð¥ ∈ ℝ64×64×3 is an image of a face?

10

Autoregressive Distribution Estimation

• rearrange an image into a sequence

• now, task can be seen a sequence prediction problem

• What is the colour distribution of the next pixel?

…

11

Connectionist learning of belief networks Neal RM,Artificial intelligence 1992

Autoregressive Distribution Estimation

ð ð¥ = ð ð¥1 ð ð¥2|ð¥1 ⋅ …⋅ ð ð¥ð ð¥1,…,ð¥ð−1

…

ð¥

ð¥1 ð¥2 ð¥3 ð¥4 ð¥5 ð¥ð−1 ð¥ð

ð ð ð¥ = ෑð(ð¥ð|ð¥1,…,ð¥ð−1) ð=1The neural autoregressive distribution estimator

Pixel Recurrent Neural Networks

12 Larochelle H, Murray I, AISTATS 2011

Van Oord A, Kalchbrenner N, Kavukcuoglu K, ICLR 2016

Autoregressive Distribution Estimations

• In general: ð(ð¥ð|ð¥1,…,ð¥ð−1) might still be very complicated.

• But images are easy:

• we store them 8 bit per channel (RGB)

• 256 element softmax per channel and pixel

• models the exact distribution

13

Sampling

ð(ð¥1)

ð ð¥2|ð¥1

ð ð¥3|ð¥1,ð¥2

…

ð ð¥ð ð¥1,…,ð¥ð−1

Created by Shmidt Serge

Created by Shmidt Serge

Created by Shmidt Serge

Created by Shmidt Serge

14

Inference

ð ð¥ = ð ð¥1 ð ð¥2|ð¥1 ð(ð¥3|ð¥1,ð¥2) ⋅ …⋅ ð ð¥ð ð¥1,…,ð¥ð−1

0.12

0.94

0.86 0.99

ð(ð¥1)

0.12

ð ð¥2|ð¥1

Created by Shmidt Serge

0.94

ð ð¥3|ð¥1,ð¥2

Created by Shmidt Serge

0.86

Created by Shmidt Serge …

ð ð¥ð ð¥1,…,ð¥ð−1

0.99

Created by Shmidt Serge

15

Learning - NN

…

ð¥1ð¥2ð¥3

ð¥ð−1

layer 1 layer 2

ð(ð¥1)

ð ð¥2|ð¥1

ð ð¥3|ð¥1,ð¥2 ð ð¥4|ð¥1,ð¥2,ð¥3

… …

…

ð ð¥ð ð¥1,…,ð¥ð−1

The neural autoregressive distribution estimator Larochelle 16

H, Murray I AISTATS 2011

Learning - CNN

• Idea: mask the weights of the convolutions

1 1 1 1 1 1 1 1 1 1 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0

Mask A

for the first layer

Pixel Recurrent Neural Networks Van Oord A, Kalchbrenner N, Kavukcuoglu K ICLR 2016 1 1 1 1 1 1 1 1 1 1 1 1 1 0 0 0 0 0 0 0 0 0 0 0 0

Mask B

for all other layers

17

Learning – CNN Receptive Field

x

blind spot

18

Results

Pixel Recurrent Neural Networks Van Oord A, Kalchbrenner N, Kavukcuoglu K ICLR 2016

Conditional Image Generation with PixelCNN Decoders Van den Oord A, Kalchbrenner N, Espeholt L, Vinyals O, Graves A

NeurIPS 19

2016

Dall-E

• Autoregressive model made fast by first learning a compressed discrete image representation

• Generation in “token-space”

• Conditioned on text prompts

• Large-scale training 400M image-text pairs

Ramesh, Aditya, Mikhail Pavlov, Gabriel Goh, Scott Gray, Chelsea Voss, Alec Radford, Mark Chen, and Ilya Sutskever. "Zero-shot text-to-image generation." In International Conference on Machine Learning, pp. 8821-8831. PMLR, 2021.

20

VQ-VAE

• Down-sample and compress the image into a lower- dimensional, discrete representation.

• Bottleneck: replace activations with closest vector from a learned codebook.

21 Neural Discrete Representation Learning Aaron van den Oord, Oriol Vinyals, Koray Kavukcuoglu, 2017

Dall-E

• One of the first examples of very good generalisation: “an illustration of a baby daikon radish in a tutu walking a dog”

22

Recall: Neural (Flow) Fields

Φ:ℝ2 → ℝ2

(x,y)

Neural Network (Φ)

Φ:ℝ2 → ℝ2

(x,y)

Neural Network (Φ)

Eulerian Flow Field

23 \[Slide: Srinath Sridhar, Towaki Takikawa at CVPR ‘22 Tutorial on Neural Fields in Computer Vision \]

Magnetic Field

\[Koldora CC\]

\[Figure: Yaron Lipman\]

Converting Samples

• Idea: convert samples from a simple distribution into samples from the data distribution

• Learn a neural field to represent the flow from ð¥ð to ð¥0

• ð¥ð¡−1 = ð ð¥ð¡ + ð¥ð¡

24

ð¥ð

ð¥0

adapted from https://cvpr2022-tutorial-diffusion-models.github.io/

Flow between distributions

25

ð¥ð ð¥0 ð¥ð¡

Diffusion Models

• Generate an image in small steps from (Gaussian) noise ð

• Instead of directly learning a model for ðð(ð¥|ð), learn small steps along a Markov chain

ð¥ð ð¥0

Diffusion process ð(ð¥ð¡|ð¥ð¡−1)

…

ð¥ð−1 ð¥1 Reverse diffusion process:ðð (ð¥ð¡−1|ð¥ð¡) 26

27 Denoising Diffusion Probabilistic Models Jonathan Ho, Ajay Jain, Pieter Abbeel, 2020

Dhariwal, Prafulla, and Alexander Nichol. "Diffusion models beat gans on image synthesis." NeurIPS’21.

Noise Schedule

• Learn a model to generate ðð(ð¥ð¡−1|ð¥ð¡)

• Construct the diffusion process:

ð ð¥ð¡ ð¥ð¡−1 = ð© ð¥ð¡; 1 − ð½ð¡ð¥ð¡−1,ð½ð¡ð¼

• ð½ð¡ is a variance schedule – often fixed

• There ð¥ð¡ from is ð¥a 0

closed-form solution to sample ð ð ð¥1:ð ð¥0 = ෑð¡=1

ð(ð¥ð¡|ð¥ð¡−1)

Noise Schedule

ð ð¥ð¡ ð¥ð¡−1 = ð© ð¥ð¡; 1 − ð½ð¡ð¥ð¡−1,ð½ð¡ð¼

Random noise image ðð¡\~ð© 0,ð¼

ð¥ð¡ = ð¼ð¡ð¥ð¡−1 + 1 − ð¼ð¡ðð¡−1

ð¼ð¡ = 1 − ð½ð¡ and തð¼ð¡ = σð=1 ð¡ ð¼ð

Applying iteratively yields:

ð¥ð¡ = തð¼ð¡ð¥0 + 1 − തð¼ð¡ð

28

Noise Schedule

ð¥ð¡ = തð¼ð¡ð¥0 + 1 − തð¼ð¡ð

Not exactly linear interpolation.

29

Noise Schedule

ð¥ð¡ = തð¼ð¡ð¥0 + 1 − തð¼ð¡ð

It looks like steps \> 500 are pure noise, but they are not. These are very important for the model to learn.

30

Training a diffusion model

• Generate training examples (ð¥ð¡,ðð¡)

• Loss ð ð¥ð¡,ð¡ − ðð¡ 22 (simple L2 loss)

31

Sampling from a diffusion model

Sample a noise image: ð¥ð\~ð© 0,ð¼

for ð¡ = ð,…,1:

ð§\~ð© 0,ð¼ ð¢ð ð§ \> 1 ðð¥ð¬ð 0

ð¥ð¡−1 = 1ð¼ð¡ ð¥ð¡ − 1−ð¼ð¡

1−ഥð¼ð¡ ð ð¥ð¡,ð¡ + ð½ð¡ ð§

Evaluate diffusion model ð times to generate one sample.

32 Denoising Diffusion Probabilistic Models Jonathan Ho, Ajay Jain, Pieter Abbeel, 2020

Predicting images instead of noise

• An equivalent model can be trained by learning to predict ð¥0 instead: ð ð¥ð¡,ð¡ − ð¥0 22

• We can use ð¥ð¡ = തð¼ð¡ð¥0 + 1 − തð¼ð¡ð to convert between sampling steps and noise.

• In practice predicting noise works often a bit better: more diversity during training.

• Predict ð¥0 model has the same target for every timestep: easier overfitting/memorisation.

33

Large Scale Diffusion Models

• Conditional diffusion: trained conditional on text input.

• Large scale training: \>1B images (\&text)

• Several details:

• Often more stable to predict noise instead of the clean sample. One can always compute one from the other.

• Noise schedule is important.

• Latent diffusion.

34

Latent Diffusion

• Diffusion needs many evaluations of the noise estimator.

• We latent can representation. make it cheaper but first compressing the image into a • Train an encoder decoder architecture: VQ-VAE.

• E.g.: D=4, H’ = H/4, W’ = W/4

Enc LS

Dec

3 x H x W latent space

3 x H x W D x H’ x W’

35

Stable Diffusion 1

• Conditional diffusion model.

• Latent diffusion.

• U-Net architecture + cross attention layers to text & timestep36

Note: Add Time Dependency

• The score function is timestep-dependent.

• ð ð¥,ð¡

• Add time dependency

• Assume time dependency is spatially homogeneous.

• Add one scalar value per channel ð(ð¡)

• Parametrize ð(ð¡) by MLP / linear of Fourier basis.

ð ⊕

MLP

Time embedding

\[ð¬ð¢ð§ððð, ðð¨ð¬ððð, …\]

Unet in Stable Diffusion 1

(conv\_in): Conv2d(4, 320, kernel\_size=(3, 3), stride=(1, 1), padding=(1, 1)) (time\_proj): Timesteps() (time\_embedding): TimestepEmbedding

(linear\_1): Linear(in\_features=320, out\_features=1280, bias=True) (act): SiLU() (linear\_2): Linear(in\_features=1280, out\_features=1280, bias=True) (down\_blocks):

(0): CrossAttnDownBlock2D (1): CrossAttnDownBlock2D (2): CrossAttnDownBlock2D (3): DownBlock2D (up\_blocks):

(0): UpBlock2D (1): CrossAttnUpBlock2D (2): CrossAttnUpBlock2D (3): CrossAttnUpBlock2D (mid\_block): UNetMidBlock2DCrossAttn

(attentions): (resnets): (conv\_norm\_out): GroupNorm(32, 320, eps=1e-05, affine=True) (conv\_act): SiLU() (conv\_out): Conv2d(320, 4, kernel\_size=(3, 3), stride=(1, 1), padding=(1, 1))

Elfwing et al., Sigmoid-Weighted Linear Units for Neural Network Function Approximation in Reinforcement Learning, 2017

SiLU: Sigmoid Linear Unit

• silu ð¥ = ð¥ð ð¥

• ð ð¥ = ðð¥

1+ðð¥

• Gradients are not cut off before 0

• Can be more stable than ReLU.

• Higher computational cost.

39

Large Scale Diffusion Models

DeepFloyd IF Dalle-2 Bing Midjourney SDXL

40

Diagram credit @nrehiew\_

Flux

• Code/models

• Transformer-based architecture

• Latent diffusion model

• Flow-based model

41

Learning better prompts

• Original: a cat drinking a pint of beer

• Enhanced: A whimsical feline sipping a frothy pint of golden ale, the condensation on the glass glistening in the warm light of a cozy pub, the cat's whiskers twitching as it savors the rich flavor and aroma of the beer, its paws curled around the glass as it sits on a worn wooden stool, surrounded by the rustic charm of a classic British pub.

42

flux-ai.org, Feb’2025

Evaluation

• Evaluation of explicit generative models is easy:

• Measure log ð ð¥ on a test set.

• Whichever model has higher probability wins.

• Evaluation of implicit models is very difficult.

• We can only sample from the model.

• We do not know how to measure the quality/probability of a sample.

43

Human Evaluation

• Ask people which model they prefer.

Example: Emu vs. SDXL

• Preference is vague.

• Also prompt, include realism, faithfulness etc. to text • Difficult model. to scale/use to improve Dai et al., Emu: Enhancing Image Generation Models Using Photogenic Needles in a Haystack, 2023

44 Podell et al., SDXL: Improving Latent Diffusion Models for High-Resolution Image Synthesis, 2023

Fréchet Distance

• Dog and owner walk on separate paths.

• Can only go forward.

• FD: the shortest possible leash that allows both to complete the path.

45 Heusel et al., GANs Trained by a Two Time-Scale Update Rule Converge to a Local Nash Equilibrium, 2017

Maurice Fréchet,1878-1973

FID: Fréchet Inception Distance

• Measure the distance between generated images and real images.

• Measure the distance in feature space (Inception v3 model).

• Input: feature extractor ð ð¼ ∈ ℝð, real imges ℐð, samples ℐð.

• Compute ð ℐð and ð ℐð

• Fit Gaussians to each set: ð©(ðð,Σð), ð©(ðð,Σð)

• ðð¹ = ðð − ðð 2 2+ tr Σð + Σð − 2 ΣðΣð

12

46 Heusel et al., GANs Trained by a Two Time-Scale Update Rule Converge to a Local Nash Equilibrium, 2017

FID

• Real ima
