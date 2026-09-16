# DL4H — Problem Sheet 4
> Source: Google Drive file 1p6MlrVzIyanQW7xj2Ym4_DPtFq6uXUIN · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Deep Learning in Healthcare Hilary Term 2026

Problem Sheet 4 Federated Learning, Privacy, Sequence Models & Transformers

1 Federated Learning for Multi-Hospital Collaboration

Federated Learning (FL) enables multiple hospitals to collaboratively train a shared model without sharing raw patient data. Each hospital trains locally on its data and only shares model updates with a central server.

FedAvg Algorithm:

1\. Server: Initialise global model wglobal 2. For each round t:

• Server broadcasts wglobal to all hospitals

• Each hospital k trains locally for E epochs on nk samples

• Hospital k computes updated weights wk

• Server aggregates: wglobal = PKk=1 nkn wk where n = Pk nk Scenario: Four hospitals collaborate to train a pneumonia detection model:

• Hospital 1: 1,000 patients (mostly elderly, \>65 years; 60% pneumonia prevalence)

• Hospital 2: 500 patients (paediatric, \<18 years; 20% prevalence)

• Hospital 3: 2,000 patients (general population, mixed ages; 30% prevalence)

• Hospital 4: 500 patients (rural, limited imaging quality; 40% prevalence)

Each hospital trains for 5 local epochs per round.

(a) Weighted aggregation in FedAvg.

(i) Hospital 3 contributes 50% of the total data while Hospital 2 contributes 12.5%. Explain the rationale for weighted averaging (proportional to nk) versus simple (uni- form) averaging. Under what circumstances might simple averaging be preferred? (ii) After local training, Hospital 3’s weights diverge significantly from the initial global model, while Hospital 4’s weights change little. If all hospitals are weighted equally, what problem might arise? Relate your answer to the convergence guarantees of FedAvg. (iii) (⋆ Challenge) Convergence analysis of FedAvg. Consider a simplified two- hospital version of the scenario: Hospital 1 (n1 = 1,000) and Hospital 3 (n3 = 2,000). Each hospital minimises a one-dimensional quadratic loss Fk(w) = 12(w−w∗k)2, where w∗1 = 1.0 and w∗3 = 2.5 reflect their different patient populations. The global objective is F(w) = n1n F1(w) + n3n F3(w) with n = 3,000.

• Show that the global minimiser is w∗ = 2.0.

• Suppose E = 1 local gradient step with learning rate η = 1 from w(0) = 0. Show that each hospital reaches its local optimum in one step. Compute the aggregated weight under (A) uniform averaging and (B) proportional averaging, and determine which recovers w∗.

Deep Learning in Healthcare Hilary Term 2026

• Now suppose E = 2 steps with η = 0.5 from w(0) = 0, using the update wcompare k (t+1)

\= to wk (t)

w∗− . η(wWhat k (t)

− does wk∗). this Compute reveal about the proportionally-averaged the effect of multiple local result epochs and

on convergence?

(b) Non-IID data and client drift. Each hospital’s data has different characteristics in terms of patient demographics, disease prevalence, and imaging equipment. Explain why this data heterogeneity causes FedAvg to converge more slowly or to a worse solution compared to IID data. Define the concept of “client drift” and explain it in terms of the local gradient directions at each hospital.

(c) Local vs federated model performance. Compare the expected test accuracy on Hos- pital 2’s paediatric test set between: (i) the federated model trained on all four hospitals, and (ii) a model trained only on Hospital 2’s 500 local samples. Which is likely to perform better and why? Under what conditions might the local model outperform the federated model?

(d) Mitigating non-IID data. Propose two techniques to address the non-IID challenge in federated learning. For each technique, describe the mechanism, the key hyperpa- rameter(s) or design choices, any privacy implications, and when you would recommend it.

Clinical Context: Federated learning enables hospitals to build more robust models by leveraging diverse patient populations while maintaining data privacy and satisfying regulatory restrictions on data sharing. However, heterogeneity across hospitals - in patient demographics, imaging protocols, and disease prevalence - poses significant challenges for model convergence and fairness.

2 Differential Privacy for Medical Data

Differential privacy (DP) provides rigorous mathematical guarantees that analyses on datasets do not reveal information about individual patients. This is especially important for DL in healthcare, where patient privacy must be protected by law (HIPAA, GDPR).

Formal Definition

An algorithm M satisfies ε-differential privacy if for all datasets D, D′ differing in one record, and all possible outputs S:

P(M(D) ∈ S) ≤ eε · P(M(D′) ∈ S)

Laplace Mechanism: To achieve ε-DP for a query f, add calibrated noise:

M(D) = f(D) + Lap(∆f/ε)

where ∆f = maxD,D′ differ by 1 |f(D) − f(D′)| is the sensitivity.

DP-SGD Algorithm: To train neural networks with differential privacy:

1\. Compute per-example gradients gi for each sample in the batch 2. Clip: ¯gi = gi/max(1,∥gi∥/C) 3. Aggregate and add noise: ˜g = B

1Pi ¯gi + N(0,σ2C2I) 4. Update: θ ← θ − η˜g

Deep Learning in Healthcare Hilary Term 2026

(a) Exact counts and differential privacy. A hospital database contains 10,000 patient records. Consider the query: “How many patients have diabetes?” with true answer 250. If the hospital releases the exact count (250), does this satisfy ε-DP for any finite ε? Use the formal definition to justify your answer. What information can an attacker infer about a specific patient?

(b) Sensitivity and noise calibration. Explain why the sensitivity of the diabetes counting query is ∆f = 1, by considering what happens when a single patient is added to or removed from the dataset. Using this sensitivity with ε = 0.1, compute the Laplace noise scale and give the approximate 95% confidence interval for the released count, using the fact that 95% of Laplace samples fall within ±2.3 × scale of the true value. Is the noisy answer clinically useful?

(c) Privacy-utility trade-off. Explain the practical difference between ε = 0.1 (strong privacy) and ε = 10 (weak privacy) in terms of the noise added, the bound on probability ratios, and the resulting utility. For what types of medical application is each setting appropriate? What happens to the total privacy budget when multiple queries are run on the same dataset?

(d) DP-SGD for chest X-ray classification. You are training a pneumonia detection model on 10,000 chest X-rays using DP-SGD with batch size B = 32, clipping norm C = 1.0, and noise multiplier σ = 1.1.

(i) Why must individual sample gradients be clipped before noise is added? What would

happen to the DP guarantee if gradients were unbounded? (ii) The privacy budget ε grows approximately as √T with the number of training steps. Explain intuitively why each additional training step “spends” privacy budget. If ε ≈ 1 is reached after 10 epochs, what does training for 100 epochs imply? (iii) The model achieves 92% accuracy with DP (ε = 1.0) versus 95% without DP. Discuss whether this 3% accuracy loss is acceptable for medical deployment. How does increasing the batch size affect the privacy-utility trade-off?

Clinical Context: Differential privacy enables hospitals to share aggregate statistics and train models on sensitive medical data while providing mathematical guarantees of patient pri- vacy. Regulatory bodies increasingly require formal privacy protections for medical AI systems.

3 LSTM Networks and Recurrent Architectures for Clinical

Time Series

Consider a recurrent model for predicting patient deterioration in the ICU from a 24-hour history of vital signs: heart rate, blood pressure, and oxygen saturation.

(a) Vanishing gradients in vanilla RNNs.

In a vanilla RNN, ht = tanh(Whhht−1 + Wxhxt).

(i) Write the gradient ∂L/∂h0 as a product of terms and explain why this product

shrinks exponentially with sequence length T. (ii) For an ICU sequence of 100 hourly readings, what does this imply about the model’s ability to learn long-range patterns, such as an 8-hour trend in heart rate that may indicate early sepsis?

Deep Learning in Healthcare Hilary Term 2026

(b) LSTM gating mechanism. The LSTM cell state is updated as:

ct = ft ⊙ ct−1 + it ⊙ ˜ct

(i) Describe the roles of the forget gate ft, input gate it, candidate state ˜ct, and output

gate ot. (ii) Explain why the additive cell state update - rather than the multiplicative update

in vanilla RNNs - mitigates the vanishing gradient problem.

(c) Forget gate initialisation and dynamics.

The forget gate is ft = σ(Wf\[ht−1;xt\] + bf). The bias bf is often initialised to a large positive value (e.g., 1-2) rather than zero.

Consider the following ICU scenarios:

• Scenario 1: A patient shows a gradual upward trend in heart rate over 8 hours (70 → 85 bpm), potentially indicating early sepsis

• Scenario 2: A ventilated patient with stable, artificially-controlled vitals is suddenly extubated and begins breathing spontaneously

Explain why the initialisation of bf matters for learning, and analyse what forget gate behaviour (ft ≈ 0 vs ft ≈ 1) is appropriate in each scenario.

(d) Gradient flow and comparison with alternative architectures.

A hospital compares three models for 12-hour-ahead sepsis prediction:

• A feedforward network using only the most recent 1-hour window of vitals

• A first-order Markov model: P(yt | xt,xt−1)

• An LSTM processing the full 24-hour history

Analyse why the LSTM can capture patterns that the other two models cannot, with reference to how gradients flow through the LSTM cell state. A colleague argues that because LSTMs have approximately 4× as many parameters as a vanilla RNN with the same hidden dimension, they must be more prone to overfitting on small clinical datasets. Critically evaluate this argument.

Clinical Context: Clinical time series often contain long-range temporal dependencies (such as a multi-hour deterioration trend) that simple models cannot capture. Recurrent archi- tectures with selective memory mechanisms are essential for early warning systems.

4 Self-Attention and Transformers for Medical Text (Optional)

Consider the following clinical note: “Patient presents with fever, cough, and shortness of breath.” Suppose we extract a simplified 4-token sequence: fever, cough, shortness, breath.

(a) Consider the (pre-softmax) attention scores between tokens, given by QK⊤:

QK⊤ =

4 1 0 0 1 0 4 1 1 8 0

6

 0 0 6 8where rows/columns correspond to tokens: fever, cough, shortness, breath.

Deep Learning in Healthcare Hilary Term 2026

(i) Apply softmax row-wise to obtain the attention weights. Which token does “short-

ness” attend to most strongly? (ii) The tokens “shortness” and “breath” form a clinical phrase. Explain how the atten-

tion pattern reflects this semantic relationship. (iii) In a bidirectional model, all tokens can attend to all others. In a causal (autoregres- sive) model, tokens can only attend to previous tokens. Which would you use for clinical note summarisation vs. next-word prediction? Why? (b) Explain the role of the scaling factor 1/√dk in self-attention. What happens to gradients

during backpropagation if this scaling is omitted when dk is large?

(c) Compare self-attention and RNN-based models for clinical text processing with respect

to:• Computational complexity,

• Parallelisability,

• Modelling long-range dependencies.

(d) A multi-head attention layer uses h = 8 heads, each with dk = dv = 64, and model

dimension dmodel = 512.

(i) Explain why the total computation is roughly equivalent to single-head attention

with full dimensionality dk = 512, despite using multiple heads. (ii) Different attention heads often learn to focus on different aspects of the input (e.g., syntactic vs. semantic relationships). Give a specific medical NLP example where this specialisation would be beneficial.

Clinical Context: Transformer-based models such as ClinicalBERT and BioBERT may be used to extract structured information from unstructured clinical notes, including medication- disease relationships and outcome prediction.
