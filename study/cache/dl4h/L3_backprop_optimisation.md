# DL4H — L3: Backpropagation & Optimisation
> Source: Google Drive file 1NYqi_03nbyZ6JBFtDyJ_8eDdX8XP6o4y · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L3\_backprop\_optimisation 

Deep Learning in Healthcare Training Neural Networks: Backpropagation & Optimisation

Ana Namburete Department of Computer Science University of Oxford

Backpropagation

ℒ(ð½)

ð¥\! ð¥" ð¥\#

Algorithm: Gradient descent with backpropagation

\!ð¦\!

ð¥$

Notation for Backpropagation

ð\[\#%'\] ð\[\#%&\] ð\[\#\] \!ð¦\! ð¤\[\#%'\]

ð¤\[\#%&\] ð¤\[\#\]

ℒ ð¾ NB: These are indices, not exponents.

ℒ ð½ ℒ ð¤\["\],ð\["\],ð¤\["$%\],ð\["$%\],ð¤\["$&\],ð\["$&\]

ðð\[\#%'\]

ð\[\#%&\] \[\#\] \!ð¦\!

ℒ ð½

ℒ ð¤\["\],ð\["\],ð¤\["$%\],ð\["$%\],ð¤\["$&\],ð\["$&\] ð¤\[\#%'\]

ð¤\[\#%&\] ð¤\[\#\]

How does a small change in the parameters (e.g. ð¤\[&\]) affect the final loss ℒ ð ?

ℒ ð¾

Loss for a single sample

• The loss of this simple network is

ℒ' … = ℎ\["\] −ð¦ & ð¤\[\#\]

ℎ\[\#\] ℎ\[\#%&\]

NB: Indexing the loss value for this single input as ‘0’

ℒ ð¾

ℎ\[&\] = 'ð¦

Activations and pre-activations

• Index network each accordingly: node in the ð¤\[\#\] ℎ\[&\],ℎ\[&(\!\],ℎ\[&("\],…

ℎ\[\#%&\] ℎ\[\#\] =ð ð\[\#\] ð\[\#%&\]

ð\[\#\] • Recall given as:

node that the ð\[&\] activation is calculated for a ℎ\[&\] =ð ð¤\[&\]ℎ\[&(\!\] + ð\[&\]

\=ð ð\[&\]

ℒ ð¾

Dependencies in the network

• Important to bear in mind the relationships between these variables: ℒ( ð¾ ℎ\[&\] =ð ð¤\[&\]ℎ\[&(\!\] + ð\[&\]

ð¦\!

\=ð ð\[&\]

ℒ(

ℎ\[\#\]

Prediction

ð¦ Ground truth ℎ\[\#%&\]

ð¤\[\#\] ℎ\[\#%&\] ð\[\#\] ℎ\[\#\]

ð\[\#\]

ð¤\[\#\]

ð\[\#\]

ð\[\#\]

How does a small change in ð¤\[&\] affect the final loss ℒ ð ?

ðℒ\! ðð¤\[\#\] = ?

ðð¤\[&\]

ℒ( ðℒ)

ðℎ\[&\]

Prediction

ℎ\[\#\]

ð¦ Ground truth ðð\[&\]

ð\[\#\]

ð¤\[\#\] ℎ\[\#%&\] ð\[\#\]

How does a small change in ð¤\[&\] affect the final loss ℒ ð ?

ℒ(

ðℒ\! ðð¤\[\#\] = ðℒ\!

ðℎ\[\#\] ⋅ ðððℎ\[\#\]

\[\#\] ⋅ ðð¤ðð\[\#\] \[\#\]

ð¦

ð¤\[\#\] ℎ\[\#%&\] ð\[\#\] tracking influence through the network

ℎ\[\#\]

ð\[\#\]

Using the chain rule

Computing the derivatives

• Loss function: ℒ' … = ℎ\["\] −ð¦ & ðℒ( ðð¤\[\#\] = ðℒ(

ðℎ\[\#\] ⋅ ðℎ\[\#\]

ðð\[\#\] ⋅ ðð\[\#\] ðð¤\[\#\]

ðℒ) ðℎ\[&\] =2 ℎ\[&\] − ð¦ Its value is linearly proportional to the difference

between the predicted and target values

Computing the derivatives

ðℒ( ðð¤\[\#\] = ðℒ(

ðℎ\[\#\] ⋅ ðℎðð\[\#\]

\[\#\] ⋅ ðð¤ðð\[\#\] \[\#\]

• Activation ℎ\["\](…)=ð values: ð\["\]

ðððℎ\[&\]

\[&\] = ð′ ð\[&\] This is just the derivative of the

activation function, evaluated at ð\["\]

Derivative of the activation function

ðℒ( ðð¤\[\#\] = ðℒ(

ðℎ\[\#\] ⋅ ðℎðð\[\#\]

\[\#\] ⋅ ðð¤ðð\[\#\] \[\#\]

• ðPre-activation \["\] … =ð¤\["\] values: ⋅ ℎ\["$%\] + ð\["\]

ðð¤ðð\[&\]

\[&\] = ℎ\[&(\!\] In this case, the effect of a change in ð¤\["\] is

highly dependent on how strong the activation of the previous layer (ℎ\["$%\]) is

\*This now relates to Hebbian Theory: “neurons that wire together, fire together”

Gradient with respect to a weight

ð¤\[\#\]

ℎ\[\#%&\] ℎ\[\#\] The sensitivity of the loss to a change in this weight is:

ð(ð¤ðℒ)(ð½)

\[&\]) =2 ℎ\[&\] −ð¦ ⋅ð\* ð\[&\] ⋅ ℎ\[&(\!\]

ℒ ð½

Gradient with respect to a bias

ð\[\#\] ðℒ(

ðð\[\#\] = ðℒ(

ðℎ\[\#\] ⋅ ðððℎ\[\#\]

\[\#\] ⋅ ðððð\[\#\] \[\#\]

ℎ\[\#%&\]

ℎ\[\#\] Pre-activation ð\[\#\] … =ð¤values:

\[\#\] ⋅ ℎ\[\#%&\] + ð\[\#\] So, it follows that: ()(\*\["\] \["\]

\= 1

The sensitivity of the loss to a change in this bias is:

ðℒðð)\[&\] (ð½)

\=2 ℎ\[&\] −ð¦ ⋅ð\* ð\[&\] ⋅ 1

ℒ ð½

From one sample to many

ð¥\!

… ð¤\[\#\]

ℒ ð½ ℎ\[\#%&\] ℎ\[\#\] This currently considers only one input ðℒ$ example (ð¥$): ðð¤\["\]

The loss for derivative all ð examples:

of the full loss function ðℒ

ðð¤\["\] is an average = ð1,%&'( ðℒ%

ðð¤\["\]

over evaluating the

Gradient vector

ð¥\!

ð¤\[&\]

… ð¤\[\#%&\]

ð¤\[\#\] ℒ ð½ • The network has 2ð¿ weights and biases

ð»ℒ =

ðℒ ðð¤\['\] ðℒ ðð.\['\] ..Gradient ðℒ

• The value of

ðð¤ðℒ

\["\] = ð1)$%&' ðℒ$

ðð¤\["\]

is just one component of the gradient vector vector

ðð¤\["\] ðℒ

• Gradient vector: ðð\["\]

• Composed of the partial derivatives of the loss function w.r.t. all the weights and biases

Gradients w.r.t. previous activations

• Quantify the impact of the ℒ(

previous activation(ℎ(&(\!)) on the loss

ℎ\[\#\]

ð¦

ðℒ( ðℎ\[\#%&\] = ðℒ(

ðℎ\[\#\] ⋅ ðððℎ\[\#\]

\[\#\] ⋅ ðℎðð\[\#%&\]

\[\#\]

ð¤\[\#\] ℎ\[\#%&\] ð\[\#\] ð\[\#\]

Pre-activation ð\[\#\] … =ð¤values:

\[\#\] ⋅ ℎ\[\#%&\] + ð\[\#\] So, in this case: (+()\["$%\] \["\]

\= ð¤\["\]

Expanding to multiple nodes

ℎ(\[\#%&\]

ð¾\[\#\]

ℎ(\[\#\]

ð¤\[\#\]

ℎ&\[\#%&\]

ℎ\[\#%&\]

ℎ\[\#\] ℎ\*\[\#%&\]

ℎ)\[\#\]

In and networks ð) keep with track multiple of the nodes individual in each nodes layer, within separate the layers

indices (ð ð: current layer ð: preceding layer

ℒ ð½

ℒ ð¾

ℎ)\[\#\]

ℎ\*\[\#%&\]

ð¤)\*\[\#\]

Loss function

ð\[\#\]

ð(\[\#\]

Note that each activation in layer (ð¿ − 1) will have an effect on all nodes in the output layer (ð¿).

So, function the effect is slightly of ℎdifferent:

\-\[&(\!\] on the loss

ð&\[\#\]

ðℒ) ðℎ-\[&(\!\] = \#=./)

\!"\# ðℎðℒ.\[&\] )

⋅ ðððℎ..\[&\]

\[&\] ⋅ ðℎðð-\[&(\!\] .\[&\]

It’s a sum over its effect on all ð&(\! nodes in the \[ð¿ − 1\]’th layer

Optimisation Algorithms

Parameters

• Parameters:

• internal estimated learn the to mapping the from model, the between data can during be input independently training, and output as the changed labels

algorithm or tries to Neural Network

• Weights • Biases

Input, ð¥ Output, ð¦

Hyperparameters

• Hyperparameters: control knobs for training neural networks

• Loss function

• Optimisation algorithm

• incl. choice of learning rate

• Activation function

• Number of hidden layers

• Number of iterations/epochs

• Batch size

• Train-test data split ratio

Parameters are internal to the model Weights and biases

Gradient Descent Update Rule

• The goal is to efficiently and reliably minimise the loss function argminð½ ℒ(ð½; ð, ð) where the loss is a function of the weights

The gradient descent update rule was to move in the direction opposite to the gradient: Learning rate

ð¤ð+,& +,& = = ð¤ð+ + − − ðð»ððð»ð¤+ + where ð»)&ℒ = \*ℒ(),.)

\*) │at ð¤%)&, .%.& and ð».&ℒ = \*ℒ(),.)

\*. │at ð¤%)&, .%.&

Figure credit

Gradient Descent Update Rule

ð¤01\! = ð¤0 − ðð»ð¤0 • At the initial location ðℒ

: ðð¤) ℒ ð¤( ð01\! = ð0 − ðð»ð0

1ðℒ Learning rate is fixed\!

ðð¤\!

2 = ððððð¡ðð£ð ððððð¡ðð£ð 1

(−) (−)

3

• So, step location

to in move a negative 2 in the opposite ð¤) direction direction, to reach must • Note: step size is fixed because ð is a constant

ð¤(

Gradient Descent Update Rule

ð¤01\! = ð¤0 − ðð»ð¤0 ℒ ð¤( ð01\! = ð0 − ðð»ð0

1ðℒ

ðð¤\!

2

3

• Epoch: one full iteration over the training dataset

ð¤(

Algorithm source

Pitfalls of Vanilla Gradient Descent

• High-dimensional loss functions are highly non-convex

• Risk of getting trapped in suboptimal local minima

Pitfalls of Vanilla Gradient Descent

• High-dimensional loss functions are highly non-convex

• Risk of getting trapped in suboptimal local minima

• High sensitivity to the weight initialisation point

Pitfalls of Vanilla Gradient Descent

• High-dimensional loss functions are highly non-convex

• Risk of getting trapped in suboptimal local minima

• High sensitivity to the weight initialisation point

• Saddle points and plateaus

• Points on loss landscape where the gradient is highly non- spherical

• Regions of small weight updates

• Risk of divergence

Gradient vector:

Gradient (Jacobian):

• first-order information Stacked vector of derivatives w.r.t. all parameters Tells us which way is downhill

Beyond gradients: Curvature matters

Gradient vector:

Gradient (Jacobian):

• first-order information Stacked vector of derivatives w.r.t. all parameters Tells us which way is downhill

Beyond gradients: Curvature matters

Matrix of second derivatives of the stacked gradient Diagonal blocks: curvature within parameters / layers Off-diagonal blocks: coupling between parameters / layers Same gradient ≠ same optimisation behaviour

The Hessian is the Jacobian of the gradient vectorwhere

Beyond gradients: Curvature matters

• Gradient descent only sees slope

• Gradient: first-order information

• Ignores curvature of the loss

• Same gradient ≠ same behaviour

• The Hessian of the lossð¯ð = ∇2"ℒ(ð)

ℒ ð+Δ ≈ ℒ ð + ∇ℒ3Δ + 12∆3ð¯∆

Depends on

gradient Depends on Hessian;

captures curvature

Eigenvalues and conditioning

• Hessian eigenvalues = curvature

• Large eigenvalue → steep direction

• Small eigenvalue → flat direction

• Condition number:

ð = ð456 ð4$\#

Figure source

Saddle points and plateaus

• High-dimensional reality

• Most critical points are saddle points

• Gradient ≈ 0

• Hessian has ± eigenvalues

Figure credit Gradient descent variants

Vanilla gradient descent

\+ Momentum Adam RMSprop Adagrad

• Momentum

• Accumulated gradients over time

• Suppresses oscillations

• Accelerates directions

along consistent

• Borrows the idea from physics

• Ball rolling inside a frictionless bowl

• Momentum accumulates

• Ball picks up speed

Intuition: GD with Momentum

Figure credits: \[1\], \[2\]

GD with Momentum

• With momentum:

Gradient at ð¤01\! = ð¤0 − ðð»ð¤0

• Without momentum:

current location

ð¤01\! = ð¤0 − ðð»ð¤0 + ð½ ⋅ update0(\!

Extra term on top of GD

0≤ð½\<1

Keeps track of the history of updates

Figure credit

GD with Momentum

• With momentum: ð¤01\! = ð¤0 − ðð»ð¤0 + ð½ ⋅ update0(\!

0≤ð½\<1

ð¡ = 0: update2 = 0 ð¡ = 1: update& =ð½⋅ update2 + ðð»ð¤& = ðð»ð¤& ð¡ = 2: update3 =ð½⋅ update& + ðð»ð¤3 = ð½ðð»ð¤& + ðð»ð¤3 ð¡ = 3: update4 =ð½⋅ update3 + ðð»ð¤4 = ð½3ðð»ð¤& + ð½ðð»ð¤3 + ðð»ð¤4 ð¡ = 4: update5 =ð½⋅ update4 + ðð»ð¤5 = ð½4ðð»ð¤& + ð½3ðð»ð¤3 + ð½ðð»ð¤4 + ðð»ð¤5

⋮ ⋮ ð¡ = ð¡: update6 =ð½⋅ update67& + ðð»ð¤6 = ð½67&ðð»ð¤& + ð½673ðð»ð¤3 + ⋯ + ðð»ð¤6

GD with Momentum

Negative sign

• With momentum: ð¤01\! = ð¤0 − ðð»ð¤0 + ð½ ⋅ update0(\!

0≤ð½\<1

ð¡ = 0: update2 = 0 ð¡ = 1: update& =ð½⋅ update2 + ðð»ð¤& = ðð»ð¤& ð¡ = 2: update3 =ð½⋅ update& + ðð»ð¤3 = ð½ðð»ð¤& + ðð»ð¤3 ð¡ = 3: update4 =ð½⋅ update3 + ðð»ð¤4 = ð½3ðð»ð¤& + ð½ðð»ð¤3 + ðð»ð¤4 ð¡ = 4: update5 =ð½⋅ update4 + ðð»ð¤5 = ð½4ðð»ð¤& + ð½3ðð»ð¤3 + ð½ðð»ð¤4 + ðð»ð¤5

⋮ ⋮ ð¡ = ð¡: update6 =ð½⋅ update67& + ðð»ð¤6 = ð½67&ðð»ð¤& + ð½673ðð»ð¤3 + ⋯ + ðð»ð¤6

GD with Momentum

Negative sign

• With momentum: ð¤01\! = ð¤0 − ðð»ð¤0 + ð½ ⋅ update0(\!

0≤ð½\<1

ð¡ = 0: update2 = 0 ð¡ = 1: update& =ð½⋅ update2 + ðð»ð¤& = ðð»ð¤& ð¡ = 2: update3 =ð½⋅ update& + ðð»ð¤3 = ð½ðð»ð¤& + ðð»ð¤3 ð¡ = 3: update4 =ð½⋅ update3 + ðð»ð¤4 = ð½3ðð»ð¤& + ð½ðð»ð¤3 + ðð»ð¤4 ð¡ = 4: update5 =ð½⋅ update4 + ðð»ð¤5 = ð½4ðð»ð¤& + ð½3ðð»ð¤3 + ð½ðð»ð¤4 + ðð»ð¤5

⋮ ⋮ ð¡ = ð¡: update6 =ð½⋅ update67& + ðð»ð¤6 = ð½67&ðð»ð¤& + ð½673ðð»ð¤3 + ⋯ + ðð»ð¤6

GD with Momentum

Negative sign

• With momentum: ð¤01\! = ð¤0 − ðð»ð¤0 + ð½ ⋅ update0(\!

0≤ð½\<1

ð¡ = 0: update2 = 0

Exponentially ð¡ = 1: update& =ð½⋅ update2 + ðð»ð¤& = ðð»ð¤& ð¡ = 2: update3 =ð½⋅ update& + ðð»ð¤3 = ð½ðð»ð¤& + ðð»ð¤3

weighted average

⋮ ⋮ ð¡ = ð¡: update6 =ð½⋅ update67& + ðð»ð¤6 = ð½67&ðð»ð¤& + ð½673ðð»ð¤3 + ⋯ + ðð»ð¤6

Figure credit

Limitations of Momentum

• Pros:

• Faster convergence

• Ability to escape local minima and plateaus

• Oscillates in and out of local minima because the momentum is able to propel it out

• Limitations:

• “Ball” rolling down blindly gradient descent momentum

Nesterov Accelerated Gradient (NAG)

• Intuition: “look before you leap\!”

• Recall momentum-based update rule:

ð¤01\! = ð¤0 − ðð»ð¤0 + ð½ ⋅ update0(\!

• NAG: two-step computation

• Instead of computing the gradient at the current point, compute it at what would be the next point

ð¤788-\_5:;5\< = ð¤0 − ð½ ⋅ update0(\! ð¤01\! = ð¤0 − ðð»ð¤788-\_5:;5\< + ð½ ⋅ update0(\!

\* We follow similar rules for ð"\#$

Momentum Nesterov

ðℒ ðð¤% ℒ

ð¤(

\= ððððð¡ðð£ð ððð ðð¡ðð£ð (+) (−)

ℒ

1

1

2

2

3

3

ð¤(

ðℒ ðð¤% = ððððð¡ðð£ð ððððð¡ðð£ð (−) (−)

Path taken

Momentum Nesterov

ðℒ ðð¤% ℒ

ð¤(

\= ððððð¡ðð£ð ððð ðð¡ðð£ð (+) (−)

ℒ

1

1

2

2

3 4

3 4a

5

4

4b

6

5ð¤(

ð¤'(()\_+,-+.

ðℒ ðð¤% = ððððð¡ðð£ð ððððð¡ðð£ð (−) (−)

Path taken

Slide credit: Vineeth Balasubramanian

Batch Gradient Descent

• For every parameter update, gradient descent parses the entire dataset

• Hence called Batch Gradient Descent

• Advantages:

• Conditions of convergence are well-understood

• Several acceleration techniques designed to operate in the batch GD setting

• Disadvantages:

• Computationally slow

Stochastic Gradient Descent

• Randomly shuffle the training set, and update parameters after gradients are computed for each training sample

Slide credit: Vineeth Balasubramanian

Mini-Batch Stochastic Gradient Descent

• Update parameters after gradients are computed for a randomly drawn mini-batch of training samples

Slide credit: Vineeth Balasubramanian

Note: Default option used today. Often referred to as SGD

Stochastic GD

High noise Unstable near optimum

Batch size affects optimisation, normalisation, and generalisation

Practical constraint in healthcare:

• Batch size often limited by memory.

• Large 3D images → very small batch sizes (sometimes 1)

Figure credit Effect of Batch Size

Batch Mini-Batch GD GD Trade-off between Low noise noise and efficiency

Slow updates

Further Reading

• Textbooks:

• Goodfellow et al. Deep Learning: Chapter 8 (Sec. 8.7)

• Articles:

• Ruder et al. Review of gradient descent algorithms \<link\>

• LeCun et al. “Efficient BackProp” \<link\>

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

<https://towardsdatascience.com/a-visual-explanation-of-gradient-descent-methods-momentum-adagrad-rmsprop-adam-f898b102325c>   
<http://www.brnt.eu/phd/img169.png>   
<https://agustinus.kristia.de/blog/hessian-curvatures/>   
<https://towardsdatascience.com/a-visual-explanation-of-gradient-descent-methods-momentum-adagrad-rmsprop-adam
