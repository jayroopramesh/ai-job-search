# DL4H — Problem Sheet 3: Student Solutions
> Source: Google Drive file 1o7lPXYjf4-il_L9EvMBspHkNYwxm6q4u · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Deep Learning in Healthcare Hilary Term 2026

Problem Sheet 3 – Student Solutions

Generative Models, Self-Supervised Learning & Domain Adaptation

This guide provides key results and concise explanations for each question. Use it to check your own working and to fill in any gaps in understanding.

1 Generative Adversarial Networks for Medical Data Augmen-

tation

(a) GAN training objective.

The GAN minimax objective is:

minG maxD Ex∼pdata\[logD(x)\] + Ez∼pz\[log(1 − D(G(z)))\]

Discriminator: maximises the objective by pushing D(x) → 1 for real chest X-rays (Term 1) and D(G(z)) → 0 for synthetic ones (Term 2). This is equivalent to binary cross-entropy classification.

Generator: minimises the objective by making D(G(z)) → 1. In practice, the non- saturating form maxG Ez\[logD(G(z))\] is used to avoid vanishing gradients early in train- ing.

The adversarial game converges at a Nash equilibrium where G generates images indistin- guishable from the training set and D can do no better than guess randomly (D∗(x)=0.5 everywhere).

(b) (⋆ Challenge) Optimal discriminator D∗(x).

For a fixed generator, the optimal discriminator is found by maximising the objective pointwise. Writing the expectation as an integral and maximising the integrand pdata(x) logy+ pG(x) log(1 − y) with respect to y = D(x) gives:

D∗(x) = pdata(x)

pdata(x) + pG(x)

When pG(x) = pdata(x) (perfect generation), D∗(x)=0.5 for all x: the generator has learned the true data distribution and the discriminator cannot distinguish real from fake.

(c) GAN failure modes.

Mode collapse: the generator maps all latent codes z to a single output x∗ that fools the current discriminator. No diversity term in the objective prevents this local minimum. Mitigations include minibatch discrimination (the discriminator sees multiple generated samples at once and can penalise lack of diversity) and the Wasserstein GAN loss, which uses the earth mover distance and provides more informative gradients throughout train- ing.

Deep Learning in Healthcare Hilary Term 2026

Vanishing gradients: if the discriminator becomes too accurate early on, D(G(z)) ≈ 0 for all generated images. The original generator loss log(1−D(G(z))) saturates near zero, giving near-zero gradient. Using the non-saturating form −logD(G(z)) or updating the discriminator less frequently mitigates this.

Oscillation: the minimax objective does not reduce to standard minimisation, so simul- taneous gradient descent can cycle rather than converge. Wasserstein GANs and spectral normalisation on the discriminator (constraining its Lipschitz constant) improve stability.

(d) Synthetic data trade-offs.

Adding 10,000 synthetic samples raises accuracy from 78% to 85%, but 30% of synthetic images contain unrealistic artefacts. The risk is that the classifier learns artefact patterns rather than clinically relevant pathology, failing on real patients who lack these artefacts. There is also a risk of the model becoming overconfident if evaluated on synthetic test images.

Quality metrics: Fréchet Inception Distance (FID) measures distributional similarity in feature space. Clinical validation (a radiologist Turing test) directly assesses realism. Anatomical constraint checking (correct rib count, organ positions) catches anatomically impossible images. The most critical metric is downstream performance on a real holdout set: if accuracy drops when synthetic samples are included, they are harmful.

Best practice: use synthetic data for pretraining or augmentation and always validate on real data. Avoid use in high-stakes applications (cancer diagnosis, surgical planning) without rigorous clinical validation and regulatory approval.

2 Self-Supervised Learning for Medical Imaging

(a) Pretext tasks.

Self-supervised learning trains a network on a pretext task whose labels are derived auto- matically from the data itself, without human annotation. Examples include: predicting the rotation angle applied to an image (0°, 90°, 180°, 270°), reassembling shuffled image patches (jigsaw puzzle), and reconstructing masked-out regions (masked autoencoders). The key insight is that solving such tasks requires learning semantically meaningful im- age representations. A network that reliably predicts rotation must have understood the content of the image.

In medical imaging, relevant pretext tasks exploit domain-specific structure: predicting which slice a 2D image came from in a 3D volume, predicting the relative position of two patches within a scan, or reconstructing masked segments of an ECG. The pretrained representations are then transferred to downstream tasks with limited labels via linear probing or fine-tuning.

(b) Contrastive learning.

In contrastive learning (e.g., SimCLR), two augmented views of the same image form a positive pair; views from different images in the same batch form negative pairs. The In- foNCE loss pulls positive pairs together and pushes negative pairs apart in the embedding space:

L = −log exp(sim(zi,zj)/τ) Pk=i exp(sim(zi,zk)/τ)

Deep Learning in Healthcare Hilary Term 2026

where τ is a temperature hyperparameter. A large batch provides many negatives, which is essential: without hard negatives the representation may collapse to a constant.

Augmentation choice is critical for medical images. Colour jittering is appropriate for colour histology but must be avoided for greyscale X-rays. Rotations and flips may be appropriate, but the degree must reflect clinically plausible variation. Augmentations should be clinically uninformative (so representations are invariant to artefacts) but not clinically destructive (so representations retain pathology information).

(c) Linear probing vs fine-tuning.

Linear probing: the pretrained backbone is frozen and only a single linear classifier is trained on the labelled downstream data. This directly measures representation quality: if the features are linearly separable by class, the representation is good. It is not confounded by subsequent feature learning.

Fine-tuning: some or all of the backbone weights are updated on the downstream task. This allows features to adapt to the target domain, often improving accuracy, but risks overwriting general representations if the target dataset is small.

With very few labels (e.g., 100 annotated images), linear probing is safer. With more labels (1,000+), fine-tuning the final few layers typically yields the best results. Full fine- tuning is only advisable when the downstream dataset is large enough to avoid catastrophic forgetting of the pretrained representations.

(d) Domain gap and medical imaging considerations.

Models pretrained on natural images (colour photographs) learn representations tuned to that domain. Medical images differ in modality (greyscale X-rays, volumetric MRI, time- series ECG), in the nature of clinically relevant features (subtle density changes rather than object edges), and in acquisition artefacts. Pretraining on unlabelled medical im- ages of the same modality consistently outperforms natural-image pretraining for medical downstream tasks.

The sample efficiency benefit is particularly valuable in healthcare. A model pretrained on 100,000 unlabelled chest X-rays and fine-tuned on 100 labelled examples can rival a model trained on 1,000 labelled examples from scratch, dramatically reducing the annotation burden on expert clinicians.

The main limitation is that pretext task objectives do not guarantee that all task-relevant features are captured. A model trained on rotation prediction may not learn features relevant to detecting subtle lung nodules. Task-aligned pretext tasks (e.g., masked recon- struction of anatomically meaningful regions) and careful augmentation design mitigate this risk.

3 Adversarial Domain Adaptation

(a) Domain shift and its effects.

A model trained on Hospital A minimises the loss under Hospital A’s data distribution PA. When deployed at Hospital B with distribution PB, input features may be systematically different due to different scanner manufacturers, field strengths, patient demographics, or imaging protocols. The model’s decision boundary, calibrated for PA, may no longer align correctly with PB.

Deep Learning in Healthcare Hilary Term 2026

Concretely, internal activations (the effective features used by the classifier) shift in mean and variance across domains. Batch normalisation statistics learned from PA are also mismatched (see PS1, Section 5). Even if the true clinical task and decision boundary are identical in both hospitals, the model cannot locate the correct boundary in the shifted feature space. Performance degrades substantially on PB even if accuracy on PA remains high, often without any visible warning signal.

(b) Domain adversarial training.

Domain Adversarial Neural Networks (DANN) add a domain discriminator Dd that clas- sifies whether a feature vector came from the source (Hospital A) or target (Hospital B) domain. The feature extractor F is trained adversarially: the task classifier loss encour- ages discriminative features, while the domain loss encourages domain-invariant features:

min F,C max Dd Lclass(F, C) − λLdomain(F, Dd)

The gradient reversal layer (GRL) implements this efficiently: it acts as an identity during the forward pass but negates gradients by −λ during backpropagation. Gradient steps that would make features easier for Dd to classify are reversed into steps that make them harder, without requiring an explicit alternating training loop.

(c) Domain-invariant features and convergence.

At convergence, the features extracted by F are ideally domain-invariant: Dd performs no better than chance at classifying source versus target. Meanwhile, the task classifier C retains discriminative power, because the adversarial pressure applies only to domain identity, not to class identity.

The theoretical motivation is: if the marginal feature distribution p(F(x)) is aligned across domains, a classifier trained on the source domain generalises to the target domain. DANN directly enforces this marginal alignment. Whether conditional alignment (p(F(x)|y)) follows depends on whether class representations are consistent across domains. This is not guaranteed when class proportions differ between hospitals.

In practice, domain adaptation works best when the domains are similar (same anatomical region, same imaging modality) and label distributions are comparable. For large domain gaps or significant class imbalance differences, additional constraints or a small number of target-domain labels (semi-supervised domain adaptation) are often needed.

(d) Limitations and alternatives.

Limitations of DANN: marginal distribution alignment does not guarantee conditional alignment. If class prevalences differ between hospitals, the adversary may align by map- ping different classes to similar features, corrupting the classifier. The method also requires access to unlabelled target-domain data during training.

CORAL (CORrelation ALignment) matches the first- and second-order feature statistics (mean and covariance) between source and target domains, without adversarial training. It is simpler to implement but less expressive.

Maximum Mean Discrepancy (MMD) minimises a kernel-based measure of distri- butional distance between source and target features. It is theoretically principled but sensitive to kernel choice.

Test-time adaptation (TTA) adapts the model at inference time using only unlabelled test examples, without retraining on target data. It is useful when the target distribution is unknown at training time.

Deep Learning in Healthcare Hilary Term 2026

For clinical deployment at a new hospital, a practical first step is batch normalisation adaptation: recompute running statistics on a small calibration set from the new hospital before deployment. This is simple, requires no retraining, and often recovers substantial performance.

4 Normalising Flow Models

(a) Change of variables and exact likelihood.

A normalising flow defines an invertible mapping f : Z→X from a simple base distribu- tion pZ (e.g., N(0,I)) to the data space. The change of variables formula gives the exact log-likelihood:

logpX(x) = logpZ(f−1(x)) + log detJf−1(x)

where Jf−1 is the Jacobian of the inverse mapping. The flow “normalises” the complex data distribution into the simpler pZ through a sequence of invertible transformations. This is particularly valuable for anomaly detection: a normal ECG should have high pX(x), while an arrhythmic ECG should have low pX(x). Unlike a GAN’s discriminator output or a classifier’s confidence score, the exact log-likelihood is a calibrated probability that can directly serve as an anomaly score without requiring labelled anomaly examples.

(b) Invertibility requirement.

Flows must be bijective for two reasons:

(1) Generation: to sample new data, draw z ∼ pZ and compute x = f(z). Without a

well-defined forward mapping, generation is undefined. (2) Likelihood computation: computing pX(x) requires evaluating f−1(x) and detJf−1.

Without invertibility, neither is defined.

A further constraint is that the Jacobian determinant must be tractable. Computing the determinant of a general d × d matrix costs O(d3), which is prohibitive for high- dimensional data (e.g., d = 512 for an ECG segment). Flows must therefore be designed with triangular or block-structured Jacobians so the determinant reduces to a product of diagonal elements, computable in O(d).

This architectural constraint distinguishes flows from GANs, which can use arbitrary neural network architectures.

(c) Affine flow layers.

An affine flow layer applies yi = exp(si) · xi + ti elementwise. Inverse: xi = (yi − ti) · exp(−si). Log-Jacobian determinant: The Jacobian is diagonal with entries ∂yi/∂xi = exp(si), so:

log|detJf| =

Xdi=1

si

This is O(d) (a simple sum) versus O(d3) for a general matrix. The diagonal structure arises because each output yi depends only on xi.

Deep Learning in Healthcare Hilary Term 2026

Expressiveness: A single affine layer transforms each dimension independently with no interaction between dimensions. To capture dependencies in the joint distribution, multi- ple affine layers must be composed with permutations (or learned linear maps) interleaved between them, so that information mixes across dimensions before each subsequent affine transformation.

(d) Comparison with GANs.

Normalising flows and GANs differ in three key ways:

Likelihood: Flows compute the exact log-likelihood via the change-of-variables formula. GANs have no tractable density: they provide a generator but no likelihood estimate.

Sample quality: GANs typically produce sharper, more realistic samples because the adversarial loss directly penalises distributional mismatch in data space. Flow samples are constrained by the expressiveness of the invertible architecture.

Training stability: Flows are trained by maximum likelihood: a well-posed single- objective optimisation. GAN training is a two-player minimax game, prone to mode collapse, vanishing gradients, and oscillation (see Section 1).

For ECG anomaly detection: Flows are most principled. The exact log-likelihood logpX(x) provides a calibrated, threshold-based anomaly score: a normal ECG should have high logpX(x) and an arrhythmia should have low logpX(x). GANs cannot compute this score directly; the discriminator output is not a calibrated density and would require additional estimation steps.
