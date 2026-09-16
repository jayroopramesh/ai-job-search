# DL4H — Problem Sheet 4: Student Solutions
> Source: Google Drive file 1x-VVa6ywD-xiSiMCE15m2it4Eo2gM79X · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Deep Learning in Healthcare Hilary Term 2026

Problem Sheet 4 - Student Solutions

Federated Learning, Privacy, Sequence Models & Transformers

This guide provides key results and concise explanations for each question. Use it to check your own working and to fill in any gaps in understanding.

1 Federated Learning for Multi-Hospital Collaboration

(a) Weighted aggregation in FedAvg.

FedAvg computes the weighted average wglobal = Pk(nk/n)wk. With hospitals contribut- ing 1000, 500, 2000, and 500 samples respectively, Hospital 3 receives weight 50%.

Why weighted averaging is preferred: the weighted average is mathematically equiv- alent to training on the pooled centralised dataset (each patient sample contributes equally). Simple (uniform) averaging over-represents smaller hospitals: Hospital 2 (500 samples) would have equal influence as Hospital 3 (2000 samples), biasing the global model and harming statistical efficiency. Weighted averaging also has theoretical con- vergence guarantees (to the centralised optimum under IID assumptions), while simple averaging does not.

Simple averaging may be preferred for institutional fairness (equal vote per hospital regard- less of size) or when data quality varies and smaller hospitals actually have higher-quality labels. (⋆ Challenge) Convergence of FedAvg. With w∗1 = 1.0, w∗3 = 2.5, n1 = 1000, n3 = 2000: (i) Global minimiser: w∗ = 1000×1.0+2000×2.5 3000 = 2.0. (ii) E = 1, η = 1 from w(0) = 0: each hospital reaches its local optimum in one step (w(1)

k = w∗k). Uniform average: 12(1.0+2.5) = 1.75 = 2.0. Proportional average: 13(1.0) + 23(2.5) = 2.0 = w∗. Only proportional averaging recovers the global minimiser. (iii) E = 2, η = 0.5 from w(0) = 0: Hospital 1: w(2)

1 = 0.75; Hospital 3: w(2)

3 = 1.875. Proportional average: 13(0.75)+ 23(1.875) = 1.5 = 2.0. Even with correct weighting, E \> 1 introduces bias because each hospital is only 75% converged to its local optimum. Aver- aging partially-converged local models systematically undershoots the global optimum - this is the quantitative signature of client drift.

(b) Non-IID data and client drift.

When hospitals have different patient demographics, disease prevalence, and imaging pro- tocols, each hospital’s local objective Lk differs from the global objective Lglobal. Local updates from Hospital 1 (elderly, 60% pneumonia prevalence) and Hospital 2 (paediatric, 20% pneumonia prevalence) point in conflicting gradient directions. Aggregating these updates produces a compromise that may not optimise any individual hospital’s task well. This is client drift: each client’s model drifts toward its local optimum during local training, pulling the global model in conflicting directions.

Deep Learning in Healthcare Hilary Term 2026

Formally, the variance of ∇Lk across hospitals increases with data heterogeneity, making the aggregated gradient a poor estimate of ∇Lglobal and slowing or preventing convergence.

(c) Local vs federated model performance.

When tested on Hospital 2’s paediatric test set, the federated model (4000 training sam- ples) most likely outperforms the local model (500 samples) for three reasons:

Data quantity: 8× more training data substantially reduces variance and overfitting risk. With only 500 samples, the local model risks memorising training-specific patterns.

Transferable features: pneumonia features (consolidation, infiltrates, airspace opaci- ties) are broadly similar across age groups. Data from adult hospitals contributes useful general visual representations.

Implicit regularisation: diverse training data discourages overfitting to dataset-specific artefacts.

The local model could outperform if paediatric pneumonia has highly disease-specific fea- tures not shared with adult presentations, or if negative transfer from adult data actively harms paediatric performance. In practice, federated models typically benefit all partici- pating hospitals, even on their own local test distributions.

(d) Mitigating non-IID data.

Data sharing (small public dataset): create a small shared dataset (e.g., 25 represen- tative samples from each hospital, 100 total) that all hospitals include in local training. This provides a common anchor, reducing distributional divergence and aligning local objectives. Effective (empirically 20-30% improvement) but requires data sharing, which may conflict with privacy regulations (GDPR, HIPAA) or patient consent frameworks.

FedProx (proximal regularisation): add a penalty term to each hospital’s local ob- jective:

min wk Lk(wk) + µ2∥wk − wglobal∥2 This prevents local models from drifting too far from the global model, reducing client drift. No data sharing is required. The hyperparameter µ controls the trade-off between local specialisation and global consensus (typical values 0.01-1.0). FedProx is provably convergent under non-IID conditions.

Recommendation: try FedProx first (no privacy cost and no data sharing). If per- formance is insufficient, consider a small public dataset with appropriate consent and de-identification.

2 Differential Privacy for Medical Data

(a) Why exact counts do not satisfy differential privacy.

Let D contain 250 diabetic patients and D′ differ by the addition of one diabetic patient. Releasing true counts gives M(D) = 250 and M(D′) = 251 deterministically. For the set S = {250}:

P(M(D) ∈ S)=1, P(M(D′) ∈ S)=0 =⇒ 1 ≤ eε · 0

which is false for any finite ε. An attacker who knows whether a specific patient was in D or D′ can infer their diabetes status with 100% confidence from the output. Randomisation is essential: no deterministic output that depends directly on individual records can satisfy differential privacy.

Deep Learning in Healthcare Hilary Term 2026

(b) Sensitivity of counting queries.

The sensitivity of a query f is ∆f = maxD,D′ differ by 1 |f(D)−f(D′)|. Adding or removing one patient changes the count by at most ±1 (adding a diabetic patient increases the count by 1; adding a non-diabetic patient leaves it unchanged). Therefore ∆f = 1 for any counting query.

Adding Laplace noise Lap(∆f/ε) to the true count achieves ε-DP. With ε = 0.1, the noise scale is b = 10, giving a 95% confidence interval of approximately ±23 around the true count of 250 - roughly 9% relative error.

(c) Privacy-utility trade-off.

ε = 0.1 (strong privacy): noise scale b = 10, 95% CI ≈ ±23. The ratio of output probabilities for any two neighbouring databases is at most e0.1 ≈ 1.1, so an attacker’s posterior belief about any individual shifts by at most 10%. Suitable for highly sensitive data (HIV status, genetic records) but poor utility for detecting fine-grained trends.

ε = 10 (weak privacy): noise scale b = 0.1, 95% CI ≈ ±0.3 (near-exact utility). The probability ratio bound is e10 ≈ 22,000, providing almost no privacy protection. Suitable only for non-sensitive aggregate statistics.

Composition: privacy degrades with multiple queries on the same data. Under basic composition, k queries each at ε give total privacy loss kε. A privacy budget must be maintained and allocated across all analyses on the dataset.

(d) DP-SGD: gradient clipping and privacy budget.

Why clip gradients: individual sample gradients gi may have arbitrary norm, making the sensitivity of the batch sum unbounded. Clipping to ∥¯gi∥ ≤ C bounds sensitivity at C, enabling calibrated Gaussian noise N(0,σ2C2I) to be added for DP. Without clipping, an outlier sample with ∥gi∥ = 100 would dominate the gradient, making it trivial for an adversary to detect that patient’s presence.

Choice of C: small C reduces sensitivity (less noise needed) but distorts gradient direc- tions. Large C preserves gradient fidelity but requires more noise. In practice, C is set so that Privacy loss after 50-80% T budget gradient of gradients grows steps are scales as clipped.

√T: as O(by √the T). advanced Training composition for 100 epochs theorem, instead of total 10 roughly privacy

triples batches ε. improve This forces the signal-to-noise early stopping ratio or short by √fine-tuning B (the signal on a averages pretrained over model. more samples Larger

while the noise magnitude stays fixed), enabling convergence in fewer steps and conserving privacy budget.

3 LSTM Networks and Recurrent Architectures for Clinical

Time Series

(a) Vanishing gradients in vanilla RNNs.

In a vanilla RNN, ht = tanh(Whhht−1 + Wxhxt). The gradient of the loss with respect to the hidden state at time step 0 involves the product:

∂L ∂h0 =

YTt=1\! Whh ⊤· diag(tanh′(zt))∂L ∂hT

Deep Learning in Healthcare Hilary Term 2026

Since tanh′(z) ≤ 1 and the spectral norm of Whh is typically less than 1 after training, this product of matrices shrinks exponentially with T. For clinical sequences of length 100 (e.g., 100 hourly ICU readings), gradients reaching early time steps are effectively zero. The RNN can learn short-range patterns but cannot discover that features from many hours ago predict current outcomes - making it fundamentally inadequate for tasks like early sepsis detection.

(b) LSTM gating mechanism.

The LSTM addresses vanishing gradients through a cell state ct updated additively rather than through a weight matrix multiplication:

ct = ft ⊙ ct−1 + it ⊙ ˜ct

The forget gate ft = σ(Wf\[ht−1;xt\] + bf) controls how much of the previous cell state to retain. The input gate it controls what new information to write; the candidate state ˜ct = tanh(Wc\[ht−1;xt\]+bc) produces that new information. The output gate ot controls what the cell state exposes to ht = ot ⊙ tanh(ct). Because the cell state update is additive, when ft ≈ 1 gradients flow back through time with ∂cT/∂c0 ≈ 1: a “gradient highway” through the network. The four separate gate matrices allow the LSTM to learn specialised memory policies impossible for a vanilla RNN’s single weight matrix.

(c) Forget gate initialisation and dynamics.

With bf state each = 0 and small initial weights, ft ≈ σ(0) = 0.5, so the LSTM forgets 50% of its cell step. Information vanishes as (0.5)T. Initialising bf to 1-2 gives ft ≈ 0.73-0.88, enabling information to persist until the network learns what to forget.

Scenario 1 (gradual heart rate trend): the LSTM should remember (ft ≈ 1). Each individual reading is within the normal range; only the accumulated trend over 8 hours signals potential sepsis. Scenario 2 (extubation event): the LSTM should forget (ft ≈ 0). The patient’s phys- iology has fundamentally changed and baselines from mechanical ventilation are no longer relevant. A fixed exponential decay rate cannot achieve both behaviours simultaneously - this is precisely why learned gating is essential.

(d) Gradient flow and comparison with alternative architectures.

Feedforward network (1-hour window): can only access the most recent 60 observa- tions. Critical 8-12 hour trends are simply not available as inputs. First-order Markov model: only the immediately preceding observation matters at each step. Multi-hour patterns are fundamentally unrepresentable regardless of model capacity.

LSTM (24-hour history): when ft ≈ 1:

∂cT ∂c0 =

YTt=1diag(ft) ≈ I

Gradients flow back through time without vanishing, so the network can learn that read- ings from 12 hours ago are predictive. The LSTM’s advantage is not merely seeing more data: it is the learned, selective memory and stable gradient flow that enable it to discover which long-range patterns matter. A colleague who argues LSTMs must overfit due to having ≈ 4× the parameters of a vanilla RNN conflates redundant capacity with necessary capacity. The RNN cannot represent

Deep Learning in Healthcare Hilary Term 2026

solutions requiring long-range memory, regardless of dataset size: this is underfitting, not good generalisation. For small clinical datasets, regularisation (dropout, weight decay) controls LSTM overfitting while preserving its structural advantages.

4 Self-Attention and Transformers for Medical Text (Optional)

(a) Attention score computation.

Given the “shortness” row of pre-softmax scores \[0,1,8,6\], apply softmax:

exp(\[0,1,8,6\]) = \[1,2.72,2981,403\] =⇒ ashortness ≈ \[0.000,0.001,0.880,0.119\]

“Shortness” attends most strongly to itself (88%) and secondarily to “breath” (12%), correctly capturing “shortness of breath” as a single semantic unit (dyspnoea). Unre- lated tokens (“fever”, “cough”) attend almost exclusively to themselves, reflecting their independence as separate symptoms.

Bidirectional vs causal attention: summarisation requires understanding the complete document before generating output - use bidirectional attention (BERT-style). Next-word prediction can only use preceding context - use a causal mask that blocks attention to future positions (GPT-style). (b) Scaling factor 1/√dk.

Dot products q·k have variance dk (a sum of dk unit-variance terms). For dk = 64, typical magnitudes are ±3√64 = ±24. At such scales, softmax becomes nearly one-hot and its gradient vanishes: ∂ softmaxi /∂zi = softmaxi(1 − softmaxi) ≈ 0. Dividing by √dk normalises the variance to 1 regardless of dk, keeping softmax in a regime with meaningful gradients and allowing attention weights to be distributed across multiple tokens rather than concentrating on one.

(c) Self-attention vs RNNs.

Complexity: self-attention is O(n2d) (all pairwise scores); RNNs are O(nd2) (sequential matrix products). Self-attention is faster for n\<d, typical for clinical notes (n ∼ 100-500 tokens, d ∼ 512).

Parallelism: self-attention is fully parallelisable across the sequence - all scores are com- puted simultaneously as matrix operations. RNNs are inherently sequential (ht depends on ht−1), giving 5-10× slower wall-clock time on GPU despite comparable FLOPs. Long-range dependencies: self-attention has a path length of 1 between any two tokens - no information degradation with distance. RNN path length is n; even LSTMs struggle over very long sequences. For clinical text where “history of diabetes” in the first sentence affects interpretation of “wound healing complications” at the end, self-attention’s direct token-to-token connections are strongly preferable.

(d) Multi-head attention.

With h = 8 heads and dk = dv = 64: each head uses 512 × 64 = 32,768 parameters per projection. 8 heads × 3 projections gives 786,432 parameters, plus 512 × 512 = 262,144 for the output projection - roughly the same total as single-head attention at full dimensionality (dk = 512). The computation is also equivalent since h × dk = 512.

Deep Learning in Healthcare Hilary Term 2026

Each head operates on a different linear projection of the input and can specialise. In a clinical note example, one head may capture syntactic structure (verb-object relation- ships), another drug-disease relationships (metformin → diabetes), and another dosage- drug associations (500mg → metformin). No single head could capture all these rela- tionship types simultaneously. The output projection combines all heads, enabling joint reasoning across multiple types of relationship.
