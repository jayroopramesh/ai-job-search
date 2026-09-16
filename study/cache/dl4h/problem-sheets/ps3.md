# DL4H — Problem Sheet 3
> Source: Google Drive file 1aZFONMoE54RL3bksM8IVQ70e6SMJ0Vd4 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Deep Learning in Healthcare Hilary Term 2026

Problem Sheet 3 Generative Models, Self-Supervised Learning & Domain Adaptation

1 Generative Adversarial Networks for Medical Data Augmen-

tation

Generative Adversarial Networks (GANs) can synthesise realistic medical images to augment limited training data. Consider a GAN for generating synthetic chest X-rays to augment a pneumonia detection dataset.

(a) GAN training objective. Write down the GAN minimax objective and explain in- tuitively what the generator and discriminator are each optimising. What is the Nash equilibrium of this game, and how does the non-saturating generator loss differ from the original formulation?

(b) (⋆ Challenge) Optimal discriminator D∗(x). When the generator is fixed, the optimal

discriminator is:

D∗(x) = pdata(x)

pdata(x) + pG(x) Derive this expression by treating the GAN objective as an integral and maximising pointwise. What value does D∗(x) take when the generator perfectly reproduces the data distribution, and why?

(c) GAN failure modes. GAN training is often unstable. Explain the mathematical cause

of each of the following failure modes and give one mitigation strategy for each:

• Mode collapse,

• Vanishing gradients, and

• Oscillation.

(d) Synthetic data trade-offs. You generate 10,000 synthetic pneumonia X-rays and add them to 1,000 real training samples. A classifier trained on real+synthetic data achieves 85% accuracy on real test data versus 78% with real data only. However, a radiologist identifies that 30% of synthetic images contain unrealistic artefacts (e.g., impossible lung anatomy).

• Discuss the trade-off between improved accuracy and potential bias.

• What quality metrics or criteria would you use to validate synthetic medical images before use?

• When should synthetic data not be used for training medical deep learning models?

Clinical Context: While GANs can alleviate data scarcity, unrealistic synthetic data can introduce harmful biases. Regulatory bodies require transparency and rigorous validation when synthetic data are used in medical AI training.

Deep Learning in Healthcare Hilary Term 2026

2 Self-Supervised Learning for Medical Imaging

Consider a large set of unlabelled chest X-rays and a small set of labelled examples for a downstream pneumonia detection task.

(a) Pretext tasks. Self-supervised learning trains a network on a pretext task whose labels

are automatically derived from the data, without human annotation.

(i) Give two examples of general-purpose pretext tasks and explain how solving each task forces the network to learn semantically meaningful image representations. (ii) Propose two pretext tasks specifically suited to medical imaging. For each, explain

what domain-specific structure they exploit.

(b) Contrastive learning. In SimCLR, two augmented views of the same image form a positive pair; views from different images in the same batch form negative pairs. The InfoNCE loss is:

L = −log ∑exp(sim(zi,zj)/τ) k=i

exp(sim(zi,zk)/τ)

(i) Explain intuitively what this loss encourages and why a large batch size matters. (ii) Standard augmentations for natural images include aggressive colour jittering, ran- dom cropping, and greyscale conversion. Discuss which of these are appropriate or inappropriate for chest X-rays and histopathology slides, and why.

(c) Linear probing vs fine-tuning. After pretraining, the backbone is evaluated on the downstream task using either (i) linear probing (the backbone is frozen and only a linear classifier is trained); or (ii) fine-tuning (some or all backbone weights are updated).

• Explain what each approach measures and when each is preferable.

• You have only 100 labelled examples. Which approach do you choose and why?

(d) Domain gap. A model is pretrained on ImageNet (natural colour photographs) and a second model is pretrained on 100,000 unlabelled chest X-rays using the same contrastive learning method. Both are subsequently fine-tuned on 100 labelled X-rays for pneumonia detection.

• Which model do you expect to perform better and why?

• What is the key practical benefit of self-supervised pretraining in healthcare settings?

• Describe one limitation of self-supervised pretraining that is particularly relevant to medical imaging.

Clinical Context: Annotation of medical images requires expert clinicians and is expensive and time-consuming. Self-supervised learning enables the use of large unlabelled datasets (far more readily available) to learn representations that transfer effectively to labelled downstream tasks.

3 Adversarial Domain Adaptation

A pneumonia detection model is trained on chest X-rays from Hospital A and then deployed at Hospital B, which uses different scanner hardware and serves a different patient population.

Deep Learning in Healthcare Hilary Term 2026

(a) Domain shift. Even if the clinical task is identical at both hospitals, the model may perform substantially worse at Hospital B. Explain what domain shift is and describe, in terms of feature distributions and decision boundaries, why the model fails.

(b) Domain adversarial training. Domain Adversarial Neural Networks (DANN) add a domain discriminator Dd that tries to classify whether a feature vector came from Hospital A or Hospital B.

(i) Write down the combined training objective for DANN and describe the roles of the

feature extractor F, task classifier C, and domain discriminator Dd. (ii) What is the gradient reversal layer (GRL)? How does it implement adversarial train-

ing without requiring an alternating optimisation loop?

(c) Domain-invariant features. At convergence, what property do the features extracted by F have with respect to the domain discriminator? What is the theoretical justification for why domain-invariant features should improve target-domain performance? Under what conditions might this assumption fail?

(d) Limitations and alternatives.

(i) Describe one fundamental limitation of DANN’s marginal distribution alignment

approach. (ii) Two approaches that address domain shift without adversarial training are described

below. CORAL (CORrelation ALignment): minimises the Frobenius norm of the differ- ence in feature covariance matrices between source and target domains, encouraging second-order feature statistics to match. Maximum Mean Discrepancy (MMD): minimises a kernel-based measure of distributional distance, MMD2(p, q) = ∥µp−µq∥2H, where µp, µq are mean embeddings of the source and target feature distributions in a reproducing kernel Hilbert space. Using these descriptions, compare the trade-offs of CORAL and MMD against DANN in terms of what they align, implementation complexity, and expressiveness. (iii) A practical first step when deploying a model to a new hospital requires no retraining

whatsoever. What is it, and why does it help?

Clinical Context: Models trained at a single institution routinely degrade when deployed elsewhere due to differences in imaging equipment, patient demographics, and local practices. Domain adaptation addresses this without requiring labels from the target site, making it valu- able for real-world multi-site deployment.

4 Normalising Flow Models

Consider using a normalising flow model for anomaly detection on ECG recordings, where the goal is to assign a likelihood score to new recordings and flag those with unusually low probability as potential arrhythmias.

(a) Change of variables and exact likelihood. A normalising flow defines an invertible mapping f : Z→X from a simple base distribution pZ (e.g., N(0,I)) to the data space.

(i) Write the change-of-variables formula for logpX(x) in terms of f−1 and the Jacobian

determinant.

Deep Learning in Healthcare Hilary Term 2026

(ii) Why is exact likelihood computation particularly valuable for anomaly detection, compared to using a trained classifier’s confidence score or a GAN’s discriminator output as a proxy?

(b) Invertibility constraints.

(i) Explain why the mapping f must be bijective, giving separate reasons for generation

and likelihood computation. (ii) Computing the Jacobian determinant of a general d × d mapping costs O(d3). Why is this prohibitive for high-dimensional data, and what structural constraint do flow layers impose to make the determinant tractable?

(c) Affine flow layers. An affine flow layer applies the elementwise transformation:

yi = exp(si) · xi + ti, i = 1,...,d

where s and t are learned parameter vectors.

(i) Write down the inverse transformation xi in terms of yi, si, and ti. (ii) Compute the log-Jacobian determinant log|detJf|. Why is it tractable, and how

does this compare to the O(d3) cost for a general transformation? (iii) A single affine layer transforms each dimension independently with no interaction between dimensions. Why must multiple layers be composed, and what must be interleaved between them to make the model expressive?

(d) Comparison with GANs. Normalising flows and GANs are both deep generative mod- els but differ fundamentally in how they are trained and what they can compute. Sum- marise the key differences with respect to likelihood tractability, sample quality, and train- ing stability. For ECG anomaly detection specifically, which approach is most principled and why?

Clinical Context: Exact likelihood-based models are particularly appealing for clinical anomaly detection, where a calibrated probability score can directly inform clinical decision thresholds. Unlike discriminative classifiers, flow models do not require labelled anomaly exam- ples at training time.
