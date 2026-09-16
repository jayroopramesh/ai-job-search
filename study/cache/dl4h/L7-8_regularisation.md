# DL4H — L7-8: Uncertainty & Regularisation
> Source: Google Drive file 1Y6NwSCeWLyGqpiZsZSJ5bDV-EOWfhvs3 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L7-8\_regularisation 

Deep Learning in Healthcare

Uncertainty and Regularisation

Ana Namburete Department of Computer Science University of Oxford

Regularisation, uncertainty, and trustworthy predictions

What does the model predict? How confident should we be?

• Roadmap:

• Why confidence matters (especially in healthcare)

• Two kinds of uncertainty

• How regularisation shapes uncertainty

• Early stopping

• Weight decay

• SGD bias

• Approximating uncertainty in practice

• Limits & failure modes

Example: Chest X-ray (lung opacities)

Model output:

• Prediction: “No pathology”

• Confidence: 99%

•

When confidence is the problem

• High confidence ≠ correctness

• Confidence failures are dangerous (especially in healthcare)

✅

Ground-truth:

• “Pathology present”

•

❌

What is uncertainty?

• Imperfect or incomplete information

• Uncertainty: dispersion of a random variable

• Distributions, not just point estimates

Two sources of uncertainty

Aleatoric

Epistemic

Uncertainty in the data Natural variation

Scenario uncertainty

Inherent randomness

Parametric uncertainty

Data uncertainty

Environmental stochasticity

Measurement error

Measurement uncertainty

Process stochasticity

Process error

Sampling uncertainty

Demographic stochasticityModel uncertainty

Uncertainty in the model

Early Stopping as Implicit Regularisation

Which optimiser should I use?

How does this technique constrain optimisation, and which solutions does it rule out?

Early Stopping

r orrETraining error

Epochs

• Track validation error

• Stop after no improvement for ð epochs (‘patience Validation error

parameter’)

• Return model at ð−ð

ð−ð ð

return this

stop model

This allows you to stop training early before the ð¡ðððð\!"" goes to 0, and ð£ðð\!"" blows up

Mechanics of Early Stopping r orrETraining error

Epochs

Recall the update rule in SGD ð¤\!"\# = ð¤\! − ð∇ð¤\!

\!

Validation error

\= ð¤\! −ð&∇ð¤$ $%\#Let ð be the maximum value of all ð−ð ðprevious gradients, then return

stop this model

ð¤\!"\# ≤ ð¤& − ðð¡ð

ð¡ controls how far ð¤\# can go from the initial ð¤$ ∴ it controls the space of exploration

Weight decay

From early stopping to weight decay

Early stopping Weight decay

• Limits number of • Modifies the objective optimisation steps

function

• Constrains how far • Penalises larger parameter parameters move from norms initialisation

• Explicit constraint on • Implicit constraint on parameter space

parameter space

Both restrict accessible solutions, but by different mechanisms. Early stopping constrains optimisation in time. Weight decay constrains optimisation in space.

L2-Regularisation

• The ð¿'-weight penalty decay on the (or ð¿'simply -norm weight of the parameters decay) is known as • Modified loss function is defined ,ℒ ð¤ = ℒ ð¤ + by:

2 ðð¤ '

Original loss

Regularisation term

L2-Regularisation

• The ð¿'-weight penalty decay on the (or ð¿'simply -norm weight of the parameters decay) is known as • New loss function is defined ,ℒ ð¤ = ℒ ð¤ by:

\+ 2 ðð¤ '

Loss gradient:

∇ ,ℒ ð¤ =∇ℒ ð¤ +ðð¤

GD update ð¤\!"\# = rule:

ð¤\! − ð∇ ℒ ,ð¤\! = ð¤\! −ð ∇ℒ ð¤\! + ðð¤\! = 1−ððð¤\! − ð∇ℒ ð¤\!

\* Theoretically equivalent to early stopping

Closer to zero

Ensembling

Model Ensembling

• The classifiers solve idea a problem behind with a common model ensembling objective and is to take fuse them a set of together ð to • By generalisation combining the output error may be of different reduced models, the ð¦%ð¦&ð¦' The can either be: - different classifiers, or - different instances of the same classifier (ensembling)

The classifiers in the ensemble can be trained with:

ð¦()\*+,

\- Different hyperparameters - Different features - Different samples of training data

Training data: Sampling with replacement

ð·%ð·&ð·'

Each model is trained with a different subsample of the full training dataset

ð¦%ð¦&ð¦'

Bagging

• Bagging forms an ensemble with different instances of the same classifier

ð¦()\*+,

• From a given dataset, construct multiple training sets sampling (ð·\#,ð·',…,ð·() by with replacement • Train the ð\!) instance of the classifier with training set ð·$

When is bagging effective?

ððð¸\*+,\*-./\* = ð 1ð + ð−1

ð ð¶

Variance termScenario \#1

Correlation term

• Perfectly correlated models

• All models make the same errors

• ð=ð¶ ⟹ MSE01203450 = ð

• No benefit from bagging

When is bagging effective?

ððð¸\*+,\*-./\* = ð 1ð + ð−1

ð ð¶

Variance termScenario \#2

Correlation term

• Uncorrelated model errors

• Errors are independent ⟹ð¶=0

• MSE01203450 = 76ð

• Variance shrinks with ensemble size

Dropout: implicit ensembling with shared parameters

Limitations of Ensembling

• Ensembling reduces variance if models are decorrelated

• Training many large neural networks is computationally infeasible

• Dropout approximates ensembling within a single network

Option \#1 Option \#2

Train several ð¦%models, each with different architectures

ð¦&ð¦'

Train multiple ð¦%instances of the same model,

ð¦()\*+,

using different ð¦\&training samples

ð¦()\*+,

Clearly expensive\! Also expensive\!

ð¦'

With either option, combining several models at test time is infeasible in real-time applications

Image credit: Mitesh Khapra Dropout

• Randomly drop units during training

• Each forward pass samples a different subnetwork

• Parameters are shared across subnetworks

Standard network With dropout

Effectively allows us to train several NNs without any significant computational overhead

Dropout: training an exponential ensemble implicitly

• Suppose a network has a total of ð nodes

• With dropout, each node can be retained or dropped

• Total number of ‘thinned’ networks that can be formed using dropout: 2+ -- too many to train\!

• Shared weights trick:

• All subnetworks that include a unit share its parameters

In this example, 5 nodes have been dropped to thin the network

Image credit: Mitesh Khapra

Dropout

ð¦6

ð¦=

ð¾\[/\]

ð 896 \~ Bernoulli ð

ð¾\[/1%\] b\["\#$\]

ð:ð¦:

8 = ð¾:8 ð 896 ⨀ ð 896 + ð:8

ð¥0

1 0 1 ð 896 , ð = 0.6

Neural network with dropout

b\["\]

Feedforward equations:

Acts as a mask ℎ% ð%% ℎ& ð%& ðℎ%- -

8 =ð ð:8

Element-wise

ð¥\# ð¥'

with

multiplication

ð: dropout probability ð: sampling distribution

Why BatchNorm and Dropout can interfere

• BatchNorm assumes stable activation statistics at test time

• Dropout injects stochastic variance during training

• This creates a train-test variance mismatch

• Effect is most severe in bottlenecked CNNs

• Layer ordering can mitigate the problem

Take-home: BatchNorm + Dropout is not “wrong”, but it must be used carefully. It is often unnecessary in modern CNNs.

Li, Xiang, et al. Understanding the disharmony between dropout and batch normalization by variance shift. CVPR 2019 (https://arxiv.org/abs/1801.05134)

Dropout for CNNs

Without dropout Spatial dropout Standard dropout Cutout dropout

For CNNs in medical imaging, prefer spatially structured dropout (feature maps or regions) over pixel-wise dropout to avoid brittle, over-confident representations.

Augmentation

Data augmentation as implicit regularisation

• Expands the effective training distribution

• Enforces invariances

• Constrains the learned function class

Acts through the data, not the loss

Garcea et al, CBM 2023

What does augmentation do?

• Many inputs, same label

• Fewer admissible solutions

Garcea et al, CBM 2023

❌ Does not remove aleatoric uncertainty Noise inherent in the data (e.g., sensor noise, ambiguous boundaries) remains, even with infinite augmentation

❌ Does not make invalid assumptions safe Augmentation encodes domain assumptions. Incorrect transformations introduce implausible samples.

❌ Does not detect distribution shift Models can be confidently wrong on out-of-distribution inputs, even with extensive augmentation

What augmentation does not do

\>ð¦223 ð¥ = ð 1C)4%5

ð6 ð)(ð¥) , ð)\~ð(ð)

Random transformation (e.g., rotation, flip, crop)

Var223 ð¥ Uncertainty due to

\= ð 1C)4%5

ð6 ð) ð¥ − \>ð¦223 ð¥

variance violations

Samples over inputs, not models

&

• Apply inference augmentations at • Measure prediction variability

• Samples over inputs, not parameters

Test-Time Augmentation (TTA)

• One component of epistemic uncertainty

• Arises from invariance violations

• Complementary to dropout and ensembles

• NOT a general OOD detector

Samples over inputs, not models

TTA and Uncertainty

Aleatoric Uncertainty

Aleatoric uncertainty refers to uncertainty arising from the inherent stochasticity of the true data generating process. This uncertainty cannot be reduced with more data.

• Inherent noise or ambiguity

• Measurement limitations

• Persists even with infinite data

Homoscedastic vs. heteroscedastic

Assumptions about the data generating process can help in distinguishing between different types of aleatoric uncertainty:

• Not all data uncertainty is uniform

• Homoscedastic: constant noise across the input space

• Heteroscedastic: space

input-dependent noise; varies across the input

Why point predictions are not enough

Point estimates hide uncertainty

\>ð¦=ð1 ð¥ ð£ð . ð ð¦ ð¥,ð)

• Standard training → point estimates

• Point estimates assume determinism

• Many tasks are intrinsically ambiguous

• Deployment requires a distribution

Modelling aleatoric uncertainty

ð ð¦ ð¥) = ð© ð ð¥ ,ð\! ð¥

Example: Regression loss ℒ ð¥,ð¦ = ð¦−ð ð¥ 2ð\! ð¥ • Mean and variance are learned

• Variance represents data noise

\!

\+ 12log ð\! ð¥

This uncertainty is about the data, not the model

Epistemic Uncertainty

Epistemic uncertainty accounts for uncertainty in the model or in its parameters. It captures our ignorance about which model can best explain the collected data. It can be reduced given enough data.

• Uncertainty about the model

• Limited data

• Under-constrained solutions

• Shaped by optimisation and architecture

Where regularisation matters\!

Bayesian Predictive Distribution

• Marginalise over parameters

• Infinite ensemble in principle

• Intractable for deep networks

Epistemic

ð ð¦ ð¥,ð) = 4ð ð¦ ð¥,ð) ð ð ð) ðð

Aleatoric

Two sources of predictive uncertainty

Var ð¦ ð¥,ð) = ð¼" Var ð¦ ð¥,ð) +Var" ð¼ ð¦ | ð¥, ð

Aleatoric Epistemic

Variance Decomposition

Model Calibration

Well calibrated (bars close to diagonal)

• A calibrated ≈ Overconfident (bars below diagonal)

model confidence is well- if accuracy y caruccal aciripmEExpected Error (ECE):

Calibration weighted between accuracy confidence average gap and Guo et al. (2017), "On Calibration of Modern Neural Networks” Perfect calibration

Predicted confidence

Each bar: accuracy of predictions within a confidence bin. Diagonal: perfect calibration.

Input distribution

e gdelwonkl edoMIn-distribution (ID) Out-of-distribution (OOD) Well-specified

Misspecified

Why uncertainty is hard

✅ Uncertainty is meaningful

(aleatoric + epistemic apply)

⚠ Overconfidence despite good data

(Inductive bias failure)

⚠ Epistemic uncertainty may increase

(some methods catch this)

❌ Predictive distribution meaningless

(Not “uncertainty”; model failure)

Input distribution

e gdelwonkl edoMIn-distribution (ID) Out-of-distribution (OOD) Well-specified

Misspecified

Why uncertainty is hard

✅ Uncertainty is meaningful

(aleatoric + epistemic apply)

⚠ Overconfidence despite good data

(Inductive bias failure)

⚠ Epistemic uncertainty may increase

(some methods catch this)

❌ Predictive distribution meaningless

(Not “uncertainty”; model failure)

Input distribution

e gdelwonkl edoMIn-distribution (ID) Out-of-distribution (OOD) Well-specified

Misspecified

Why uncertainty is hard

✅ Uncertainty is meaningful

(aleatoric + epistemic apply)

⚠ Overconfidence despite good data

(Inductive bias failure)

⚠ Epistemic uncertainty may increase

(some methods catch this)

❌ Predictive distribution meaningless

(Not “uncertainty”; model failure)

Input distribution

e gdelwonkl edoMIn-distribution (ID) Out-of-distribution (OOD) Well-specified

Misspecified

OOD ≠ epistemic uncertainty

Why uncertainty is hard

✅ Uncertainty is meaningful

(aleatoric + epistemic apply)

⚠ Overconfidence despite good data

(Inductive bias failure)

⚠ Epistemic uncertainty may increase

(some methods catch this)

❌ Predictive distribution meaningless

(Not “uncertainty”; model failure)

Gal and Ghahramani, "Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning." ICML, 2016

Dropout as approximate Bayesian inference

• Random subnetworks at training time

• Parameter sharing across models

• Dropout defines a distribution over subnetworks

• Monte-Carlo dropout ≈ posterior sampling

• Keep dropout active at test time

• Run ð stochastic forward passes

• Compute mean and variance

Monte Carlo Dropout

Dropout for Uncertainty Estimation

Mean prediction: - Average over ð passes

Red regions: - High predictive variance

Epistemic uncertainty appears near ambiguous or unstable regions.

What regularisation really controls

Training loss

high low

Model bias Optimisation

issue

Test loss

high low

Increase model complexitySuccess\! Strengthen the optimiser

Overfitting Covariate shift

Trade-off

Add more training data

Batch normalisation Data augmentation Simplify the model

Domain adaptation Dropout

Credit: Hung-yi Lee

Uncertainty Estimation: Quality vs Cost

Method Training Cost Inference Cost Memory

Deep Ensemble (ð models) ð × single model ð forward passes ð × model

MC Dropout (ð passes) 1 × single model ð forward passes 1 × model

Test-Time Augmentation (ð¾ augmented inputs) 1 × single model ð¾ forward passes 1 × model

\* MC Dropout: lowest training cost, minimal memory overhead

Deep ensembles give the best uncertainty quality. MC Dropout gives the best cost-quality trade-off.

Regularisation shapes uncertainty

• Regularisation shapes epistemic uncertainty

Early stopping Limits exploration

L2 regularisation Implicit Gaussian prior

SGD Favours flat minima

Architectures Constrains function space

References

• Textbooks:

• Goodfellow et al. Deep Learning: Chapter 7

• Sections 7.1-7.5; 7.8; 7.12

• Hinton et al., “ Improving neural networks by preventing co-adaptation of feature detectors.” CoRR, 2012

• Baldi and Sadowski, “The dropout learning algorithm.” Artificial Intelligence, 2014

• Srivastava et al, “Dropout: A simple way to prevent neural networks from overfitting.” Journal of Machine Learning Research, 2014

• Gal and Ghahramani, "Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning." ICML, 2016

• Lakshminarayanan et al., "Simple and Scalable Predictive Uncertainty Estimation using Deep Ensembles." NeurIPS, 2017

Appendix

Bagging

• Suppose we have a set of ð classifiers

• We sample can assume that each classifier makes an error ð: on a given test • For distribution simplicity, let ð: be drawn from a zero-mean multivariate normal ðð ð = ð¼ ð 1C)ð) &

Variance = ð¼ ð)& = ð The expected mean squared

Covariance = ð¼ ð)ð7 = ð¶ error (MSE) is:

\= ð1& ð¼ C)

ð% + ð& + …+ð' &

The average error made by all models for the given test sample is: 1ð C)ð)

ð)ð7

\= ð1& ð¼ C)

Cð)ð7 + CC)47

)

)87

ð)& + C)

ð)ð7

\= ð1& C)

C)87

ð¼ ð)& + C)

Linearity of expectation: ð¼ ð + ð = ð¼\[ð\] + ð¼\[ð\] ð¼ ð)ð7

\= = ð1ð 1& ð + ðð+ð ð−1

ð ð−1 ð¶

C)87

ð¶

Credit: Vineeth Balasubraramian

Dropout at ‘test time’

ð¦6

ð¦=

ðð¾\[/\]

b\["\#$\]

ð¥\# ð¥'

ð¥0

Neural network without dropout at test time

b\["\]

Feedforward equations:

ℎ% ð%% ℎ& ð%& ðℎ%- -

ð:8 = ðð¾:8 ð 896 + ð:where

ð: dropout probability in training

8

ð¦:

8 =ð ð:8 ðð¾\[/1%\]
