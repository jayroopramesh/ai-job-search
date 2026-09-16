# DL4H — L16: Explainability & Trust
> Source: Google Drive file 1WTjc7Do5PiKBO0GcqVS02Byf788IzIRu · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L16\_explainability 

Deep Learning in Healthcare

Explainability and Trust

Ana Namburete Department of Computer Science University of Oxford

Case Study: COVID-19

ICU patient outcome prediction

Hospital worklist triaging

Ranking of clinical variables for predicting patient mortality

Goncharov et al, CT-based COVID-19 triage. Med Imag Anal, 2021 Chao et al, Integrative analysis for COVID-19 patient outcome prediction. Med Imag Anal, 2021

Tasks chosen for convenience, not clinical utility

Labels were easy to obtain, but weak proxies for clinical severity.

Imaging used in isolation, ignoring multimodal context

High performance on a convenient task ≠ real-world usefulness

Not fit for deployment

Spurious Correlations: Hospital Markers

Models relied on hospital-specific laterality markers rather than lung pathology.

DeGrave et al, AI for radiographic COVID-19 detection selects shortcuts over signal. Nature Mach Intell, 2021

Image credit Projection Bias (AP vs PA)

(same patient)

Roberts et al, Common pitfalls and recommendations for using machine learning to detect and prognosticate for COIV-19 using chest radiography and CT scans. Nature Mach Intell, 2021

Severe COVID patients: supine in AP projection

Healthy patients: Upright in PA projection

Anterior-Posterior (AP) projection Posterior-Anterior (PA) projection

Why explainability?

Why do we need explainability?

• Correct ≠ Intelligent

• Incorrect medical diagnoses have serious implications

• Need to ensure the model does not encode hidden biases

• If model behaves abnormally, we need to be able to explain why

Explainability vs. Interpretability

• Terms are often used interchangeably, but they have slightly different meanings

• Explainable: capable of justifying its decision

• Interpretable: transparent model

Image credit

Vs.

Classifier

There is a lesion in this liver because…

e.g. Which type of contact lens to prescribe?

XAI categories

1\. Visual explanations 2. Text-based explanations 3. Example-based explanations

Why do you think this is an image of a liver?

What does a “liver” look like?

or 1. Ante-hoc 2. Post-hoc

or 1. Local explanations 2. Global explanations

Pixel Attribution Methods

Which component is most relevant?

• Which pixels are most critical for decision- making?

• We can determine this by occluding parts of the image and seeing how that changes the prediction

Zeiler and Fergus, ECCV 2014

Input ð

Image, text, etc.

Example components:

• Image: pixel, patch, etc.

• Text: a word

Components: ð\!,⋯,ð"

Which component is most relevant?

1 Occlusion Experiments • Goal: probability understand of a particular which parts class of the image are responsible for maximising the • Remove or modify image regions

• The occlusion resulting in the largest decision change is the most important component

Zeiler and Fergus, ECCV 2014

Image credit

Zeiler and Fergus, ECCV 2014

Which component is most relevant?

• Goal: understand which parts of the image are responsible for maximising the probability of a particular class

• Remove or modify image regions • The occlusion resulting in the largest decision change is the most important componentOcclusion Experiments 1

Zeiler and Fergus, ECCV 2014

Which component is most relevant?

Occlusion Experiments 1

ð¥\! ð¥\# . . .

. . . . .

. . . . .

. . . . ð¥$

Gradient as influence

• Let an ð×ð image be flattened as ð¥∈ℝ\!, where ð = ðð

• Let ð" denote the score (logit) for class ð

If a small perturbation Δð¥\! causes a large change in ð", then pixel ð¥\! has high local influence on class ð.

flatten

ð¥\!

ðð" ðð¥\!

We compute the gradient:

ðð\! ðð¥"

ðð" ðð¥$ ðð" ðð¥\#

. . .

. . . . .

. . . . .

. . . . ðð"

ðð¥%&

Pixel Attribution

• Let an ð×ð image be flattened as ð¥∈ℝ\!, where ð = ðð

• Let ð" denote the score (logit) for class ð

flatten

ð¥\!

ðð" ðð¥\!

∇\#ð\! ð¥ = ðð\!

ðð¥$ ,…, ðð\! ðð¥%

Reshape this vector → Saliency Map

Which component is most relevant?

Saliency Maps 2

Which component is most relevant?

2 Saliency Maps • Useful for sanity checking

Training accuracy: 98.6% Test set accuracy: 98.2%

Feature-Level Explanations

Global average pooling

Zhou et al. Learning deep features for discriminative localisation, CVPR 2016

Feature contributions

Uses the concept of Global Average Pooling (GAP)

Class Activation Maps (CAM)

Global average pooling

Zhou et al. Learning deep features for discriminative localisation, CVPR 2016

Feature contributions

Uses the concept of Global Average Pooling (GAP)

Class Activation Maps (CAM)

Note: The same activation maps produce different CAMs based on weights that connect features to individual classes

Zhou et al. Learning deep features for discriminative localisation, CVPR 2016

Class Activation Maps (CAM)

Top 5 predicted classes

Namazi et al. Surgical Endoscopy, 2022

Gradient-Weighted CAM (Grad-CAM)

• No longer required to drop the FC layers

• Can be applied to any general CNN

ð´)

ðð( ðð´)

Ramprasaath et al. Grad-CAM: Visual explanations from deep networks via gradient-based localisation , ICCV 2017 (https://arxiv.org/abs/1610.02391)

Gradient-Weighted CAM (Grad-CAM)

• No longer required to drop the FC layers

• Can be applied to any general CNN

ð´)

ð¼)( = GlobalAveragePooling ðð( ðð´)

ðð( ðð´)

Ramprasaath et al. Grad-CAM: Visual explanations from deep networks via gradient-based localisation , ICCV 2017 (https://arxiv.org/abs/1610.02391)

Gradient-Weighted CAM (Grad-CAM)

• No longer required to drop the FC layers

• Can be applied to any general CNN

ð´)ð¼)(

\*ð¼&\!ð´&

&

ðð( ðð´)

Ramprasaath et al. Grad-CAM: Visual explanations from deep networks via gradient-based localisation , ICCV 2017 (https://arxiv.org/abs/1610.02391)

Guided Grad-CAM

• Guided gradient-weighted class activation map (Guided Grad-CAM)

• Combines guided backpropagation and Grad-CAM

GRAD-CAM

• Class-discriminative

• Localises relevant regions

• Coarse resolution

Grad-CAM vs Guided Grad-CAM

Guided Grad-CAM

• Class-discriminative

• Fine-grained

Guided backpropagation

• High resolution gradients

• Emphasises edges and textures

Grad-CAM: Counterfactual Explanations

• Negating the gradients used for calculation of the importance weights (ð¤-") shows regions that adversarially affect the output prediction

Note: These regions indicate features that suppress the class score.

Optimising over images

Recap: Backpropagation

Can we generate an image that maximises the score of a particular class?

Pose this as an optimisation problem wrt. ð¼∈ℝ'×), i.e. pixels (ð\*,ð$,…,ð'))

ð¼: zero-image

Recall: Gradient descent update rule

ð¤\#$% = ð¤\# − ð∇ð¤\#

The optimisation can be written as

argmax

\! Regulariser to ensure that ð¼

looks like an image

ð" ð¼ −ð ð¼

To update the image, use the following rule ð\#$% = ð\# + ð∇ð\#

Scores vector for class ð (before applying softmax)

Backpropagate to the Image

ð\! = 0,0,…,0,1,0,…,0

Images that maximise class scores

• Examples of images that maximise a class score

Adversarial attacks

Image source: MIT CSAIL

Fooling CNNs

• Using the idea of optimising over the input, we can “fool” CNNs

• Instead of maximising the log-likelihood of the correct class, set the loss to maximise some incorrect class

“benign” “malignant”

Minimal Perturbations

• Only minimal changes to the image (using backprop) are required to convince the CNN that this is a “malignant” skin lesion

“benign” perturbation

adversarial

“malignant”

Szegedy et al, Intriguing properties of neural networks. 2013. https://arxiv.org/abs/1312.6199 Finlayson et al, Adversarial attacks against medical deep learning systems, 2018. https://arxiv.org/abs/1804.05296

Credit: Mitesh Khapra

Why does this happen?

• There is a large number of points in the high-dimensional space of an image (e.g. ℝ\!)

“benign”

“benign”

Only a few images are seen during training

This (relatively) small set of training images are used to fit the decision boundaries

Ultimately, decision boundaries end up taking decision about many unseen points in this high-dimensional space

1\. Fragility

• Imperceptible perturbations can flip predictions

• High confidence ≠ robustness

2\. Shortcut learning

• High accuracy ≠ correct reasoning

• Models may exploit spurious correlations

3\. Explanation is not immunity

• Gradients explain behaviour

• The same gradients enable manipulation

• Not all explanations are faithful

Why this matters for trust

Adebayo et al, Sanity checks for saliency maps, NeurIPS, 2018 Tomsett et al, Sanity checks for saliency metrics, AAAI, 2020

Sanity Checks for Saliency Maps

• Saliency maps similar to edge detectors

• Insensitive to model or data

Technical

• Has it been stress-tested?

• Has it been evaluated out-of-distribution?

• Are failure modes understood?

When can we trust the model?

Clinical / Domain

• How does it perform across subgroups?

• What happens when it disagrees with experts?

• Is uncertainty quantified?

Ethical / Societal

• Who is accountable?

• Who is affected by errors?

• What level of transparency is required?

Thank you\!

Further Reading

• Interpretable Machine Learning, by Christoph Molnar -- online textbook

• https://pubs.rsna.org/doi/10.1148/ryai.2021200267

Useful resources:

• Filter visualisation tools:

• Lucid (for Tensorflow)

• Feature visualisation • Demos:

• t-SNE: https://distill.pub/2016/misread-tsne/ • https://distill.pub/2020/grand-tour/

• https://distill.pub/2018/building-blocks/

• Explainability toolboxes:

• DeepExplain

• iNNvestigate

Appendix

Which component is most relevant?

2 Saliency Maps Example: • 1 hidden units

• Biases: ð \! = ð \# = 1

• ReLU activation

• Weights: ð¾ \! = −1,−1 ,ð¾ \# = \[−1\]

If we forward-propagate, the output of the hidden unit in 'ð

the next layer will be

ð¾\['\]ℎ"

ð\["\]

ð¥% ð¥'

ð\[$\]

ℎ$ = max 0, 1 − ð¥$ − ð¥+ ;ð¦=1−ℎ$

ℎ%

8ð¦

ð¾\[%\]

\= :−ð¥, ð¥, ð¥% + ð¥' \> 1

ð¥ ≥ 0

1 2 Gradient Saturation Problem: The gradient of ℎ% wrt. both ð¥% and ð¥' is 0 if ð¥% + ð¥' \> 1

ð¥% + ð¥'

Which component is most relevant?

2 Saliency Maps • Limitation: Noisy gradients

Solution:

Gazelle Typical SmoothGrad • SmoothGrad: saliency maps randomly of the noisy add images

noise to the input image; average the https://arxiv.org/abs/1706.03825

Baumgartner, Christian F., et al. "Real-time standard scan plane detection and localisation in fetal ultrasound using fully convolutional neural networks." MICCAAI, 2016.

Application: Organ Localisation

Application: Pneumonia Detection

• Classification network • 121-layer DenseNet

• Pneumonia detection from chest X-rays

• Dataset: ChestX-ray14 • 100,000 frontal X-ray images with 14 disease classes

• Outperformed radiologists

Rajpurkar et al. CheXNet: Radiologist-level pneumonia detection of chest X-rays with deep learning, ICLR 2017

Application: Pneumonia Detection

Pathology-specific saliency maps

Rajpurkar et al. CheXNet: Radiologist-level pneumonia detection of chest X-rays with deep learning, ICLR 2017

Backpropagate to the Image

ð¼: zero-image

1\. Pass a zero-image as input 2. Set the score vector to be ð" = 0,0,…,0,1,0,…,0 3. 4. Compute the gradient Update the pixel: ð. )\*\!(,) = ð. )\!− "

ð )\*)\!\!(,)

" 5. Forward-pass the updated image through the network 6. Return to Step 2, repeat until convergence Note: this optimisation can be done

w.r.t. any neuron in the network

ð\! = 0,0,…,0,1,0,…,0

<https://radiopaedia.org/articles/chest-ap-erect-view-1?lang=gb>   
<https://www.cs.cmu.edu/~bhiksha/courses/10-601/decisiontrees/DT.png>   
<https://adalabucsd.github.io/research-blog/research/2019/06/07/krypton.html>   
<https://arxiv.org/abs/1610.02391>   
<https://arxiv.org/abs/1610.02391>   
<https://arxiv.org/abs/1610.02391>   
<https://arxiv.org/abs/1312.6199>   
<https://arxiv.org/abs/1804.05296>   
<https://arxiv.org/pdf/1810.03292.pdf>   
<https://arxiv.org/abs/1912.01451>   
<https://christophm.github.io/interpretable-ml-book/>   
<https://christophm.github.io/interpretable-ml-book/>   
<https://pubs.rsna.org/doi/10.1148/ryai.2021200267>   
<https://pubs.rsna.org/doi/10.1148/ryai.2021200267>   
<https://github.com/tensorflow/lucid>   
<https://github.com/tensorflow/lucid>   
<https://distill.pub/2017/feature-visualization/>   
<https://distill.pub/2017/feature-visualization/>   
<https://distill.pub/2016/misread-tsne/>   
<https://distill.pub/2016/misread-tsne/>   
<https://distill.pub/2016/misread-tsne/>   
<https://distill.pub/2020/grand-tour/>   
<https://distill.pub/2020/grand-tour/>   
<https://distill.pub/2020/grand-tour/>   
<ht
