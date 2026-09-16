# DL4H — Problem Sheet 4: Worked Solutions
> Source: Google Drive file 1LxUuhSYqxvHJQJos5FqHdpUytfQOanMI · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Deep Learning in Healthcare Hilary Term 2026

Problem Sheet 4 - Worked Solutions Federated Learning, Privacy, Sequence Models & Transformers

1 Federated Learning for Multi-Hospital Collaboration

1\. FedAvg Aggregation.

(a) Data contribution:

• Hospital 3: 2000/4000 = 50% of data

• Hospital 2: 500/4000 = 12.5% of data Should Hospital 3 have more influence? Yes, weighted averaging is preferred for several reasons: 1. Represents the global data distribution:

• If we pooled all data and trained centrally, each sample would contribute equally

• Weighted averaging (Pk nkn wk) replicates this: each sample (not each hospital) has equal influence

• Hospital 3’s 2000 samples should contribute 50% of the gradient signal 2. Better gradient estimation:

• Larger datasets produce more accurate gradient estimates (lower variance)

• Weighting by nk upweights reliable estimates 3. Convergence guarantees:

• FedAvg with weighted averaging converges to the same solution as centralized training (under IID assumptions)

• Simple averaging would bias toward hospitals with less data Simple averaging alternative: Would give each hospital equal influence regardless of data size:

• Hospital 2 (500 samples) would have same weight as Hospital 3 (2000 samples)

• This over-represents smaller hospitals’ potentially noisier estimates

• May be desired for fairness (all hospitals equal voice), but hurts accuracy

(b) Scenario: After local training, some hospitals diverge significantly from the initial

global model. Problem with equal weighting: If Hospital 4 (small dataset, 500 samples) diverges significantly but receives 25% weight (equal share):

• Its potentially noisy/biased update has outsized influence

• Small datasets are more prone to overfitting on local idiosyncrasies

• Local features specific to Hospital 4 (e.g., unique scanner artifacts) contaminate the global model Weighted averaging mitigates this:

• Hospital 4 gets only 12.5% weight, limiting damage from divergent updates

• Hospital 3 (reliable, large dataset) dominates at 50%, anchoring the global model

Deep Learning in Healthcare Hilary Term 2026

Convergence • • Under This is weighted equivalent implications:

averaging, to minimising FedAvg the minimises loss on the the pooled weighted dataset

sum Pk nkLk(w)

• Equal weighting optimises a different objective that may not reflect clinical pri- orities

(c) Weighted average (FedAvg):

w = Xk

nn kwk = 0.25w1 + 0.125w2 + 0.50w3 + 0.125w4

Simple average (uniform weights):

w = 14(w1 + w2 + w3 + w4)=0.25w1 + 0.25w2 + 0.25w3 + 0.25w4

Why weighted average is better: 1. Represents global dataset: Weighted average is equivalent to training on centralized data. Proof (informal): Consider gradient descent. The centralized gradient is:

∇Lcentral = n

1Xi=1

n∇Li

Splitting by hospitals:

∇Lcentral = n

1 X

i∈Hosp 1∇Li + X

i∈Hosp 2∇Li + ··· = n1n · 1n1

X i∈Hosp 1∇Li + n2n · 1n2

X i∈Hosp 2∇Li + ···

\=

XKk=1

nn k∇Lk

This is exactly the FedAvg weighted average\! Therefore, FedAvg converges to the same solution as centralized training (under IID data assumption). 2. Fairness to data size:

• Hospital 3 has 2000 samples (50% of total data)

• Should have 50% influence on global model (represents 50% of patients)

• Hospital 2 has 500 samples (12.5% of data)

• Should have 12.5% influence (represents 12.5% of patients)

• Simple average: All hospitals equal weight (25% each)

– Unfair to Hospital 3\! (Contributes 50% data, gets 25% influence) – Unfair to patients\! (Patients at Hospital 3 under-represented) 3. Convergence guarantees: Theorem: tralized optimum Under at IID rate data, O(1/FedAvg √T) where with T weighted is the number averaging of communication converges to the rounds. cen-

Simple average has no such guarantee. 4. Statistical efficiency:

• Weighted average: Each patient sample counted equally

Deep Learning in Healthcare Hilary Term 2026

• Simple average: Small hospitals over-represented, large hospitals under-represented

• Weighted average makes optimal use of all available data When simple average might be preferred: Case 1: Data quality varies

• Hospital 3 has poor labeling (50% error rate)

• Hospital 1 has excellent labeling (1% error rate)

• Weighted average: Dominated by low-quality data from Hospital 3\!

• Solution: Weight by quality, not quantity

w = 0.5w1 + 0.1w2 + 0.1w3 + 0.3w4

(Downweight Hospital 3 due to poor quality) Case 2: Strategic fairness

• Want each hospital to have equal say (democratic model)

• Prevent large hospitals from dominating consortium

• Political/governance reason, not statistical Case 3: Privacy protection

• Large hospitals contribute more gradients ⇒ leak more information

• Weighted average: Hospital 3 pays 4× the privacy cost of Hospital 4

• Simple average: Equal privacy cost per hospital (more fair) Answer: Use weighted average (FedAvg default) because:

• Statistical optimality (converges to centralized solution)

• Fairness to data contributors and patients

• Better utilisation of large datasets

• Theoretical convergence guarantees Exception: Weight by data quality if quality varies significantly across hospitals. (d) Computation per hospital:

Hospital 1: 1000 samples × 5 epochs = 5,000 gradient updates Hospital 2: 500 samples × 5 epochs = 2,500 gradient updates Hospital 3: 2000 samples × 5 epochs = 10,000 gradient updates Hospital 4: 500 samples × 5 epochs = 2,500 gradient updates

Hospital 3 does twice the computation of Hospital 1, and four times the com- putation of Hospitals 2 and 4\! Is this fair? Perspective 1: Data-proportional (current scheme) - Patient-fair Argument YES (computation-fair):

\+ Hospital 3 processes more data ⇒ more compute required (linear scaling) + Should Hospital 3 be penalized for having more patients? + Each patient contributes equally to global model (ethical\!) + Weighted aggregation already accounts for data size + Each local gradient computed with equal effort (one backprop per sample) Argument NO (resource-fair):

− Hospital 3 spends 2× GPU time compared to Hospital 1 − Hospital 3 pays 2× electricity costs − Hospital 3 takes 2× longer per round ⇒ other hospitals wait

Deep Learning in Healthcare Hilary Term 2026

− Hospital 3 is the bottleneck in federated training Perspective 2: Computation-proportional - Hospital-fair Each hospital does equal compute, regardless of data size:

• Hospital 3: 2000 samples, 2.5 epochs ⇒ 5,000 updates

• Hospital 1: 1000 samples, 5 epochs ⇒ 5,000 updates

• Hospital 4: 500 samples, 10 epochs ⇒ 5,000 updates Problem: Small hospitals overtrain (overfit\!)

• Hospital 4 sees same data 10 times per round

• High risk of overfitting, poor generalisation

• May hurt global model quality Perspective 3: Equal-weight (simple average) - Institution-fair Each hospital has equal influence, regardless of data or compute:

• All hospitals: 25% weight in aggregation

• Democratic governance Problem: Statistical inefficiency

• Doesn’t reflect data size

• Patients at Hospital 3 under-represented

• Doesn’t converge to centralized optimum Recommendation for medical federated learning: Default: Data-proportional (FedAvg standard) Justification:

• Maximises statistical efficiency

• Converges to centralized optimum

• Each patient contributes equally (patient-level fairness - ethical\!)

• Best global model performance Modifications for hospital fairness: 1. Computation budget:

• Hospital 3 objects to 2× compute cost

• Allow Hospital 3 to do fewer epochs (e.g., 2-3 instead of 5)

• Reduce weight proportionally: w3 = (2000 × 3)/(4000 × 5) × 2.5 = 30%

• Balances computation and contribution 2. Financial compensation:

• Pay hospitals for compute: $10 per epoch-sample

• Hospital 3 earns: 2000 × 5 × $10 = $100,000

• Hospital 4 earns: 500 × 5 × $10 = $25,000

• Fair compensation for contribution

• Incentivizes participation 3. Privacy-fairness:

• Large hospitals contribute more gradients ⇒ leak more information

• Cap contribution: Max 25% weight per hospital

• Hospital 3: Weight capped at 25% (down from 50%)

• Protects privacy of large hospitals

• Encourages participation without privacy penalty Answer: Current scheme is patient-fair but hospital-unfair.

• Hospital 3 does 2× compute for 2× data (proportional effort)

Deep Learning in Healthcare Hilary Term 2026

• Ethically justified: Each patient should contribute equally

• Practically: May need compensation or computation budgets to incentivize large hospital participation Best practice: Use data-proportional weighting with financial compensation or flexible computation budgets for fairness. (e) (⋆ Challenge) Convergence analysis of FedAvg.

(i) Global minimiser. The global objective is F(w) = 13F1(w) + 23F3(w). Setting F ′(w) = 0:

13(w − 1.0) + 23(w − 2.5) = w − 1+5

3 =0 =⇒ w∗ = 2.0

Equivalently, w∗ = n1w∗1 + n3w∗3

n = 1000 × 1.0 + 2000 × 2.5

3000 = 6000

3000 = 2.0. (ii) One local step (E = 1, η = 1) from w(0) = 0. The gradient of Fk at w is ∇Fk(w) = w − w∗k. With η = 1:

w(1)

k = w(0)

k − 1 · (w(0)

k − w∗k) = w∗k

So Hospital 1 reaches w(1)

1 = 1.0 and Hospital 3 reaches w(1)

3 = 2.5 in a single step.

• (A) Uniform averaging: 12(1.0+2.5) = 1.75 = w∗

• (B) Proportional averaging: 1000 3000(1.0) + 2000 3000(2.5) = 13 + 53 = 2.0 = w∗ ✓ Proportional averaging recovers the global minimiser exactly because, when each hospital reaches its own local optimum in one step, the weighted average reproduces the minimiser of the global weighted objective. (iii) Two local steps (E = 2, η = 0.5) from w(0) = 0. Using w(t+1)

k = w(t)

k − 0.5(w(t)

k − w∗k): Hospital 1: w(1)

1 =0+0.5(1.0) = 0.5; w(2)

1 = 0.5+0.5(0.5) = 0.75 Hospital 3: w(1)

3 =0+0.5(2.5) = 1.25; w(2)

3 = 1.25 + 0.5(1.25) = 1.875 Proportional average: 13(0.75) + 23(1.875) = 0.25 + 1.25 = 1.5 = w∗ = 2.0. After two steps each hospital is only 75% of the way to its own local optimum ((1 − 0.5)2 = 0.25 of the gap remains). Averaging these partially-converged models introduces a systematic bias: the aggregated result (1.5) falls well short of w∗ (2.0), even with correct proportional weighting. This is the mathematical underpinning of client drift: multiple local epochs drive each hospital toward its own local optimum, and the average of these diverging trajectories undershoots the true global minimiser. The effect is absent when E = 1 with η = 1 (part ii), but worsens as E increases or as heterogeneity (|w∗1 − w∗3|) grows.

2\. Non-IID Data Challenge.

(a) IID (Independent and Identically Distributed) data:

• Each hospital’s data is a random sample from the same population

• Local objectives Lk ≈ Lglobal for all hospitals

• Local updates point in the same direction

• FedAvg converges smoothly to global optimum Non-IID data (current scenario):

• Hospital 1: Elderly (¿65 years), 60% pneumonia prevalence

• Hospital 2: Pediatric (¡18 years), 20% pneumonia prevalence

Deep Learning in Healthcare Hilary Term 2026

• Hospital 3: General population, 30% prevalence

• Hospital 4: Rural, poor image quality, 40% prevalence Each hospital’s data has different:

• Feature distribution: Age, anatomy, imaging quality

• Label distribution: Pneumonia prevalence varies 3× (20%-60%) Why this hurts convergence: 1. Client drift: Each hospital optimises for its local objective Lk, not global objective Lglobal. Example:

• Hospital 1 learns: “Elderly features ⇒ high pneumonia risk”

• Hospital 2 learns: “Pediatric features ⇒ low pneumonia risk”

• These objectives conflict\!

• Local updates ∇L1 and ∇L2 point in different directions

• Aggregated update: wglobal = Pk(nk/n)wk is a compromise

• Compromise may not optimise any local objective well Mathematical intuition: IID case:

L1 ≈ L2 ≈ L3 ≈ L4 ≈ Lglobal

All hospitals optimise the same objective ⇒ consistent updates. Non-IID case:

L1 = L2 = L3 = L4

Hospitals optimise different objectives ⇒ conflicting updates ⇒ slow convergence. 2. Gradient diversity: Non-IID data causes gradients to have higher variance across hospitals:

Var(∇Lk) increases with non-IID severity

High variance ⇒ aggregated gradient less accurate ⇒ slower convergence. 3. Local overfitting: Each hospital may overfit to its local data distribution:

• Hospital 1: Overfits to elderly patients

• Hospital 2: Overfits to pediatric patients After aggregation, the global model is a mixture of these overfitted models ⇒ worse generalisation. 4. Convergence to suboptimal solution: Non-IID data can cause FedAvg to converge to a local minimum instead of global minimum:

• Global objective: Lglobal = (1/4)(L1 + L2 + L3 + L4)

• FedAvg may converge to a point that is:

– Local minimum of Lglobal (not global minimum) – Or doesn’t converge at all (oscillates) Answer: Data heterogeneity (non-IID) causes FedAvg to converge slowly or poorly because:

i. Client drift: Local objectives Lk differ, causing conflicting gradient directions ii. High gradient variance: Aggregated gradients less accurate iii. Local overfitting: Each hospital overfits to its distribution

Deep Learning in Healthcare Hilary Term 2026

iv. Suboptimal convergence: May reach local minimum or oscillate Concept of “client drift”: Each client (hospital) updates the model toward its local optimum, which “drifts” away from the global optimum. After aggregation, the global model is pulled in multiple conflicting directions, slowing convergence. (b) Scenario: Test both models on Hospital 2’s test set (pediatric patients).

Model 1: Local model (Hospital 2 only)

• Trained on: 500 pediatric samples

• Data: Homogeneous (all pediatric, 20% prevalence)

• Specialisation: Highly specialised to pediatric pneumonia Model 2: Federated model (all 4 hospitals)

• Trained on: 4000 total samples (500 pediatric + 3500 non-pediatric)

• Data: Heterogeneous (elderly, pediatric, general, rural)

• Generalisation: More diverse training data Which performs better on Hospital 2’s pediatric test set? Trade-off analysis: Local model advantages:

\+ Perfectly matched to test distribution (pediatric) + No interference from other hospitals’ data + Optimised specifically for pediatric pneumonia features Local model disadvantages:

− Small dataset (500 samples) ⇒ high risk of overfitting − Limited diversity ⇒ poor generalisation to unseen pediatric cases − May miss features common across all age groups Federated model advantages:

\+ Large dataset (4000 samples) ⇒ better generalisation + Diverse data ⇒ learns robust features (lung opacity, consolidation) + Age-invariant features transferable to pediatric cases + Less overfitting due to implicit regularization from diverse data Federated model disadvantages:

− Not optimised specifically for pediatric data − Influenced by elderly (Hospital 1) and rural (Hospital 4) data − May underweight pediatric-specific features (only 12.5% of training data) Expected outcome: Most likely: Federated model performs better Reasoning:

i. Data quantity: 4000 vs 500 samples (8× more data)

• Deep learning benefits from large datasets

• 500 samples may be insufficient to train a robust CNN

• Federated model has much lower variance ii. Transferable features:

• Pneumonia features (lung infiltrates, consolidation, airspace opacities) are similar across age groups

• Models trained on adults can transfer to pediatric cases

• Federated model learns these general features from diverse data iii. Reduced overfitting:

• Local model: High risk of memorizing 500 training samples

Deep Learning in Healthcare Hilary Term 2026

• Federated model: Regularized by diversity ⇒ better generalisation iv. Empirical evidence:

• Studies show federated models often outperform local models, even on local test sets

• Benefit of large, diverse data outweighs cost of heterogeneity Exception - Local model might win IF:

• Pediatric pneumonia has very distinct features (e.g., different pathogens, anatomy)

• Non-pediatric data actively harms performance (negative transfer)

• 500 samples are sufficient for local model (simple task, good data) Typical accuracy estimates:

• Local model: 80-85% (limited data, high variance)

• Federated model: 87-92% (more data, better generalisation) Answer: Federated model likely performs better on Hospital 2’s test set because:

i. 8× more training data (4000 vs 500) ⇒ better generalisation ii. Learns age-invariant pneumonia features transferable to pediatrics iii. Less overfitting due to diverse data However, if pediatric pneumonia has highly distinct features, the local model could outperform. In practice, federated learning usually benefits all participants, even on local test sets. (c) Technique 1: Data Sharing (Small Public Dataset)

Mechanism:

• Create a small shared dataset (e.g., 100 samples from each hospital)

• All hospitals can access this public dataset

• Each hospital trains on: Local data + Shared data How it helps:

• Shared data provides common ground for all hospitals

• Reduces distribution mismatch across clients

• Aligns local objectives toward common goal Trade-offs:

\+ Simple to implement + Significantly improves convergence (empirical: 20-30% accuracy gain) + Small dataset (¡1% of total) sufficient − Requires data sharing (may violate privacy/regulatory constraints) − Must ensure shared data represents all distributions − Not always feasible in medical settings (HIPAA, GDPR) Example: Create public dataset with 25 samples from each hospital (100 total), covering all age groups and imaging protocols. Technique 2: FedProx (Proximal Term Regularization) Mechanism: Modify local training objective to penalize drift from global model:

min wk Lk(wk) + µ2∥wk − wglobal∥2

where:

• Lk(wk): Local loss on hospital k’s data

Deep Learning in Healthcare Hilary Term 2026

• µ2∥wk − wglobal∥2: Proximal term (penalty for deviating from global model)

• µ \> 0: Regularization strength How it helps:

• Prevents local models from drifting too far from global model

• Encourages consensus across hospitals

• Reduces client drift Trade-offs:

\+ No data sharing required (privacy-preserving\!) + Provably improves convergence for non-IID data + Simple to implement (add one term to loss) + Hyperparameter µ controls trade-off (specialisation vs consensus) − Requires tuning µ (typical: µ = 0.01-1.0) − May underfit if µ too large (forces too much consensus) − Doesn’t address root cause (data heterogeneity remains) Example: Set µ = 0.1. Hospital 1 optimises:

min w1 L1(w1)+0.05∥w1 − wglobal∥2

This keeps w1 close to wglobal while still specialising to elderly patients. Other notable techniques (brief): 3. Personalization:

• Train global model + local personalization layers

• Each hospital has: Shared backbone + hospital-specific head

• Best of both: Global features + local adaptation 4. More local epochs:

• Increase local epochs from 5 to 20-50

• Reduces communication frequency

• Can improve convergence (counterintuitive\!) 5. Dynamic weighting:

• Weight hospitals by: Data quality, not just quantity

• Downweight hospitals with poor data quality Answer: Two techniques to mitigate non-IID data: 1. Data sharing (small public dataset):

• Share 100 samples (25 per hospital) as common ground

• Pro: Simple, effective (20-30% improvement)

• Con: Requires data sharing (privacy concerns) 2. FedProx (proximal regularization):

• Add penalty term µ2∥wk − wglobal∥2 to local loss

• Pro: Privacy-preserving, provably improves convergence

• Con: Requires tuning µ, doesn’t eliminate heterogeneity Recommendation: Try FedProx first (no privacy cost). If insufficient, consider small public dataset.

Deep Learning in Healthcare Hilary Term 2026

2 Differential Privacy for Medical Data

1\. Laplace Mechanism for Medical Queries.

(a) Analysis:

NO, releasing true counts does NOT satisfy ε-DP for any finite ε. Proof: Let D be the database with 250 diabetic patients, and D′ be the database with 251 diabetic patients (adding one diabetic patient). If we release true counts:

• M(D) = 250 (deterministic)

• M(D′) = 251 (deterministic) For ε-DP, we require:

P(M(D) ∈ S) ≤ eε · P(M(D′) ∈ S)

Consider S = {250}:

P(M(D) = 250) = 1 P(M(D′) = 250) = 0

⇒ 1 ≤ eε · 0

1 ≤ 0 FALSE for any finite ε\!

Attack scenario: An attacker knows a specific patient (Patient 1001) was either in D or D′, and wants to determine if this patient has diabetes.

• If released count = 250 ⇒ Dataset is D ⇒ Patient 1001 does NOT have diabetes

• If released count = 251 ⇒ Dataset is D′ ⇒ Patient 1001 HAS diabetes

The attacker can infer Patient 1001’s diabetes status with 100% confidence\! This is a complete privacy breach. Key insight: Deterministic outputs that depend directly on individual records can- not satisfy differential privacy. Randomisation (noise) is essential. (b) Why sensitivity ∆f = 1 for counting queries:

The sensitivity of a query f is defined as:

∆f = max D,D′ differ by 1 record|f(D) − f(D′)|

For a counting query (“How many patients have diabetes?”): Consider two databases differing by one patient:

• Worst case 1: Adding a diabetic patient

– f(D) = 250 – f(D′) = 251 – |f(D) − f(D′)| = 1

• Worst case 2: Adding a non-diabetic patient

– f(D) = 250 – f(D′) = 250 – |f(D) − f(D′)| = 0

• Worst case 3: Removing a diabetic patient

– f(D) = 250 – f(D′) = 249

Deep Learning in Healthcare Hilary Term 2026

– |f(D) − f(D′)| = 1 Maximum change: ∆f = 1 Answer: Sensitivity ∆f = 1 Intuition: Adding or removing one person can change the count by at most ±1. (c) With Laplace scale b = ∆f/ε = 1/0.1 = 10, the 95% confidence interval spans

approximately ±2.3 × 10 = ±23 patients around the true value. Utility implications: For the true count of 250 diabetic patients:

• 95% CI: Approximately \[227,273\]

• Relative uncertainty: ±23/250 ≈ 9% Is this clinically useful? For population-level planning: Yes

• Knowing “approximately 225-275 diabetic patients” is sufficient for resource al- location

• Budget planning, staffing decisions don’t require exact counts

• The order of magnitude (hundreds, not thousands) is preserved For precise statistics: Limited

• Prevalence estimate: 250/10000 = 2.5% becomes \[2.3%,2.7%\]

• Detecting small year-over-year changes (e.g., 250 → 260) is difficult

• Comparing subgroups with small differences becomes unreliable Key insight: Strong privacy (ε = 0.1) trades accuracy for protection. The utility depends on whether approximate answers suffice for the clinical question. (d) ε = 0.1 (Strong Privacy):

• Privacy bound: e0.1 ≈ 1.105

• Meaning: Output distributions for D and D′ are nearly identical

P(M(D) ∈ S) P(M(D′) ∈ S) ∈ \[1/1.105,1.105\] = \[0.90,1.11\]

• Attacker’s inference:

– Prior belief about Patient 1001: 50% chance has diabetes – After seeing query output: Can update to at most 50% × 1.105 = 55.25% – Only 5% change\! Very hard to infer individual’s data

• Noise scale: b = 1/0.1 = 10 (high noise)

• Utility: Low (95% CI: ±28, relative error ≈ 11%)

• Use case: Highly sensitive data

– HIV status databases – Genetic disease registries – Mental health records

ε = 10 (Weak Privacy):

• Privacy bound: e10 ≈ 22,026

• Meaning: Output distributions can differ drastically

P(M(D) ∈ S) P(M(D′) ∈ S) ∈ \[1/22026,22026\]

• Attacker’s inference:

– Prior belief: 50% chance has diabetes

Deep Learning in Healthcare Hilary Term 2026

– After seeing output: Could update to nearly 100% (with clever attack) – Substantial information leakage about individuals

• Noise scale: b = 1/10 = 0.1 (low noise)

• Utility: High (95% CI: ±0.28, relative error ≈ 0.11%)

• Use case: Less sensitive aggregate statistics

– Public health surveillance – Hospital resource planning – Population-level trends Privacy-Utility Trade-off Table:

ε Privacy Utility Noise Scale Medical Use Case 0.01 Strongest Worst Lap(100) Individual genetics 0.1 Strong Poor Lap(10) Patient diagnoses 1.0 Moderate Good Lap(1) Hospital statistics 10 Weak Excellent Lap(0.1) Public health trends

Medical AI Guidelines:

• HIPAA-compliant: ε ≤ 1.0

• Research ethics boards: ε ≤ 3.0

• Public datasets: ε \< 10

• Recommendation: ε = 0.1-1.0 for medical applications Important caveat - Privacy composition: Multiple queries on the same data compound privacy loss:

• Query 1: ε1-DP

• Query 2: ε2-DP

• Combined: (ε1 + ε2)-DP (privacy degrades\!) Example: If ε = 0.1 per query:

• 10 queries: Total ε = 1.0 (moderate privacy)

• 100 queries: Total ε = 10 (weak privacy\!) Must carefully budget ε across all queries\!

2\. DP-SGD for Chest X-ray Classification.

(a) Intuition: Privacy budget grows with √T

Each training step involves:

i. Sampling a batch from the dataset ii. Computing per-example gradients iii. Adding calibrated Gaussian noise Why more steps spend more privacy:

• Each step reveals information about the training data through the noisy gradient

• An adversary observing all T gradient updates gains more information than observing just one

• • Privacy The √T loss dependence composes comes across from steps: advanced total leakage composition accumulates

theorems (sublinear, not linear\!) Implication for 100 epochs: If ε ≈ 1 after 10 epochs, then after 100 epochs:

ε100 ≈ ε10 ×

r100

10 = 1 × √10 ≈ 3.2 This is problematic because:

Deep Learning in Healthcare Hilary Term 2026

• ε = 3.2 provides much weaker privacy than ε = 1.0

• Typical deep learning uses 50-100 epochs; DP-SGD forces early stopping

• Must balance convergence needs against privacy budget

• Pre-training on public data, then short DP fine-tuning is a common strategy Practical guidance: DP-SGD typically limits training to 10-20 epochs for strong privacy (ε ≤ 1), making efficient use of each gradient update critical. (b) Example: A gradient gi = \[2.5,−1.3,0.8\] has norm ∥gi∥ ≈ 2.9. After clipping with C = 1.0, the gradient is scaled down to ¯gi ≈ \[0.85,−0.44,0.27\] with ∥¯gi∥ = 1.0. Why unbounded gradients violate DP: Differential privacy requires that adding/removing one sample changes the output by a bounded amount (the sensitivity). In DP-SGD:

• Each sample contributes one gradient gi to the batch average

• Without clipping, a single outlier sample could have ∥gi∥ = 100 or more

• This outlier would dominate the batch gradient, making it easy to detect

• An adversary could infer: “The gradient changed drastically ⇒ outlier patient present” Clipping bounds sensitivity: By ensuring ∥¯gi∥ ≤ C for all samples, no individual sample can influence the aggregate gradient by more than C/B. This bounded sensitivity enables calibrated noise addition. Trade-off in choosing C: Small C (aggressive clipping):

• Pro: Lower sensitivity ⇒ less noise needed ⇒ better privacy-utility trade-off

• Con: Most gradients are clipped ⇒ gradient direction distorted ⇒ slower/worse convergence

• Con: Outlier samples (which may be clinically important\!) are heavily down- weighted Large C (mild clipping):

• Pro: Gradients preserved more faithfully ⇒ faster convergence

• Pro: Rare but informative samples retain influence

• Con: Higher sensitivity ⇒ more noise needed ⇒ worse privacy or utility Practical guidance: C is typically set so that 50-80% of gradients are clipped (e.g., median gradient norm). This balances information preservation with sensitivity control. Key insight: Clipping bounds sensitivity:

• Without clipping: Large gradients from outlier samples dominate

• Sensitivity = unbounded ⇒ Would need infinite noise for DP\!

• With clipping: All gradients have ∥¯gi∥ ≤ C

• Sensitivity of average gradient = C/B (bounded\!) 2. Enables calibrated noise: After clipping, the sensitivity of the sum Pi ¯gi is at most C (adding/removing one sample changes the sum by at most C). Therefore:

For ε-DP: Add noise ∼ N(0,σ2C2I) where σ = Cε · B

3\. Prevents information leakage: Without clipping:

• Sample with very large gradient ⇒ Outlier data point

Deep Learning in Healthcare Hilary Term 2026

• Large gradient reveals information about that specific sample

• Attacker could identify outliers in training set With clipping:

• All gradients normalised to same scale

• No single sample can dominate the update

• Individual contributions indistinguishable Effect on training:

• Regularization: Prevents extreme gradient updates (similar to gradient clip- ping for stability, but stronger)

• Convergence: Can slow convergence if C is too small (underfitting)

• Typical values: C = 0.1-10 depending on model and data

(c) Given:

• Without DP: 95% accuracy

• With DP (ε = 1.0): 92% accuracy

• Accuracy loss: 3 percentage points Is this acceptable for medical deployment? Arguments FOR acceptance:

i. Privacy is paramount:

• Medical data is highly sensitive (HIPAA, GDPR requirements)

• Legal requirement: Cannot risk patient re-identification

• 3% accuracy trade-off is necessary for regulatory compliance

• Lawsuits from privacy breaches could be more costly than false diagnoses ii. Still clinically useful:

• 92% accuracy may exceed human radiologist performance (∼85-90%)

• Better than no model (baseline random: 50%)

• Can adjust decision threshold to control false positive/negative rates

• 3% loss is within acceptable bounds for many screening applications iii. Enables data sharing and collaboration:

• DP-trained models can be shared across hospitals without legal barriers

• Enables collaborative learning on larger, more diverse datasets

• Long-term benefit (better generalisation) outweighs short-term accuracy loss iv. Prevents privacy attacks:

• Membership inference: Can’t determine if patient in training set

• Model inversion: Can’t reconstruct training images

• 3% accuracy is worth preventing these attacks

Arguments AGAINST acceptance:

i. Clinical consequences of misdiagnosis:

• 95% → 92%: 3% more patients misdiagnosed

• For pneumonia (10% prevalence in 10,000 patients = 1,000 cases): – Without DP: 50 false negatives (5% miss rate) – With DP: 80 false negatives (8% miss rate) – 30 additional patients miss treatment\!

• For deadly disease, this is unacceptable ii. Liability and trust concerns:

• Hospital sued: “You used inferior model to protect privacy/save costs”

• Hard to explain DP to patients, juries, regulators

• Perception: “You prioritized privacy over patient safety”

Deep Learning in Healthcare Hilary Term 2026

• Erodes trust in AI-assisted diagnosis iii. Alternative privacy-preserving methods exist:

• Federated learning: 90-93% accuracy, similar privacy, better trade-off

• Secure multi-party computation (SMPC): Cryptographic privacy, no accuracy loss (but slower)

• Data use agreements: Legal privacy contracts, full accuracy

• DP may be unnecessary if better alternatives available iv. ε = 1.0 provides weak privacy:

• e1.0 ≈ 2.72 privacy bound

• Attacker can still gain substantial information

• Not clear if patients understand what ε = 1.0 guarantees

• False sense of security

Recommendation (Context-Dependent): Acceptable IF:

✓ Legal requirement (GDPR right to deletion, cannot retain data) ✓ No federated learning possible (single hospital, limited infrastructure) ✓ Research use only (not clinical deployment) ✓ Low-risk application (screening, triaging, not definitive diagnosis) ✓ Accuracy drop doesn’t disproportionately increase false negatives NOT acceptable IF:

× Life-critical application (cancer detection, sepsis prediction) × Federated learning achieves 93% with better privacy guarantees × Baseline human performance is 93% (DP model worse than clinician\!) × Patients not informed of accuracy-privacy trade-off Best practice approach:

i. Try federated learning first (often better privacy-utility trade-off) ii. If DP required: Consider larger ε (e.g., ε = 3) to recover accuracy (92% → 94%) iii. Report both DP and non-DP performance metrics transparently iv. Inform patients and clinicians of the trade-off in consent forms

v. Allow patient opt-in: Choose privacy vs. accuracy for their case vi. Monitor real-world performance closely after deployment vii. Have fallback to human expert for low-confidence predictions Verdict: Conditionally acceptable

• Disclose trade-off transparently to all stakeholders

• Use only if no better privacy-preserving alternative exists

• Monitor post-deployment performance and patient outcomes

• Maintain human oversight and intervention capability

(d) Signal-to-Noise Ratio Analysis:

Small batch (B = 8):

• Gradient: ˜g = 18

• Signal (gradient Pmagnitude): 8i=1 ¯gi + N(0,σ∥18

2C2I)

• Noise standard deviation: σC = P1.1 i ¯g× i∥ 1.0=1.1

≈ 1 (assuming aligned gradients)

• SNR: signal/noise = 1.0/1.1 ≈ 0.91 (poor\!) Large • • • Gradient: Signal: Noise batch standard ∥ 32 1(B ˜g P= = i ¯g32

1deviation: 32): i∥ P≈ 32 i=1 1 ¯gi + N(0,σ2C2I)

(clipped gradients roughly aligned) Still σC = 1.1 (same noise\!)

Deep Learning in Healthcare Hilary Term 2026

• But: Averaging 32 gradients reduces variance by factor of √32

• Effective noise seen by gradient: 1.1/√32 ≈ 0.19

• SNR: 1.0/0.19 ≈ 5.3 (much better\!) Key insight: The noise added is independent of batch size (always N(0,σ2C2I)), but the signal (average of clipped gradients) benefits from averaging over more samples. This improves the signal-to-noise ratio by √B. Convergence speed:

• Higher SNR ⇒ More accurate gradients

• More accurate gradients ⇒ Faster convergence

• Faster convergence ⇒ Fewer steps T needed to reach target loss

• Since total privacy ε ∝ √T, fewer steps ⇒ less privacy leakage Privacy amplification perspective: The privacy cost per step scales as:

εstep ∝ qσ = B/Nσ

Larger B increases q (worse per-step privacy), BUT:

• Better gradient quality ⇒ Need fewer total steps T

• Total privacy: εtotal ∝ pT · q2/σ

• Empirically, the reduction in T often outweighs the increase in q Trade-offs: Advantages of larger batches:

\+ Better signal-to-noise ratio (improves by √B) + Faster convergence (fewer epochs needed) + Less total privacy budget consumed + More stable training (less variance in gradient estimates) Disadvantages of larger batches:

− Higher memory requirements (B samples must fit in GPU) − Potential generalisation gap (large batches sometimes generalise worse in non-

private training, but less of an issue with DP noise) − Diminishing returns: Beyond B ≈ 0.1%-1% of dataset, benefits plateau Optimal strategy for DP-SGD: i. Use the largest batch size that:

• Fits in GPU memory

• Is less than ∼1% of dataset size (to maintain convergence properties)

• Doesn’t harm model generalisation ii. For medical imaging: B = 32-128 is typical iii. For 10,000 samples: B = 32 (0.32% of data) is reasonable iv. Could increase to B = 64 or B = 128 if memory allows Answer: Larger batches improve privacy-utility trade-off because:

i. Better SNR: Averaging more gradients reduces relative noise by √B ii. Faster convergence: Higher SNR ⇒ fewer steps T needed iii. Less privacy cost: Total ε ∝ √T, so fewer steps conserves privacy budget Use the largest batch size practical (typically 0.3-1% of dataset).

Deep Learning in Healthcare Hilary Term 2026

3 LSTM Networks and Recurrent Architectures for Clinical

Time Series

(a) Vanishing gradients in vanilla RNNs.

In a vanilla RNN, ht = tanh(Whhht−1 + Wxhxt). Applying the chain rule back through time:

∂L ∂h0 =

YTt=1\! Whh ⊤· diag(tanh′(zt))∂L ∂hT

Why this product shrinks:

• tanh′(z)=1 − tanh2(z) ≤ 1 always, and is much smaller than 1 for large activations

• If the spectral norm of Whh is ρ \< 1, each factor contributes a factor ≤ ρ

• The product of T such factors shrinks as ρT: exponential decay

• Even if ρ = 1, the tanh′ saturation factors still cause exponential decay in practice

Implications for 100-step ICU sequences: After 100 steps, the gradient ∂L/∂h0 is effectively zero. This means:

• The model cannot adjust weights to reflect patterns from early time steps

• An 8-hour gradual heart rate trend spanning steps 1-48 contributes no gradient signal

• Only patterns from the most recent few steps (within the last hour) influence learning

• The model is fundamentally incapable of learning that early deterioration signals predict sepsis onset, regardless of how much data it is trained on

(b) LSTM gating mechanism.

Roles of each gate: The cell state ct = ft ⊙ ct−1 + it ⊙ ˜ct is updated through three learned gating signals:

• Forget gate ft = σ(Wf\[ht−1;xt\] + bf): element-wise multiplies the previous cell state. When ft,j ≈ 1, dimension j of the memory is retained; when ft,j ≈ 0, it is erased. Allows selective forgetting in response to new inputs.

• Input gate it = σ(Wi\[ht−1;xt\]+bi): controls how much of the new candidate state is written. Prevents irrelevant observations from overwriting long-term memory.

• Candidate state ˜ct = tanh(Wc\[ht−1;xt\] + bc): the proposed update to memory, computed from the current input and previous hidden state.

• Output gate ot = σ(Wo\[ht−1;xt\]+bo): controls which dimensions of the cell state are exposed as the hidden state ht = ot ⊙ tanh(ct). Separates what is stored from what is communicated.

Why additive updates mitigate vanishing gradients: The gradient of the cell state at time 0 with respect to time T is:

∂cT ∂c0 =

YTt=1diag(ft)

When ft ≈ 1 (the network has learned to remember), this product is approximately the identity matrix I, regardless of sequence length T. This is in contrast to the vanilla RNN where the gradient involves repeated multiplication exponentially. The additive cell state update creates by a “gradient Whh ⊤· diag(tanh′), which decays highway” that preserves gradient magnitude over long distances.

Deep Learning in Healthcare Hilary Term 2026

(c) Forget gate initialisation and dynamics.

Why initialisation matters:

With bf = 0 and small initial weights:ft ≈ σ(0)=0.5

The LSTM forgets 50% of its cell state at each step, causing information to decay as (0.5)T. After 10 steps, only (0.5)10 ≈ 0.1% of the original signal remains.

Initialising bf to 1 or 2 gives ft ≈ 0.73-0.88, so information persists long enough for the gradient signal to teach the network when to forget. Starting with ft ≈ 0.5 means the LSTM never has the opportunity to learn from long-range patterns.

Scenario 1 (gradual 8-hour heart rate trend):

The LSTM should remember (ft ≈ 1). Each individual reading (e.g., 71 bpm, 73 bpm, ...) lies within the normal range and carries no alarm signal in isolation. Only the accumulated 8-hour trend from 70 to 85 bpm indicates early sepsis. The cell state must preserve this running history; selective forgetting would destroy the very signal that matters. Large bf enables the network to learn this “keep accumulating” policy.

Scenario 2 (extubation event):

The LSTM should forget (ft ≈ 0). Mechanical ventilation enforces artificial respiratory patterns, heart rates, and blood pressures that are irrelevant once the patient breathes spontaneously. The entire pre-extubation baseline is stale. The LSTM must learn to reset its memory at this physiological discontinuity, treating post-extubation observations as a fresh context.

A single fixed exponential decay rate cannot simultaneously implement both policies. Learned gating allows the LSTM to apply different forget rates in different physiological contexts.

(d) Gradient flow and comparison with alternative architectures.

Feedforward network (1-hour window):

• Input: Only the most recent 60 observations (1-hour window)

• An 8-hour deterioration trend beginning 7 hours ago is simply absent from the input

• No amount of additional parameters or training can compensate for missing input features

• Fundamental limitation: architectural, not statistical

First-order Markov model P(yt | xt,xt−1):

• Conditions only on the two most recent observations

• Multi-hour patterns are structurally unrepresentable regardless of model size

• Cannot capture that a sequence of individually normal readings constitutes an ab- normal trend

LSTM (24-hour history):

When ft ≈ 1, the gradient highway gives:

∂cT ∂c0 =

YTt=1diag(ft) ≈ I

Deep Learning in Healthcare Hilary Term 2026

Gradients flow back to time step 0 without attenuation. The network can therefore dis- cover that a reading from 12 hours ago (or a trend beginning then) is predictive of the current outcome. The key advantage is not access to more data but the learned selective memory: the LSTM discovers which patterns across the full 24-hour window are clinically relevant. Evaluating the overfitting argument: The colleague conflates redundant capacity with necessary capacity. A vanilla RNN with the same hidden dimension cannot represent solutions that require long-range memory - it suffers from structural underfitting, not good generalisation. Adding more vanilla RNN parameters does not fix the vanishing gradient problem; it simply adds more parameters that are equally unable to learn from distant time steps. LSTM’s 4× parameter count reflects four distinct gating matrices, each learning a spe- cialised memory policy. This capacity is necessary, not redundant. For small clinical datasets, overfitting is controlled through standard regularisation (dropout on inputs and hidden states, weight decay, early stopping) without sacrificing the structural advantages of the LSTM.

Clinical Context: Clinical time series often contain long-range temporal dependencies (such as a multi-hour deterioration trend) that simple models cannot capture. Recurrent archi- tectures with selective memory mechanisms are essential for early warning systems.

4 Self-Attention and Transformers for Medical Text (Optional)

(a) Attention score computation.

(i) Applying softmax to the “shortness” row: Pre-softmax scores for “shortness”: \[0,1,8,6\]

exp(\[0,1,8,6\]) = \[1, e1, e8, e6\] ≈ \[1, 2.72, 2981, 403\]

Sum ≈ 3388 ⇒ ashortness ≈ \[0.000, 0.001, 0.880, 0.119\]

“Shortness” attends most strongly to itself (88%), secondarily to “breath” (12%), and negligibly to “fever” and “cough”.

(ii) Semantic relationship: The attention pattern reflects that “shortness” and “breath” together form the compound medical term “shortness of breath” (dyspnoea). The high pre-softmax score of 8 between these tokens indicates that their query-key inner product is large - the model has learned representations for which these two words are highly compatible. Attending to “breath” allows “shortness” to incorporate context that disambiguates it (“shortness of breath” vs “shortness of stature”). “Fever” and “cough” are independent symptoms with low cross-token scores, correctly reflecting semantic independence.

(iii) Bidirectional vs causal: Clinical note summarisation: use bidirectional (BERT-style) attention. Summarisation is a comprehension task requiring full document context before generating output. The model must understand how “wound healing complications” at the end of a note relates to “history of diabetes” at the beginning. Causal masking would prevent this. Next-word prediction: use causal (GPT-style) attention. Auto-regressive generation must condition only on the tokens generated so far. Attending to future tokens would constitute “cheating” - the future words are precisely what the model must predict.

Deep Learning in Healthcare Hilary Term 2026

(b) Scaling factor 1/√dk.

If queries q · k = Pdj=1 and kkeys are drawn from distributions with unit variance, the dot product

qjkj is a sum of dk independent unit-variance terms, giving:

Var(q · k) = dk ⇒ std = pdk

For dk = 64, typical dot product magnitudes are ±3√64 = ±24. At such scales, the softmax becomes nearly one-hot:

softmax(zi) ≈

(1 for the maximum zi

0 otherwise

The gradient of the softmax output with respect to its input is softmaxi(1 − softmaxi), which approaches 0 when softmax concentrates on one token. This causes vanishing gradients through the attention layer: backpropagation cannot update query and key matrices, Dividing by √and dk the attention mechanism fails to learn meaningful token relationships. rescales the dot products to unit variance regardless of dk, keeping softmax in a regime with well-distributed attention weights and meaningful gradients. This scaling is critical for stable training at large model dimensions (e.g., dk = 512 or larger).

(c) Self-attention vs RNN-based models.

Computational complexity:

• Self-attention: O(n2d) - computing all n2 pairwise attention scores, each requiring O(d) operations

• RNN: O(nd2) - sequential matrix-vector products of dimension d × d at each of n steps

• Self-attention is more efficient when n\<d, which is typical for clinical notes (n ∼ 100- 500 tokens, d ∼ 512-1024)

Parallelisability:

• Self-attention: fully parallel - all n2 attention scores are computed simultaneously as a single matrix multiplication QK⊤. Modern GPUs achieve near-linear speedups with sequence length.

• RNN: inherently sequential - ht depends on ht−1, so step t cannot begin until step t − 1 completes. Even with optimised implementations, RNNs are 5-10× slower on GPU for sequences of length 256+ despite comparable FLOPs.

• Self-attention enables training on much longer sequences within the same wall-clock budget.

Modelling long-range dependencies:

• Self-attention: path length of 1 between any two tokens - “history of diabetes” in sentence 1 can directly attend to “wound healing” in sentence 10. No information degradation with distance.

• RNN (LSTM): path length of n - information from token 1 must propagate through n − 1 hidden state updates to reach token n. Even LSTMs experience residual degradation over hundreds of steps.

Deep Learning in Healthcare Hilary Term 2026

• For clinical notes where critical clinical relationships may span long distances (e.g., allergy mentioned at admission and antibiotic prescribed on day 5), direct token-to- token attention is strongly preferable.

(d) Multi-head attention.

(i) Computational equivalence:

With h = 8 heads and dk = dv = 64, each head uses projection matrices of shape dmodel × dk = 512 × 64. The total parameter count for all heads:

• Query projections: 8 × (512 × 64) = 262,144

• Key projections: 8 × (512 × 64) = 262,144

• Value projections: 8 × (512 × 64) = 262,144

• Output projection WO: 512 × 512 = 262,144

• Total: ≈ 1,048,576 parameters

Single-head attention with dk = 512 uses the same total - 3 × (512 × 512) + 512 × 512 ≈ 1,048,576. The computation per forward pass is also equivalent since each head processes a dk = 64 subspace and the h×dk = 8×64 = 512 total dimensions match the single-head case.

(ii) Specialisation in medical NLP:

Each head operates on a different linear projection of the input and learns to attend to different types of relationships simultaneously. In a clinical discharge summary, different heads may specialise as follows:

• Head 1 (drug-indication): attends from drug names to their associated diagnoses (“metformin” attends strongly to “type 2 diabetes”)

• Head 2 (dosage-drug): attends from dosage values to the drug they modify (“500 mg” attends to “metformin”)

• Head 3 (temporal): attends from current medications to historical medications (“now prescribed lisinopril” attends to “previously on enalapril”)

• Head 4 (negation): attends from negated terms to the clinical finding being negated (“no” attends to “chest pain”)

No single head could capture all these relationship types simultaneously within a 64- dimensional subspace. The output projection WO combines all heads, enabling the model to jointly reason across drug-indication, dosage, temporal, and negation relationships when generating a prediction or summary.

Clinical Context: Transformer-based models such as ClinicalBERT and BioBERT may be used to extract structured information from unstructured clinical notes, including medication- disease relationships and outcome prediction.
