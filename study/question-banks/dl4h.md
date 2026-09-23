# Question Bank — DL4H · [OXFORD]
<!-- Appended by tutor sessions. Format: see README.md. Seeded from Day 1 baseline onward. -->

### QB-DL4H-0001 · [OXFORD] · complete the sentence · L2 p.2 · first asked 2026-09-17
Q: "Training a neural network means minimising a loss over the data. The formal name for this principle is ______."
A: **Empirical risk minimisation** — minimising expected loss under the empirical data distribution, standing in for the true risk. (Maximum likelihood is related but narrower: it is what ERM reduces to for particular loss/noise pairings, e.g. cross-entropy.)
Asked: 2026-09-17 🟡 (answered "maximum likelihood estimation")
Linked flag: FP-7

### QB-DL4H-0002 · [OXFORD] · open · L2 p.15–16 · first asked 2026-09-17
Q: Every loss encodes a noise model. Which noise does L2 assume, which does L1 assume, and why does MSE let outliers dominate?
A: L2 ↔ **Gaussian** noise; L1 ↔ **Laplace** noise; cross-entropy ↔ **categorical uncertainty**. "Choosing a loss is choosing which errors are plausible." MSE squares the residual, so a point 10× further out contributes 100× the loss and dominates the gradient — Gaussian tails are thin, so the loss treats a large residual as near-impossible and strains to fix it.
Asked: 2026-09-17 ❌ ("no idea")
Linked flag: FP-6

### QB-DL4H-0003 · [OXFORD] · structural · L2 p.22 · first asked 2026-09-17
Q: Dice = 2TP / (2TP + FP + FN). For a scan with many false positives, which of precision and recall is damaged, and which is untouched?
A: Precision is damaged (FP is in its denominator: TP/(TP+FP)). Recall is untouched — FP appears nowhere in TP/(TP+FN); only false negatives move recall. Dice is hurt by both, which is why it behaves like a balance of the two.
Asked: 2026-09-17 ❌ (said false positives affect recall)
Linked flag: FP-4, FP-5

### QB-DL4H-0004 · [OXFORD] · open · L2 p.20 · first asked 2026-09-17
Q: Why were overlap-based losses like Dice proposed for segmentation instead of plain pixel-wise cross-entropy?
A: **Class imbalance.** Pixel-wise CE is summed over every pixel, and in a large scan the background vastly outnumbers a small structure — so the total is dominated by the sheer *count* of easy background pixels (each contributing a small loss), and predicting "all background" already scores well. Overlap losses measure agreement on the structure itself, so a small tumour still carries weight.
Asked: 2026-09-17 🟡 (core insight correct — small tumour drowned out — but said CE is "high for all the parts that match"; CE is *low* where prediction matches, it is their number that dominates)
Linked flag: FP-5

### QB-DL4H-0005 · [OXFORD] · pre-test → taught · L1 · asked 2026-09-18
Q: Namburete opens with "unique data, unique challenges." What makes medical data harder than a natural-image dataset like ImageNet? Two challenges is enough.
A: Two layers. **The data**: many modalities and formats in one patient record (MRI, ultrasound, EEG, vital signs, lab results, genomics, wearable/patient-generated data), and the same signal means different things across modalities — there is no single "image" to learn from. **The open challenges** the deck names: *bias and fair representation* (equal performance regardless of patient demographic), *explainability* (can the decision process be interpreted?), and *privacy and security* (medical data is sensitive and personally identifying, not easily shared, protected by legislation such as GDPR). The last one also motivates federated learning in L13.
Asked: 2026-09-18 ❌ ("no idea")
Linked flag: FP-6-adjacent; own ledger item

### QB-DL4H-0006 · [OXFORD] · forced choice + pairing (FP-6 new angle) · L2 p.15–16 · asked 2026-09-18
Q: Regression targets contain large outliers. Which loss treats a big residual as nearly impossible and contorts the fit to chase it — L1 or L2? And which noise distribution is each assuming?
A: **L2.** It squares the residual, so a point 10× further out contributes 100× the loss and dominates the gradient. The assumption underneath: L2 ↔ **Gaussian** noise, whose tails are thin, so a large residual is treated as near-impossible and worth great effort to remove. L1 ↔ **Laplace** noise, whose heavier tails make a large residual merely unusual — which is exactly why L1 is the robust choice. Cross-entropy ↔ categorical uncertainty.
Asked: 2026-09-18 🟡 (L2 + Gaussian correct; L1 ↔ Laplace missing, and no account of why thin tails cause the contortion)
Linked flag: FP-6, FP-5

### QB-DL4H-0007 · [OXFORD] · reverse flashcard (FP-7 drill) · L2 p.2 · asked 2026-09-18
Q: Name the principle: minimising the average loss over your training sample as a stand-in for the loss you actually care about. What are you replacing with what?
A: **Empirical risk minimisation.** The substitution: the **true risk** — the expected loss over the real data distribution, which you cannot compute because you never see the distribution — is replaced by the **empirical risk**, the average loss over the finite sample you happen to hold. The whole edifice rests on that sample resembling what the model will meet in deployment; the deck flags this as the lecture's "implicit assumptions", and in healthcare it is where distribution shift between hospitals bites.
Asked: 2026-09-18 🟡 (named correctly — the same item he answered "MLE" to on D1, so the FP-7 substitution habit is fixed — but the substitution itself not articulated)
Linked flag: FP-7 (1/3), FP-9

<!-- PS1 mining pass, 2026-09-23. Source: Problem Sheet 1 (Hilary Term 2026), questions
     `1WYpUwHEUSISQcwhRAEPnpufUwR8Hust_`, full worked solutions `1nFfztScT7a2Hxv8_5lN9GPOyA_sAAajL`.
     Held in reserve — NOT yet posted; the standing queue was at 5 when these were written. -->

### QB-DL4H-0008 · [OXFORD] · structural formula-reading · PS1 Q1(b) · not yet asked
Q: The sigmoid derivative is $\sigma'(z)=\sigma(z)\,(1-\sigma(z))$, and it peaks at $z=0$ where $\sigma=0.5$. Backpropagating through $L$ sigmoid layers multiplies one such factor per layer. **Point at what makes depth fatal here** — and say in one line why ReLU does not have the same problem.
A: The peak value is $0.5\times0.5=\mathbf{0.25}$ — so **every** layer multiplies the gradient by *at most* a quarter, never more. Through $L$ layers the gradient carries $(0.25)^L$; at $L=10$ that is $\approx10^{-6}$. The killer is that the factor is bounded **below 1**, so the shrinkage compounds and early layers stop learning — the vanishing gradient problem. ReLU's derivative is exactly **1** for $z>0$, so active neurons pass the gradient through unattenuated: nothing compounds, and depth stops being a penalty. That is what made very deep nets (ResNets) trainable.

### QB-DL4H-0009 · [OXFORD] · mechanism-only (FP-9 drill) · PS1 Q1(c) · not yet asked
Q: A neuron sits at $z_i=-2.5$. Its gradient is $\dfrac{\partial L}{\partial w_i}=\dfrac{\partial L}{\partial h_i}\cdot\dfrac{\partial h_i}{\partial z_i}\cdot\dfrac{\partial z_i}{\partial w_i}$. **Which factor is zero, and why can no amount of upstream error rescue it?**
A: The **middle** factor. $h_i=\mathrm{ReLU}(-2.5)=0$ and ReLU's derivative is $0$ for $z<0$, so $\partial h_i/\partial z_i=0$. It sits in a **product**, so a zero there annihilates the whole thing no matter how large $\partial L/\partial h_i$ is — the upstream error cannot reach the weight. If $z_i$ stays negative for every training example the weight never updates and the neuron is permanently **dead**. Leaky ReLU fixes it by making that middle factor $\alpha>0$ instead of $0$, so the product is never forced to zero.

### QB-DL4H-0010 · [OXFORD] · forced-choice direction (FP-5 drill) · PS1 Q2(b)(c) · not yet asked
Q: A loss has Hessian $H=\mathrm{diag}(1,20)$, so $\kappa=\lambda_{\max}/\lambda_{\min}=20$. Stability needs $\alpha<2/\lambda_i$ in every direction. **Which eigenvalue sets the ceiling on the learning rate, and which direction is then left crawling?**
A: The **largest**, $\lambda_2=20$, sets the ceiling: $\alpha<2/20=0.1$. It binds because the steep direction diverges first. But that same $\alpha$ has to serve the flat direction too, where the effective step is $\alpha\lambda_1=0.1\times1=0.1$ — tiny. So the steep direction dictates the rate and the **flat** direction ($w_1$) crawls along the valley floor. One knob, two incompatible demands: that is what an ill-conditioned loss costs you.

### QB-DL4H-0011 · [OXFORD] · compare + mechanism · PS1 Q2(d)(e) · not yet asked
Q: Momentum and Adam both help on the loss above. **What does each actually do to the two directions, and what is the one difference that matters?**
A: **Momentum** averages past gradients. In the steep direction the gradients keep flipping sign as you bounce across the valley, so averaging **cancels** them and damps the oscillation; in the flat direction they all point the same way, so averaging **reinforces** them. It is a low-pass filter on the gradient. **Adam** accumulates squared gradients $v_i$ and divides the step by $\sqrt{v_i}$: large-gradient directions get scaled **down**, small-gradient directions **up**. The difference: Adam gives every coordinate its **own** learning rate, attacking the conditioning directly; momentum only smooths over time and never compensates for the curvature mismatch.

### QB-DL4H-0012 · [OXFORD] · structural formula-reading · PS1 Q5(b) · not yet asked
Q: Batch normalisation computes $\hat z_i=\dfrac{z_i-\mu_B}{\sqrt{\sigma_B^2+\epsilon}}$. A model is run on **one** test example. **Read the numerator and say what every activation becomes** — then what that does to the model's output.
A: With a batch of one, $\mu_B=z_i$ — the mean *is* the value. So the numerator is $z_i-z_i=\mathbf{0}$, and $\hat z_i=0/\sqrt{\epsilon}=0$ for **every** activation, whatever the input. All information is destroyed and the model returns the **same prediction for any input**. The fix is the running (population) statistics gathered over training, which normalise relative to the training distribution and preserve differences between activations — which is why a model must be switched to **eval mode** at inference.

### QB-DL4H-0013 · [OXFORD] · interview-style, clinical deployment · PS1 Q5(a) · not yet asked
Q: A model trained at Hospital A is deployed at Hospital B and degrades, though the clinical task is identical. **What exactly is stored inside batch normalisation that breaks** — and name the architectural fix that removes the dependency altogether. Follow-up: why does that fix also survive a batch size of 2?
A: BatchNorm stores **running $\mu$ and $\sigma^2$ estimated from Hospital A's data**, and uses those fixed numbers at inference. Different demographics, scanners or case mix shift Hospital B's activation distribution, so A's statistics normalise it into the **wrong range** and every downstream layer receives out-of-distribution input. Mitigations: train multi-site; recompute the running statistics on a calibration set from B. **Architectural fix: Group Normalisation** (or Layer Norm) — it normalises within channel groups **per example**, so there are no cross-batch statistics to carry over and nothing about Hospital A is baked in. Follow-up: because the statistics never involve the batch dimension at all, batch size is irrelevant — it behaves identically at size 2 or 200, and identically at train and test time. That is why it is standard in medical imaging (nnU-Net), where 3D volumes force tiny batches.

