# DL4H — L4: Initialisation & Normalisation
> Source: Google Drive file 1f4sinFabHkGfycQZo78O-PLXWsmuv6O0 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L4\_initialisation\_normalisation 

Deep Learning in Healthcare Training Neural Networks: Initialisation & Normalisation

Ana Namburete Department of Computer Science University of Oxford

Recap: NAG anticipates curvature

Nesterov

ℒ

ð¤0

Standard momentum:

• Update the parameters using:

ð¤),+ = ð¤) − ðð»ð¤) + ð½ ⋅ update)\*+

1

2

3 4a

ð¤/

4b

5ð¤\!""\#\_%&'%(

Nesterov:

• First, compute a look-ahead position

ð¤0112\_45647

ð¤\!""\#\_%&'%( = ð¤) − ð½ ⋅ update)\*+

ð¤/89 4

• Then, evaluate the gradient at this look-ahead position, ð»ð¤\!""\#\_%&'%(, and use it to compute the next update ð¤),+ = ð¤) − ðð»ð¤\!""\#\_%&'%( + ð½ ⋅ update)\*+

Learning Rate

Difficult to Choose a Learning Rate

• Difficult to choose a learning rate

• Too small: painfully slow convergence, or can fail to converge

• Too large: can lead to fluctuations around the minimum, or (worse) divergence

• The same learning rate applies to all parameter updates

• Learning rate schedules must be defined in advance

• High-dimensional loss functions are highly non-convex

• Risk of getting trapped in suboptimal local minima or saddle points

Step Decay: Halve the LR after every ð epochs, or Halve the learning rate after an epoch, if the validation error is more than what it was at the end of the previous epoch

Step Decay Linear Decay Cosine Decay

Exponential Decay: ð=ð-\*\#) where ð- and ð are hyperparameters, and ð¡ is the iteration number

ð/ð Decay: ð = .\!

\+,\#) where ð- and ð are hyperparameters, and ð¡ is the iteration number

Learning Rate Annealing

SGD, Momentum, and NAG update all parameters at the same time, with the same ð

Adaptive Methods

Adaptive Methods

• Problem:

• The magnitudes of the gradients often highly vary between layers

• Global learning rate may not be suitable

• Sparse input features may undergo infrequent updates

dense ð¥+dense ð¥/sparse ð¥0dense ð¥1

• Solution:

• Choose different learning rate for every weight in the network

• Several approaches to choose from Most methods either adapt to the variance of the weights, or to the local curvature

AdaGrad

• AdaGrad: adaptively scales the learning rate for each weight

• Intuition:

• Decay the learning rate for the parameters in proportion to their update history

ð£\! ð¤\!%\# = = ð£ð¤\!"\# \! − + ð£\! ð»ð¤ð+ \! ð $

⋅ ð»ð¤\!

Here, we just divide the Term to keep track of

learning rate by the the gradient history

cumulative gradient history

Note: As denominator grows, the learning rate decays very aggressively

RMSProp: controlled adaptation

• Adagrad decays the learning rate very aggressively

• After a while, the more frequently-updating parameters will receive very small updates due to the decayed LR

• Solution:

• Decay the denominator and prevent its rapid growth

• This is called RMSProp (“Root-Mean-Squared Propagation”)

Term to keep track of the gradient history

ð£\! ð¤\!%\# =ð½⋅ð£= ð¤\! − \!"\# ð£+ \! 1+ (1 ð − ⋅ ðð»ð¤ð½) ð»ð¤\!

\! $

\* With a similar set of equations for ð)

Adam: momentum and adaptation

• Another option to solve AdaGrad’s decay problem: Adam

• Adam: “Adaptive Momentum Estimation”

• Does everything that RMSProp does

• But also uses a cumulative history of the gradients

ð/ = ð½9 ⋅ ð/B9 + 1−ð½9 ð»ð¤/

ð£/ = ð½C ⋅ ð£/B9 +(1−ð½C) ð»ð¤/ C

0ð/ = ð/

1−ð½9/ -ð£/ = ð£/

1−ð½C/ ð¤/89 = ð¤/ − -ð£/ 1+ ð ⋅ ðð» 0ð/

In practice, ð½+ = 0.9 and ð½/ = 0.999

\* With a similar set of equations for ð)

Adam as a diagonal Hessian approximation

• Adam adapts step sizes

• Per-parameter scaling

• Large variance → smaller step

• Small variance → larger step

• Adam uses only the diagonal (per-parameter curvature)

• Full Newton → uses entire Hessian matrix

• Adam → uses diagonal only

ð» = Approximates curvatures diagonallyð\# × … × ⋮ ð⋮ $ … ⋱

Credit: Mitesh Khapra

Which optimiser to use?

• SGD: • Manages to reach a minimum • May take longer than other methods • Reliant on good initialisation and annealing schedule

• May get stuck in saddle points rather than local minima

• Adaptive methods

• Achieve fast convergence • Able to train complex models • Ideal if the input data is sparse • No need to tune the learning rate itself

ADAM is the default choice for now (ð½+ = 0.9, ð½/ = 0.999, ð = 1ð\*2)

But it does have 2 momentum parameters to be tuned

Note: Recent work has shown that SGD with momentum (Nesterov or classical) with a simple annealing learning rate schedule also works well in practice (typically starting with ð = 0.001)

Weight Initialisation

ℒ(ð¤K,ð¤9)

Weight Initialisation

• Selecting an initial set of values for ð\!

• Increase the chances of reaching a better local minimum

ð¤K

ð¤9

Zero Initialisation

• Any constant weight initialisation schemes perform poorly

Example: • 2 hidden units

• Biases = 0

• ReLU activation

• Weights: ð LB9 = ð L = ð½

\!ð = ð(ð)

If we forward-propagate, the outputs of both hidden units in ð¾\[/\]ℎ" the next layer will be ℎ$

ð\[$\]

ℎ) = ℎ\* = ReLU ð½ð¥) + ð½ð¥\*

ð¾\[+\]

Problem: ð\["\]

Both hidden units will have the same output, and thus an

ð¥+ ð¥/

identical influence on the loss, so they will have identical gradients Identical gradients → Identical updates, so the weights will always remain the same.

Random initialisation and scale

0ð

Consider normalised inputs (zero-mean, variance = 1)

Suppose the initial weight values have also been

ð¾\[5\] normalised (i.e. zero-mean). ð¾\[5\*+\] ð¥\# ð¥$ ð\[%\]

ðℎ)) ) ðℎ\*) \* ðℎ+) +

ð\[%&"\]

Weight initialisation as a statistical problem:

• Choose weight distributions that preserve information flow across layers

The goal of principled initialisation

• Choose a distribution for ð ℓ such that:

Var ℎ ℓ ≈ Var ℎ ℓ"\# ∀ℓ

• Consequences:

• Forward activations neither vanish nor explode

• Backward gradients remain well-scaled

• Signa—to-noise is preserved with depth

Interpretation: Initialisation should make deep signal propagation approximately variance-preserving.

Setup and assumptions

• Consider a fully connected feedforward network.

• For layer ℓ:

ð\[ℓ\] = ð¾ ℓ ð ℓ"\# + ð ℓ ð ℓ = ð(ð ℓ )

• We make the following standard assumptions:

• Inputs to each layer at i.i.d.

• Weights are i.i.d., zero mean:

ð¼ ð)\*ℓ = 0

• Weights and activations are independent at initialisation

• Biases are initialised to zero (or negligible variance)

Setup and assumptions

• We analyse one neuron, ð in layer ℓ

• Let:

ðℓB9 = number of incoming connections (fan−in)Var ð\[ℓ\] = ðQC

ℎ,ℓ

ð,ℓ

Variance of the pre-activation

For a single neuron )./0

ð:

ð"\[ℓ\] = &ð"&&'(

ℓ ℎ&ℓ\*(

Because and zero-mean:

the terms )./0 are independent Var ð"\[ℓ\] = \&Var ð"&&'(

ℓ ℎ&ℓ\*(

So \*:

Var ð ℓ = ð+\*(ð,- Var ℎ ℓ\*(

ð,ℓ

ð¾\[ℓ\]

ð\[ℓ\*+\]

This is the key forward-propagation relationship.

\* Using independence: Var ðℎ = Var ð Var(ℎ)

Effect of the activation function

Now consider:ℎ ℓ =ð ð ℓ

We by its approximate linearisation the around activation zero:

locally ð ð ≈ ð. 0 ð

This training approximation is valid early in Then:

Var ℎ ℓ ≈ ð. 0 - Var ð ℓ

ℎ,ℓ ð,ℓ

ð¾\[ℓ\]

ð\[ℓ\*+\]

\* Using independence: Var ðℎ = Var ð Var(ℎ)

Effect of the activation function

Substituting

Var ð ℓ = ð0B9ðQC Var ℎ ℓB9

into Var ℎ ℓ ≈ ðS 0 C Var ð ℓ yields

Var ℎ ℓ ≈ ð+ 0 $ð,"\#ð-$ Var ℎ ℓ"\#

Stability condition

To prevent exploding or vanishing gradients, we require:

Var ℎ ℓ ≈ Var ℎ ℓ\*(

This gives the condition:

ð. 0 -ðℓ\*(ð,- = 1

Solving for the weight invariance:

ð,- = 1

ðℓ\*(ð. 0 -

This is the general initialisation rule\!

Everything else follows from choosing ð.

Xavier initialisation

For tanh and sigmoid near zero: ð+ 0 ≈1 So

ð-$ = 1ðℓ"\#

This gives us Xavier (Glorot) initialisation:

ð)\*\~ð© 0, 1ðℓ"\#

Glorot, X., & Bengio, Y. (2010). Understanding the difficulty of training deep feedforward neural networks. International Conference on Artificial Intelligence and Statistics, 9, 249–256.

He initialisation

For ReLU: ð ð ≈max(0,ð) Under a symmetric zero-mean distribution:

• Half the activations are zero, half are linear

This gives:

ð¼ ð7 ð / = +/ so effectively ð7 0 / ≈ +/

Plugging into the stability condition:

ð8/ = 2ðℓ\*+

This gives us He initialisation:

ð9:\~ð© 0, 2ðℓ\*+

He, K., Zhang, X., Ren, S., & Sun, J. (2015). Delving deep into rectifiers: Surpassing human-level performance on ImageNet classification. IEEE International Conference on Computer Vision, 1026–1034. 38, 113, 183

Avoiding Vanishing / Exploding Gradients

Let ð¿ be the output layer in the network. For every layer ℓ,

Var ℎ ℓ = ðℓ1) Var ð ℓ Var ℎ ℓ1)

Unrolling this from the input ℎ\[3\] = ð¥ to the output ℎ\[5\]:

Var ℎ 5 = 4ℓ6)5

ðℓ1)Var ð ℓ Var ð¥

Variance multiplier

If we assume identical fan-in ðℓ\*+ = ð and identical weight varianceVar ð ℓ = ð8/ for all ℓ, this simplifies to

Var ℎ ℓ = ðð8/ 5 Var ð¥

Which initialisation scheme to use?

Activation function?

Tanh / Sigmoid

Xavier initialisation

Initialise weights as ð©\~ 0, ;ℓ\#$ +

or as ð©\~ 0, ;ℓ\#$/

,;ℓ

(i.e. the latter is the harmonic mean of ;ℓ\#$ +

and ;+ℓ )

ReLU

He initialisation

Initialise weights as

ð©\~ 0, ðℓ\*+

2

What breaks these assumptions in practice?

When initialisation theory stops being exact

• Assumptions that break in real networks:

• Activations are not independent

• Distributions are non-Gaussian

• Nonlinearities saturate

• Depth compounds small mismatches

• Data are non-i.i.d

• Implications:

• Variance drift still occurs

• Optimisation becomes fragile

• Normalisation layers become essential

Normalisation Layers

Training data Test data

Source distribution (distribution of the training set)

Note: Although BatchNorm was originally motivated by internal covariate shift, later work suggests this is not its primary benefit.

Motivation: Covariate Shift

Covariate shift

• A change in the data distribution between the training and test scenarios

• Problematic because the model needs to adapt to a new distribution

Target distribution (distribution of the test set)

Source distribution (distribution of the training set)

Motivation: Covariate Shift

Covariate shift

• A change in the data distribution between the training and test scenarios

• Problematic because the model needs to adapt to a new distribution

Training data Test data

Target distribution (distribution of the test set)

Internal covariate shift Can also happen during the training process, e.g. from epoch to epoch

Normalisation as Optimisation

• Network training converges faster if the inputs are whitened (i.e. mean = 0, variance = 1)

• We can explicitly ensure that each layer’s inputs are unit Gaussians (across each dimension)

\-ð¥ 0 = ð¥ 0 −ð¸ ð¥ 0

Var ð¥ 0

• Mini-batch allows us to compute the mean and variance of any layer

• Batch-normalisation introduces additional learnable parameters:

ð¾ 0 = Var ð¥ 0 and ð½ 0 =ð¸ð¥ 0

BatchNorm Mechanics

ACTIVATION, e.g. ReLU

LINEAR, e.g. fully-connected or CONV layer

Batch Normalisation

ð¥9.

ð + ð = ð9

Step 1 Compute batch statistics

Compute the empirical mean and variance across the batch

ð¥C.

ð + ð = ðC of ð inputs, ℬ= ð¥\#,…,ð¥.

ð/,ð/$ …ð¥f .

ð + ð = ðf ð/ = ð1M)0\#.

ð)ℓ

Note: BatchNorm cannot be applied to small batches.

Input (pre-)activations to the normalisation layer

Batch mean:

Batch variance:

ð/$ = ð1M)0\#.

ð)ℓ − ð/

$

Credit: Hung-yi Lee

Batch Normalisation

Step 2 Normalise layer inputs Oð)ℓ = ð)ð¥9.

ð + ð = ð9

Sð9ℓ − ð/

ð¥C.

ð + ð = ðC SðCð/$ + ð

…ð¥f .

ð + ð = ðf Sðf

ð/,ð/$

Credit: Hung-yi Lee

Batch NormalisationStep 3

Scale and shift Pð)ð¥9.

ð + ð = ð9

Sð9-ð9ð ∎

ð¥C.

ð + ð = ðC SðC-ðCð ∎

ℓ = ð¾ ℓ Oð)ℓ + ð½ ℓ

…Note:

ð¾ and ð½ are learnt during training.

ð¥f

.

ð + ð = ðf Sðf

\-ðf

ð ∎

ð/,ð/$

ð¾, ð½

Credit: Hung-yi Lee

Credit: Hung-yi Lee

Batch Normalisation

At test (or inference) time:

8ð7ℓ = ð7Problem: During testing, the batches are no longer available

Ideal solution:

• Compute ð and ð½ over the whole training set

Practical solution:

• Compute the moving average of ð and ð½ of the batches during training

ℓ − ð8 ð8\* + ð \<ð7ℓð¥ . ð + ð = ð Sð = ð¾ ℓ 8ð7ℓ + ð½ ℓ

\-ð ð ∎

ð, ð

ð¾, ð½ are computed

are learnable from the batch

parameters

Why is BatchNorm helpful?

• Smooths the optimisation landscape

• Enables larger learning rates as a consequence

• Reduces training times

• Reduces sensitivity to parameter initialisation

• Acts as implicit regularisation

BatchNorm improves conditioning by reducing sharp curvature along gradient directions.

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

ðº = number of groups ⁄\< = = number of channels per group

Further Reading

• Textbooks:

• Goodfellow et al. Deep Learning: Chapter 8 (Sec. 8.7)

• Articles:

• Ruder et al. Review of gradient descent algorithms \<link\>

• LeCUn et al. “Efficient BackProp” \<link\>

• He et al. “Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification” \<link\>

• Ioffe and Szegedy. “Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift” \<link\>

Other useful resources

• Neural networks:

• Tensorflow Playground

• Optimisation:

• https://distill.pub/2017/momentum/

• https://ruder.io/optimizing-gradient-descent/

• https://github.com/lilipads/gradient\_descent\_viz

• Loss landscapes:

• http://www.telesens.co/loss-landscape-viz/viewer.html

• https://github.com/tomgoldstein/loss-landscape

• https://jithinjk.github.io/blog/nn\_loss\_visualized.md.html

• Weight initialisation:

• https://www.deeplearning.ai/ai-notes/initialization/index.html

<https://theaisummer.com/normalization/>   
<https://theaisummer.com/normalization/>   
<https://theaisummer.com/normalization/>   
<https://www.deeplearningbook.org/contents/optimization.html>   
<https://arxiv.org/pdf/1609.04747.pdf>   
<https://link.springer.com/chapter/10.1007/978-3-642-35289-8_3>   
<https://arxiv.org/abs/1502.01852>   
<https://arxiv.org/abs/1502.03167>   
<https://playground.tensorflow.org/>   
<https://playground.tensorflow.org/>   
<https://playground.tensorflow.org/>   
<https://distill.pub/2017/momentum/>   
<https://distill.pub/2017/momentum/>   
<https://ruder.io/optimizing-gradient-descent/>   
<https://ruder.io/optimizing-gradient-descent/>   
<https://ruder.io/optimizing-gradient-descent/>   
<https://ruder.io/optimizing-gradient-descent/>   
<https://ruder.io/optimizing-gradient-descent/>   
<https://ruder.io/optimizing-gradient-descent/>   
<https://github.com/lilipads/gradient_descent_viz>  
