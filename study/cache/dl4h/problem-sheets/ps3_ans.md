# DL4H — Problem Sheet 3: Worked Solutions
> Source: Google Drive file 1zFl8uzb6LpSseuAcXeCB91EF7ZkkWMxg · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Problem Sheet 3: Worked Solutions 

|  |
| :-: |
| [**Page 1**]() |

Deep Learning in Healthcare

Hilary Term 2026

Problem Sheet 3: Worked Solutions

Generative Models, Self-Supervised Learning & Domain Adaptation

Important: These solutions are for instructor use only. Provide to students only after submis-

sion deadlines.

1 Generative Adversarial Networks for Medical Data Augmen-

tation

(a) GAN training objective.

The GAN minimax objective is:

min

G

max

D

Ex∼pdata \[log D(x)\] + Ez∼pz \[log(1 − D(G(z)))\]

Discriminator: maximises both terms simultaneously. Term 1 pushes D(x) → 1 for real

X-rays (classify real as real). Term 2 pushes D(G(z)) → 0 for synthetic X-rays (classify

fake as fake). This is binary cross-entropy classification.

Generator: only affects Term 2, which it minimises: push D(G(z)) → 1 so the discrim-

inator is fooled into thinking the synthetic X-ray is real.

Nash equilibrium: the generator reproduces the data distribution (pG = pdata), so

the discriminator cannot distinguish real from fake and guesses randomly (D∗(x)=0.5

everywhere). No player can improve their outcome by changing strategy.

Non-saturating loss: the original generator loss log(1 − D(G(z))) saturates near zero

when the discriminator is strong early in training, giving vanishing gradients. The non-

saturating form −log D(G(z)) (equivalently, maxG E\[log D(G(z))\]) has stronger gradients

precisely when the generated images are poor, accelerating early learning.

(b) (⋆ Challenge) Optimal discriminator D∗(x).

For a fixed generator, the discriminator objective is:

V (D) = Ex∼pdata \[log D(x)\]+Ex∼pG \[log(1−D(x))\] =

Z

pdata(x) log D(x)+pG(x) log(1−D(x))&#3;dx

Maximise pointwise: set a = pdata(x), b = pG(x), y = D(x) and maximise f(y) =

alog y + blog(1 − y) over y ∈ (0,1):

df

dy

\=

a

y

−

b

1 − y

\=0 =⇒ y =

a

a + b

Hence:

D

∗

(x) =

pdata(x)

pdata(x) + pG(x)

When pG(x) = pdata(x), D∗(x) = 0.5 everywhere: the generator has perfectly repro-

duced the training distribution, so the discriminator cannot do better than random.

This is the Nash equilibrium. Substituting D∗ back into V yields V (G, D∗) = −log 4 +

2 JSD(pdata∥pG), where the Jensen–Shannon divergence reaches its minimum of zero when

pG = pdata.

-----

|  |
| :-: |
| [**Page 2**]() |

Deep Learning in Healthcare

Hilary Term 2026

(c) GAN failure modes.

Mode collapse. The generator finds a single output x∗ = G(z) for all z that reliably

fools the current discriminator. Because the objective has no explicit diversity term, the

generator has no incentive to explore the full support of pdata; the local minimum of a

single convincing output is stable.

Mitigation: minibatch discrimination – the discriminator receives multiple generated sam-

ples at once and can detect when they are all similar, penalising collapse. Alternatively,

the Wasserstein GAN replaces JS divergence with the earth mover distance, providing

more informative gradients globally and reducing collapse.

Vanishing gradients. If the discriminator becomes very accurate early in training,

D(G(z)) ≈ 0 for all generated images. The original generator loss log(1 − D(G(z)))

saturates near zero with near-zero gradient, so the generator stagnates. This occurs

because the discriminator can train faster than the generator on very poor early samples.

Mitigation: use the non-saturating generator loss −log D(G(z)), which provides strong

gradients when the generator is weakest. Alternatively, update the discriminator less

frequently (1 update per 2–5 generator updates).

Oscillation. GAN training is a two-player minimax game, not a standard minimisation.

Simultaneous gradient descent on G and D can cycle around the Nash equilibrium rather

than converge to it, because each player’s optimal strategy is a moving target as the other

player updates.

Mitigation: spectral normalisation constrains the discriminator’s Lipschitz constant, sta-

bilising the gradient signal. Wasserstein GANs enforce a 1-Lipschitz constraint via weight

clipping or gradient penalty, providing a smoother, more convex landscape.

(d) Synthetic data trade-offs.

Adding 10,000 synthetic samples improves accuracy from 78% to 85%, but 30% of those

samples contain unrealistic artefacts. The risk is spurious feature learning: the classifier

may learn to associate the GAN’s characteristic artefacts (e.g., texture statistics, specific

pixel patterns) with the pneumonia label rather than genuine pathological signs. Such a

classifier would fail on real patients who lack these artefacts, potentially performing worse

than the 78% baseline on a truly independent test set.

Quality metrics. (i) Fréchet Inception Distance (FID): measures distributional simi-

larity between real and synthetic images in a deep feature space; lower is better. (ii)

Radiologist Turing test: a blinded radiologist classifies images as real or synthetic; syn-

thetic images passing at rates near 50% are considered realistic. (iii) Anatomical constraint

checking: automated rules (correct rib count, cardiac silhouette, lung symmetry) catch

anatomically impossible images. (iv) Downstream task performance on a real holdout set:

the only ultimately reliable metric. If accuracy on the real holdout set decreases when

synthetic training data are included, those data are harmful regardless of how realistic

they appear.

When not to use synthetic data. In high-stakes applications (cancer diagnosis, sur-

gical planning, emergency triage) where errors have severe patient consequences. When

the synthetic data quality is low (artefacts in \> 10% of images), as spurious features are

likely to be learned. When the target pathology is rare and the GAN cannot learn a

good distribution from the available real examples (fewer than ∼100 cases). Any clinical

deployment should disclose synthetic data usage and may require additional regulatory

validation.

Best practice: use synthetic data for pretraining or augmentation, always validate on a

real holdout set, and never use a test set that includes synthetic images.

-----

|  |
| :-: |
| [**Page 3**]() |

Deep Learning in Healthcare

Hilary Term 2026

2 Self-Supervised Learning for Medical Imaging

(a) Pretext tasks.

Self-supervised learning trains a network on a pretext task whose labels are derived au-

tomatically from the data, without human annotation. The hypothesis is that solving a

challenging pretext task requires learning representations that capture semantically mean-

ingful structure.

General-purpose pretext tasks.

Rotation prediction: apply one of four rotations (0°, 90°, 180°, 270°) and ask the network

to classify which rotation was applied. A network that reliably identifies rotation must

have understood the content and orientation of the image – it cannot rely on low-level

statistics alone. This forces learning of object parts and their spatial relationships.

Jigsaw puzzle: shuffle image patches into a random permutation from a pre-defined set

and ask the network to identify the permutation. Solving this requires understanding the

spatial arrangement of parts, which drives learning of object-level structure. More difficult

than rotation prediction but also more representationally rich.

Masked autoencoders (MAE): mask a large fraction (∼75%) of patches and reconstruct

the missing content. The network must learn rich, contextual representations to predict

masked regions from limited visible context.

Medical imaging pretext tasks.

Slice order prediction (3D volumes): given two 2D slices extracted from a 3D MRI or CT

volume, predict which came first in the anatomical sequence. Correct ordering requires

understanding anatomical structure (e.g., liver above kidney), driving learning of clinically

meaningful spatial features.

Relative patch position (X-ray or histology): given two patches from the same image,

predict the spatial relationship of one relative to the other (one of eight possible directions).

Forces learning of long-range structural relationships within the image. Works well when

global anatomy is informative.

Masked ECG reconstruction: mask segments of a time series and reconstruct them from

surrounding context. Drives learning of waveform morphology and temporal dynamics –

precisely the features needed for arrhythmia detection.

(b) Contrastive learning.

InfoNCE loss. Two augmented views of the same image form a positive pair (zi,zj);

all views from different images in the same batch form negative pairs. The loss:

L = −log

exp(sim(zi,zj)/τ)

P

k̸=i exp(sim(zi,zk)/τ)

encourages the embedding of the two augmented views to be similar (numerator) while

pushing them apart from all other images in the batch (denominator). The tempera-

ture τ controls the concentration: small τ makes the distribution over negatives sharper,

providing stronger gradients.

Why large batch size matters. Each image in the batch provides B − 1 negatives for

every other image. With B = 4096 (SimCLR), each positive pair is contrasted against

\>8000 negatives, including hard negatives (images from similar classes that must be distin-

guished). Without sufficient hard negatives, the representation may collapse to a coarse,

trivially separable space.

Augmentation design for medical images.

-----

|  |
| :-: |
| [**Page 4**]() |

Deep Learning in Healthcare

Hilary Term 2026

Colour jittering: appropriate for colour histopathology slides (random changes in stain

intensity mimic scanner variability and force stain-invariant representations). Should be

avoided for chest X-rays, which are inherently greyscale and where intensity encodes clin-

ically relevant information (tissue density). Applying colour jitter to greyscale images or

to images where grey-level changes carry pathological meaning can destroy diagnostically

relevant structure.

Random cropping: generally appropriate for both modalities. Cropping forces the network

to recognise anatomy from partial views, which is a desirable robustness property. Care

is needed not to crop out the entire pathological region of interest (e.g., a small nodule).

Greyscale conversion: irrelevant for chest X-rays (already greyscale). For histopathology,

converting to greyscale removes colour information that may be diagnostically informative

(e.g., haematoxylin–eosin staining patterns); use with caution.

Key principle: augmentations should mimic clinically uninformative variability (scanner

differences, patient positioning) while preserving clinically informative content (pathology,

tissue type).

(c) Linear probing vs fine-tuning.

Linear probing: the pretrained backbone is frozen and only a single linear classifier is

trained on the downstream labelled data. This directly measures representation quality:

if the pretrained features are linearly separable by class, the backbone has captured the

relevant structure. Crucially, it is not confounded by further feature learning.

Fine-tuning: some or all backbone weights are updated jointly with the classifier on

the downstream task. This allows features to adapt to the target domain and task,

often improving accuracy. The risk is overfitting or catastrophic forgetting when the

downstream dataset is small – the backbone may overwrite general representations learned

during pretraining.

When to use each. With abundant labels (≫1000), fine-tuning the last 1–2 blocks

typically yields the best accuracy. With very few labels, linear probing is safer – there are

far fewer trainable parameters and the strong regularisation prevents overfitting.

With 100 labelled examples: linear probing is strongly preferred. Fine-tuning a back-

bone with millions of parameters using 100 examples is an extreme overfitting regime. Lin-

ear probing reduces the problem to fitting dmodel×C classifier weights (e.g., 2048×2 = 4096

for binary classification with ResNet-50), which is feasible with 100 examples and appro-

priate regularisation.

Practical tip: if linear probing performance is insufficient, consider fine-tuning only the

final few layers (partial fine-tuning) with a small learning rate and strong weight decay.

(d) Domain gap.

Pretraining domain matters. Models pretrained on ImageNet learn representations

tuned to natural colour photographs: colour gradients, textures of fur, bark, and fabric,

and shape boundaries of everyday objects. Chest X-rays differ fundamentally: they are

greyscale, the relevant signal is subtle density differences rather than colour or sharp tex-

ture boundaries, and clinically meaningful features (consolidation, nodules) are largely

invisible to features trained for dog/cat classification. Medical-domain pretraining con-

sistently outperforms ImageNet pretraining for downstream medical tasks, even when the

medical pretraining dataset is much smaller. The medical-pretrained model is expected

to perform substantially better.

Key practical benefit. Self-supervised pretraining unlocks the use of large unlabelled

datasets, which are far more readily available in healthcare than labelled ones. Expert

-----

|  |
| :-: |
| [**Page 5**]() |

Deep Learning in Healthcare

Hilary Term 2026

annotation of medical images requires specialist time and is expensive. A model pretrained

on 100,000 unlabelled chest X-rays and fine-tuned on 100 labelled examples can rival a

model trained from scratch on 1,000 labelled examples. This 10× reduction in annotation

burden is often the difference between a feasible and an infeasible clinical AI project.

Key limitation. Pretext task objectives do not guarantee that all task-relevant features

are captured. A model trained on rotation prediction learns orientation-invariant features

and coarse structure, but may not learn to represent subtle density changes indicative of

early pneumonia. Task-aligned pretext tasks (e.g., masked reconstruction of anatomically

meaningful regions, or contrastive learning with augmentations that preserve pathological

appearance) partially mitigate this. Careful ablation – comparing linear probing perfor-

mance of different pretraining approaches on the specific downstream task – is essential

before committing to a pretraining strategy.

-----

|  |
| :-: |
| [**Page 6**]() |

Deep Learning in Healthcare

Hilary Term 2026

3 Adversarial Domain Adaptation

(a) Domain shift.

A model trained at Hospital A optimises its parameters to minimise the loss under Hos-

pital A’s data distribution PA(X, Y ). The learned decision boundary is calibrated for the

feature space induced by Hospital A’s inputs. When deployed at Hospital B with distri-

bution PB(X, Y ), the inputs X are systematically different even if the task (predicting Y

from X) is identical. Sources of shift include: scanner manufacturer (different point spread

functions, noise characteristics), field strength or acquisition protocol (MRI), patient de-

mographics (age, BMI, comorbidities affecting appearance), and disease prevalence (label

shift).

Why performance degrades. The internal activations of the network – the effective

feature representation – shift in mean and variance across domains, even in deep layers.

Batch normalisation statistics computed from Hospital A data are mismatched at Hospital

B (see PS1, Section 5). The model’s decision boundary, which lies in feature space, may

no longer correctly separate classes when features are shifted. A classifier trained to detect

consolidation at a certain feature-space location may no longer fire at the right threshold

for Hospital B’s slightly different feature distribution. Critically, this degradation occurs

silently: accuracy on Hospital A’s test set remains high, providing no warning of the

failure.

Common mistake to avoid: students sometimes argue that because the label-generating

process (pathology) is the same at both hospitals, the model should generalise. This

conflates the true data-generating process with the observed image distribution. The

model has learned to map from images to labels through the lens of Hospital A’s images;

the mapping changes when images change, even if labels remain the same.

(b) Domain adversarial training.

DANN adds a domain discriminator Dd that classifies whether a feature vector F(x) came

from the source or target domain. The combined objective is:

min

F,C

max

Dd

Lclass(F, C) − λLdomain(F, Dd)

Roles of each component.

• Feature extractor F: trained to (i) extract features that are predictive of the class

label (via Lclass) and (ii) confuse the domain discriminator (via −λLdomain, which re-

verses the domain gradient). These two objectives are in tension: task-discriminative

features may also be domain-discriminative.

• Task classifier C: trained to minimise Lclass using source-domain labels only (target

labels are unavailable).

• Domain discriminator Dd: trained to maximise Ldomain, i.e., correctly classify source

vs target features. It acts as the adversary providing signal to F.

Gradient reversal layer (GRL). The GRL sits between F and Dd. During the forward

pass, it is an identity: GRL(h) = h. During the backward pass, it negates and scales the

gradient: ∂GRL/∂h = −λI. This means that gradient steps which would make features

more domain-discriminative (as signalled by Dd) are reversed into steps that make them

less domain-discriminative. The GRL thus implements the minimax objective in a single

forward–backward pass without an alternating optimisation loop, allowing end-to-end

training with standard optimisers.

-----

|  |
| :-: |
| [**Page 7**]() |

Deep Learning in Healthcare

Hilary Term 2026

(c) Domain-invariant features.

Convergence criterion. At convergence (if it is achieved), Dd performs no better

than chance at classifying source versus target features – its accuracy is ≈ 50%. This

means the marginal feature distribution pF (x) is identical across domains: psource(F(x)) ≈

ptarget(F(x)).

Theoretical justification. Ben-David et al. (2010) proved an upper bound on target

risk:

Rtarget(h) ≤ Rsource(h) + dH∆H(psource,ptarget) + λ

∗

where dH∆H is the H-divergence (roughly, how well the best classifier can distinguish

source from target) and λ∗ is the error of the ideal joint hypothesis. DANN directly

minimises dH∆H through the adversarial training. If this divergence is small, the source

risk transfers to the target.

When the assumption fails. The bound also includes λ∗, which is the performance of

the best classifier that simultaneously minimises source and target error. If the domains

have very different label distributions (e.g., Hospital A has 60% pneumonia prevalence,

Hospital B has 20%), the optimal classifiers for the two domains may differ even in a

shared feature space. In this case, aligning marginal feature distributions may hurt: the

adversary can align psource(F) and ptarget(F) by mixing class-conditional distributions,

potentially mapping features from different classes to overlapping regions and corrupting

the classifier.

(d) Limitations and alternatives.

Fundamental limitation of DANN. DANN enforces marginal distribution alignment:

psource(F(x)) ≈ ptarget(F(x)). It does not enforce conditional alignment: psource(F(x)|y) ≈

ptarget(F(x)|y) for each class y. If class prevalences differ between hospitals, marginal

alignment can be achieved by “blending” class-conditional distributions in a way that

destroys class discriminability. Furthermore, DANN requires access to unlabelled target-

domain data during training, which may not always be available at training time.

CORAL vs DANN. CORAL aligns first- and second-order feature statistics (mean and

covariance) between source and target. It operates on the feature layer directly without

adversarial training, making it simpler to implement and more stable (no minimax game).

However, matching second-order statistics is strictly less expressive than matching full

distributions (DANN’s adversary can in principle align distributions of arbitrary com-

plexity). CORAL is effective when domain shift is primarily a mean and covariance shift,

which is common for scanner differences.

MMD vs DANN. MMD minimises a kernel-based measure of distributional distance

between feature distributions. It provides a theoretically principled, smooth surrogate

for distributional distance, with convergence guarantees depending on kernel choice. Im-

plementation is simpler than DANN (single objective, no adversary) but performance is

sensitive to the choice of kernel and bandwidth. Computationally, MMD scales as O(n2)

in the number of samples, whereas DANN scales linearly.

Practical first step: batch normalisation adaptation. Before deployment at Hospi-

tal B, run a small calibration set of unlabelled Hospital B images through the model and

recompute the running mean and variance in each batch normalisation layer (keeping γ

and β fixed). This takes minutes, requires no retraining, and corrects the most significant

distributional mismatch – the feature distribution shift that BN statistics encode. Empir-

ically, this simple step often recovers 50–80% of the performance gap caused by domain

shift.

-----

|  |
| :-: |
| [**Page 8**]() |

Deep Learning in Healthcare

Hilary Term 2026

4 Normalising Flow Models

(a) Change of variables and exact likelihood.

A normalising flow defines an invertible mapping f : Z→X. By the change-of-variables

formula:

log pX(x) = log pZ(f

−1

(x)) + log detJf−1 (x)

where Jf−1 is the Jacobian matrix of the inverse mapping evaluated at x. The first term

is the log-probability of the latent code under the simple base distribution; the second

term corrects for the volume change induced by the transformation.

Why exact likelihood is valuable for anomaly detection. A trained classifier’s

confidence score (e.g., p(arrhythmia|x)) requires labelled anomaly examples to train. In

practice, labelled arrhythmia recordings may be rare, biased towards common types, or

unavailable. A flow model trained only on normal ECGs can compute log pX(x) for

any new recording; a recording with very low log pX(x) is unlikely under the normal

distribution, flagging it for review regardless of the specific anomaly type.

A GAN’s discriminator output D(x) is not a calibrated density: it is trained to output

values near 1 for training-distribution inputs and near 0 for generated inputs, but pro-

vides no principled probability. It may assign high scores to out-of-distribution recordings

simply because they lie far from the generator’s typical outputs. Thresholding log pX(x)

directly corresponds to a likelihood-ratio test, which is the statistically optimal anomaly

detector under a simple null hypothesis.

(b) Invertibility constraints.

Why bijective?

(1) Generation: to sample a new ECG, draw z ∼ pZ and compute x = f(z). Without a

well-defined forward mapping (i.e., without injectivity of f), the same z might map

to multiple outputs, making generation undefined. Without surjectivity, some data

points x would have no latent code.

(2) Likelihood computation: to evaluate log pX(x), we must compute f−1(x) and detJf−1 (x).

Without invertibility, f−1 does not exist.

Tractable Jacobian. For an ECG segment of dimension d = 512, computing the deter-

minant of a general 512 × 512 Jacobian matrix costs O(d3) = O(5123) ≈ 108 operations

per sample – prohibitive for training with thousands of samples. Flows must therefore be

designed so that the Jacobian is triangular: either upper or lower triangular. The deter-

minant of a triangular matrix is the product of its diagonal entries, computable in O(d).

This constraint on the Jacobian structure (rather than the function itself) distinguishes

flow architectures from unconstrained networks. GANs can use arbitrary architectures

precisely because they never need to compute a likelihood or an inverse.

(c) Affine flow layers.

An affine flow layer applies:

yi = exp(si) · xi + ti,

i = 1,...,d

Inverse:

xi = (yi − ti) · exp(−si)

This is obtained directly by rearranging the forward equation. Unlike general neural

network inverses, no iterative solver is needed – the inverse is closed-form and as cheap to

compute as the forward pass.

-----

|  |
| :-: |
| [**Page 9**]() |

Deep Learning in Healthcare

Hilary Term 2026

Log-Jacobian determinant: The Jacobian of the forward transformation is:

∂yi

∂xj

\=

(

exp(si) i = j

0

i ̸= j

i.e., a diagonal matrix with entries exp(si). Its determinant is:

log |detJf | =

d

X

i=1

si

This is O(d) – simply a sum of d learned scalars – compared to O(d3) for a general

transformation. The diagonal structure arises because each output yi depends only on xi:

there is no cross-coupling between dimensions in the Jacobian.

Expressiveness and the need for permutations. A single affine layer transforms

each dimension independently with no interaction. The i-th output depends only on the

i-th input, so no statistical dependencies between dimensions of x can be modelled –

the joint distribution would factorise as a product of marginals. To model a joint ECG

distribution (where adjacent time points are highly correlated), multiple affine layers must

be composed with permutations or invertible linear maps interleaved between them. After

a permutation, what was previously the j-th dimension becomes the i-th, so the next affine

layer effectively transforms dimension j conditioned (via the permutation) on the history

of all previous layers. Stacking many affine–permutation pairs allows the composition to

approximate complex joint distributions.

(d) Comparison with GANs.

Normalising flow

GAN

Likelihood

Exact

None

Sample quality

Moderate

Sharp

Training stability

Stable (MLE)

Unstable (minimax)

Architecture

Constrained (invertible, diagonal Jacobian)

Flexible

Likelihood. Flows compute log pX(x) exactly via the change-of-variables formula. GANs

have no tractable density: they provide a generator G but the probability of a given x

under pG cannot be computed without a separate density estimator.

Sample quality. GAN samples are typically sharper because the adversarial loss di-

rectly minimises a perceptual distance in data space. Flow samples are limited by the

expressiveness of the invertible architecture – a stack of affine layers with permutations

can model complex distributions but may smooth over fine-grained detail.

Training stability. Flows are trained by maximum likelihood, a well-posed single-

objective optimisation with clear convergence criteria. GAN training is a two-player

minimax game prone to mode collapse, vanishing gradients, and oscillation (Section 1).

For ECG anomaly detection, flows are most principled. The exact log-likelihood

log pX(x) provides a calibrated, threshold-based anomaly score: normal ECGs have high

log pX(x); arrhythmic ECGs have low log pX(x). This is the optimal likelihood-ratio test

under a Gaussian null. GANs cannot compute this score; a GAN’s discriminator output

is not calibrated as a probability and would require additional estimation. Furthermore,

flows require no labelled anomaly examples at training time, unlike supervised classifiers

– a critical advantage given the rarity and diversity of arrhythmia types.

-----

|  |
| :-: |
| [**Page 10**]() |

Deep Learning in Healthcare

Hilary Term 2026

Remark: These solutions cover four advanced topics central to modern medical AI. GANs

address data scarcity but require careful validation of synthetic data quality. Self-supervised

learning reduces annotation burden by exploiting large unlabelled datasets. Adversarial domain

adaptation extends models across institutions without requiring target-domain labels. Normal-

ising flows provide exact likelihood-based generative models suited to anomaly detection. In

clinical deployment, all four techniques require rigorous external validation and awareness of

their failure modes.
