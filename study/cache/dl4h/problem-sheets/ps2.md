# DL4H — Problem Sheet 2
> Source: Google Drive file 11SWkyTDYZgEp6gw2URoHJBKHd1PJTdVk · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Deep Learning in Healthcare Hilary Term 2026

Problem Sheet 2 Inductive Biases, Uncertainty & Transfer Learning

1 Inductive Biases and Geometric Equivariance in Medical Im-

age Analysis

Medical imaging tasks often require models to handle geometric transformations appropriately. This question explores how architectural choices encode assumptions about geometry.

Setup: Consider two tasks:

• Task A: Segmenting lung nodules from CT scans

• Task B: Classifying whether a chest X-ray shows cardiomegaly, where images come from different hospitals with varying patient positioning and scanner configurations

(a) Translation equivariance in CNNs.

(i) Explain why convolution is translation equivariant, and discuss the implications of

this property for Tasks A and B. (ii) Standard CNN classifiers apply global average pooling before the final fully-connected layer. Explain how this affects the network’s equivariance properties, and why this design choice is appropriate for some tasks but not others.

(⋆ Challenge) Let Tδ denote the translation operator by δ pixels. Prove that discrete convolution with kernel k satisfies Tδ\[k ∗ x\] = k ∗ Tδ\[x\]. Then characterise the class of linear operators L that are translation equivariant, i.e., satisfy Tδ ◦ L = L ◦ Tδ for all δ.

(b) Skip connections as an inductive bias.

UNet’s skip connections concatenate encoder features with decoder features at matching spatial resolutions.

(i) What assumption about the relationship between input and output does this archi- tecture encode? Describe a medical imaging scenario where this assumption would be violated. (ii) A student proposes removing skip connections and instead using a much deeper bottleneck to preserve spatial information. Analyse this proposal in terms of the optimisation landscape and what the network must learn.

(c) Spatial Transformer Networks.

A Spatial Transformer Network (STN) contains a localisation network that predicts trans- formation parameters, and a differentiable sampling module that applies the transforma- tion to feature maps.

(i) Explain the key difference between using an STN versus data augmentation for han- dling geometric variability, particularly regarding generalisation to unseen transfor- mations.

Deep Learning in Healthcare Hilary Term 2026

(ii) For a 2D affine transformation, the localisation network outputs 6 parameters. How would you modify the parameterisation to restrict the STN to learning only rigid transformations (rotation + translation)?

(⋆ Challenge) For the rigid transformation parameterisation in (ii), derive the Jacobian ∂x//∂θ needed for backpropagation, where x/ = R(θ)x+t and θ is the rotation angle. Ex- plain why this parameterisation avoids the singularities that can arise with other rotation representations.

(d) Architectural choices for clinical deployment.

A hospital wants to deploy a model for detecting pneumothorax from portable bedside chest X-rays, which have high variability in patient positioning, rotation, and cropping compared to standard acquisitions. Compare the trade-offs between: (i) a standard CNN with aggressive data augmentation, (ii) a CNN with an STN module, and (iii) an alternative approach of your choice. Consider sample efficiency, interpretability, and potential failure modes.

Clinical Context: Inductive biases determine what a model can learn efficiently from limited data. Choosing architectures whose assumptions match the clinical task is essential for robust deployment.

2 Dropout and Uncertainty Quantification in Medical Imaging

Consider a CNN for diabetic retinopathy grading from fundus images. The model uses dropout layers and you wish to quantify uncertainty in its predictions.

Setup:

• Input: 512×512 RGB fundus images

• Architecture: VGG-16 style network with dropout (p = 0.5) before each of the final two fully-connected layers

• Output: 5-class classification (severity grades 0–4)

• Training set: 35,000 images from 3 hospitals

(a) Dropout as regularisation.

(i) During training, dropout randomly zeroes neurons with probability p. Explain why the remaining activations must be scaled by 1/(1 − p), and what would happen to the output magnitude at test time if this scaling were omitted. (ii) Dropout is typically applied to fully-connected layers but rarely to early convolu- tional layers. Explain why dropout is less effective (and potentially harmful) in early convolutional layers.

(b) Monte Carlo Dropout for uncertainty estimation.

At test time, instead of disabling dropout, we run T = 50 stochastic forward passes with dropout enabled and collect the predicted probability vectors.

(i) Explain how the variance across these T predictions provides an estimate of model

uncertainty, and why this approach approximates Bayesian inference. (ii) Two test images both receive a mean predicted probability of ∼0.72 for class 2 (moderate diabetic retinopathy), but one has standard deviation 0.04 across the 50 passes while the other has standard deviation 0.31. Explain how a clinician should interpret these predictions differently.

Deep Learning in Healthcare Hilary Term 2026

(c) Aleatoric vs epistemic uncertainty.

Discuss how aleatoric and epistemic uncertainty would manifest in the following scenarios, and explain the implications for improving the system:

• Test images from a hospital whose scanner produces image characteristics not seen during training

• Fundus images with poor focus or lens artefacts that obscure the retina

(d) Clinical decision-making under uncertainty.

A screening programme uses the CNN to triage patients: high-confidence normal predic- tions are cleared automatically, while uncertain cases are reviewed by an ophthalmologist. The model shows systematically higher uncertainty on images from patients over 80, de- spite similar accuracy to other age groups.

Discuss whether the triage system should use uncertainty estimates (rather than pre- dicted probability alone), and propose explanations for the elevated uncertainty in elderly patients.

Clinical Context: Uncertainty quantification is essential for safe deployment of DL in screening programmes, where overconfident incorrect predictions could lead to missed diagnoses or unnecessary referrals.

3 Transfer Learning in Medical Image Analysis (Optional)

A research team wants to build a classifier for a rare autoimmune skin condition from der- matoscopy images. Labelled medical data is scarce, but large-scale pretrained models are avail- able.Setup:

• Target dataset: 500 labelled dermatoscopy images (200 positive, 300 negative)

• Source model: ResNet-50 pretrained on ImageNet (1.2 million natural images, 1000 object classes)

(a) Feature transferability and fine-tuning.

The team considers three strategies: (A) use the pretrained network as a fixed feature extractor (freeze all convolutional layers, train only a new classification head), (B) fine- tune the entire network end-to-end, and (C) progressively unfreeze layers starting from the head.

Analyse the trade-offs between these strategies. Your answer should address what types of features at different layers of the ImageNet model are likely to transfer to dermatoscopy, and why fine-tuning with a large learning rate (e.g., 10-2) can cause validation accuracy to drop sharply before partially recovering.

(b) Source model selection and clinical deployment.

The team is offered access to two additional pretrained models:

• Model P: A ResNet-50 trained on 200,000 chest X-rays for pneumonia detection

• Model Q: A ResNet-50 trained on 100,000 dermatoscopy images for melanoma classification

Deep Learning in Healthcare Hilary Term 2026

Analyse which source model (ImageNet, Model P, or Model Q) would be most effective for the target task. A clinician then asks: “If the best model was originally trained to recognise dogs and cars, how can I trust it to diagnose skin conditions?” Critically address this concern.

Clinical Context: Transfer learning is the dominant paradigm in medical image analysis, where labelled datasets are typically too small to train deep networks from scratch.
