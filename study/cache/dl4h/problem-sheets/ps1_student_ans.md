# DL4H — Problem Sheet 1: Student Solutions
> Source: Google Drive file 1h_p6SLCgD9O49cgzgWecnELZQi7hbu_- · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Deep Learning in Healthcare Hilary Term 2026

Problem Sheet 1 – Student Solutions

This guide provides key results and concise explanations for each question. Use it to check your own working and to fill in any gaps in understanding.

1 Backpropagation for medical diagnosis

(a) Chain rule and backpropagation.

The chain rule expression for ∂L/∂W1 is:

∂L ∂W1 = ∂L∂ˆy · ∂ˆy

∂z2 · ∂z2

∂h · ∂h

∂z1 · ∂z1 ∂W1 Each factor corresponds to a derivative through one layer of the network. Backpropagation computes these in reverse order because each layer’s gradient depends on the gradient from the layer above. This avoids redundant recomputation, giving an efficient O(n) algorithm.

(b) Vanishing gradients.

(i) Using the quotient rule on σ(z) = 1+e1 −z:

dσdz = σ(z)(1 − σ(z)) The maximum occurs at z = 0 where σ(z)=0.5:

max z

dσdz = 0.5 × 0.5= 0.25

(ii) Through L sigmoid layers, the For L = 10: (0.25)10 ≈ 10−6. gradient is multiplied by σ′(zℓ) ≤ 0.25 at each layer. The gradient shrinks exponentially with depth, pre- venting early layers from learning. This is the vanishing gradient problem. (iii) ReLU has derivative 1 for z \> 0 and 0 for z \< 0. For active neurons, gradients pass through unchanged, enabling gradient flow through arbitrarily deep networks. This was a key enabler for architectures like ResNets.

(c) Dead ReLU problem.

(i) With zi = −2.5: hi = ReLU(−2.5) = 0 and upstream error signal.

∂h∂zi i = 0, so ∂L ∂wi = 0 regardless of the

(ii) If the pre-activation is negative for all training examples, the gradient is always zero and the weights never update. The neuron is permanently “dead” and cannot recover. This can occur with poor initialisation or if the bias becomes too negative during training. (iii) Leaky ReLU has derivative α \> 0 (typically 0.01) for z ≤ 0. Even when zi \< 0,

gradients still flow (scaled by α), so neurons can never become permanently dead.

Deep Learning in Healthcare Hilary Term 2026

2 Optimisation and ill-conditioned losses

(a) The gradient is ∇L = (w1,20w2)⊤. At w = (1,1)⊤: ∇L = (1,20)⊤. The gradient in w2

is 20 times larger, reflecting the much higher curvature in that direction.

(b) The Hessian is H = diag(1,20), with eigenvalues λ1 = 1 and λ2 = 20.

Condition number: κ = λmax/λmin = 20 . A high condition number means the optimal step size differs dramatically by direction, forcing gradient descent to use a conservatively small learning rate and converge slowly.

(c) For convergence, we need |1−αλi| \< 1 for both eigenvalues, giving α \< 2/λi. The binding

constraint is the largest eigenvalue:

α \< 220 = 0.1 With this learning rate, progress along w1 is very slow (αλ1 = 0.1).

(d) Momentum averages past gradients. In the high-curvature direction (w2), oscillating gradi- ents partially cancel, damping oscillations. In the low-curvature direction (w1), consistent gradients reinforce each other, increasing effective step size. Momentum acts as a low-pass filter: dampening oscillations while amplifying consistent signal. (e) Adam tracks per-parameter squared gradient averages vi and scales updates by 1/√vi. Directions with large gradients (high curvature) get smaller effective learning rates; direc- tions with small gradients (low curvature) get larger ones. Key difference from momentum: Adam directly normalises step sizes per coordinate, effectively giving each parameter its own adaptive learning rate. Momentum dampens oscillations through temporal averaging but does not explicitly compensate for curvature differences.

3 Bias-variance trade-off in medical DL

(a) Model A (100 params, 60%/58%): High bias, low variance (underfitting).

Model B (10K params, 85%/82%): Moderate bias, low variance (well-balanced). Model C (1M params, 98%/75%): Low bias, high variance (overfitting).

(b) Model A is underfitting; Model B is well-balanced; Model C is overfitting.

(c) Strategy 1: Data augmentation – random transformations (rotations, flips, inten- sity variations) artificially increase the effective dataset size, preventing the model from memorising specific pixel patterns and forcing it to learn robust features. Strategy 2: Dropout – randomly zeroing neurons during training prevents co-adaptation and acts as an implicit ensemble, reducing effective capacity without changing the archi- tecture.

(d) (i) Under the 10-examples-per-parameter heuristic: 10 × 1,000,000 = 10,000,000 la-

belled examples. (ii) The dataset has only 1,000 examples, which is 10,000 times fewer than required. Large medical imaging datasets rarely exceed 10,000 examples due to annotation costs. Training models with millions of parameters from scratch on medical data is fundamentally infeasible.

Deep Learning in Healthcare Hilary Term 2026

(iii) Transfer learning pre-trains on a large natural image dataset (e.g., ImageNet). Gen- eral visual features (edges, textures, shapes) transfer to medical images. Fine-tuning freezes early layers and trains only the final layers on medical data, reducing the effective number of trainable parameters from 1M to roughly 10K–100K. This makes it feasible to train powerful models with only thousands of medical examples.

4 Architecture design under memory constraints

(a) Fully connected design.

(i) Parameters in a fully connected layer: nout(nin + 1). (ii) For input (784) → hidden (h) → output (10): total parameters = 795h+10 ≤ 50,000. Solving: h ≤ 49,990/795 ≈ 62.88. Maximum hidden units: h = 62 , giving 49,300 parameters.

(b) Convolutional design.

(i) Parameters in a convolutional layer: Cout(Cin · k2 + 1). (ii) Example design with 3×3 convolutions and 2×2 max-pooling:

Layer Output size Params Input 28 × 28 × 1 0 Conv1: 1 → 16, 3×3 28 × 28 × 16 160 MaxPool 2×2 14 × 14 × 16 0 Conv2: 16 → 32, 3×3 14 × 14 × 32 4,640 MaxPool 2×2 7 × 7 × 32 0 Flatten 1568 0 FC: 1568 → 10 10 15,690 Total 20,490

Well under the 50,000 budget, with room for a third convolutional layer if desired.

(c) The CNN uses fewer than half the parameters yet provides far greater representational

capacity, thanks to:

Weight sharing: Each filter is applied at every spatial location. Conv1 uses 160 param- eters but produces 12,544 activations.

Translation equivariance: A feature detector learned in one location works everywhere, whereas an FC network must learn the same pattern independently for each position.

Hierarchical features: Convolutional layers compose edges into textures and shapes. The CNN would significantly outperform the FC network on image classification.

5 Batch normalisation in clinical deployment

(a) Domain shift and deployment.

Deep Learning in Healthcare Hilary Term 2026

(i) Batch normalisation stores running statistics (µ, σ2) from Hospital A’s data. If Hospital B has different demographics, imaging protocols, or disease prevalence, the activation distributions will differ. Normalising with Hospital A’s statistics shifts activations to incorrect ranges, degrading performance even if the clinical task is identical. (ii) Mitigations include: training on multi-site data; recomputing running statistics on a calibration set from Hospital B before deployment; and using alternatives like Group Normalisation or Layer Normalisation, which compute statistics per-example and are less sensitive to distributional shift.

(b) Training vs inference behaviour.

(i) With a single test example, the batch mean equals the input value and the batch

variance is zero. (ii) Substituting: ˆzi = (zi − zi)/√0 + ϵ = 0. Every normalised activation becomes zero,

regardless of the input. (iii) This destroys all information; the model outputs the same prediction for any input. Using running (population) statistics avoids this by normalising relative to the train- ing distribution, preserving meaningful activation magnitudes. This is why models must be switched to “eval mode” at inference time.

(c) Small-batch clinical training.

(i) With very small batches (e.g., 2–4 for 3D volumes), batch statistics are highly noisy, leading to: training instability, poor running statistics for inference, and a mismatch between noisy training-time and stable inference-time normalisation. (ii) Group Normalisation divides channels into groups and normalises within each group per example. Batch size is irrelevant, no running statistics are needed, and behaviour is identical at train and test time. It is now standard in medical imaging architectures such as nnU-Net.

(d) Effect on optimisation.

(i) Batch normalisation standardises pre-activations to approximately zero mean and unit variance. This controls activation scale, stabilises gradients, and reduces sensi- tivity to weight initialisation. (ii) Stable activations and gradients allow larger learning rates (empirically 10–30×

larger) and smoother loss landscapes, accelerating convergence. (iii) The original “internal covariate shift” hypothesis proposed that BatchNorm helps by stabilising layer input distributions. However, Santurkar et al. (2018) showed the primary benefit is smoothing the loss landscape, making it more Lipschitz and better-conditioned, which allows larger learning rates and more predictable gradient steps.
