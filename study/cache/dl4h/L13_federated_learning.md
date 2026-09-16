# DL4H — L13: Federated Learning & Data-Private Learning
> Source: Google Drive file 1a6LyGTW5Vn1D4VXi2UN6VAqVsnGR2H_9 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L13\_federated\_learning 

Deep Learning in Healthcare

Data-Private Learning

Ana Namburete Department of Computer Science University of Oxford

Core Tension

Centralised learning assumes:

Access to a single dataset ð·={ð¥\!,ð¦\! }$

\!"\#

Healthcare reality:

ð·\=⋃& %"\# ð·% with ð·% siloed.

• Large, distributed, sensitive data

• Cannot be freely centralised

How do we optimise without pooling ð·\!?

Site 1

Site 3

Local data

Local data

Local data Site ð

Site 2

Local data

A concrete scenario: Multi-hospital training

Site Samples Scanner Shift

UK 200 Modern Baseline

Germany 100 Older Lower intensity

USA 150 High-end Higher intensity

Japan 50 Rural Gaussian blur

Statistical perspective:

Governance perspective: Pooling improves robustness.

Pooling is constrained.

Problem: Data are decentralised and heterogeneous.

Constraints on Centralisation

Anonymisation is insufficient

• Removing identifiers ≠ eliminating re-identification risk

• Linkage attacks and anatomical uniqueness remain possible

Cross-institutional agreements are complex

• Jurisdiction-dependent legal requirements

• Cross-border transfer constraints under GDPR

• Significant administrative overhead

Practical constraints on centralised training

Quantifying label shift across sites

Step 1 Label distribution at each site

Let ð%(ð¦) be the empirical distribution of labels at site ð (discrete classes)

Example: proportion of patients requiring oxygen, ICU, etc.

Step 2 Measuring difference between two distributions

We first define Kullback-Liebler (KL) Divergence:

ð·\!" ð∥ð =\*ð ð¦ \# logð(ð¦) ð(ð¦)

Interpretation:

• Measures how “surprised” we are if we assume ð but the truth is ð

• ð·\!" = 0 only if distribution are identical

• Not symmetric: ð·\!" ð∥ð ≠ð·\!" ð∥ð

Step 3 Jensen-Shannon Divergence (symmetric)

Compute the JSD between sites ð and ð:

ð½ðð· ð$ ∥ ð% = 12 ð·\!" ð$ ∥ð + 12 ð·\!" ð% ∥ ð

where ð = &' ð$ + ð% .

Properties:

• Symmetric, bounded: 0 ≤ ð½ðð· ≤ log 2 (base-e)

• ð½ðð· = 0 ⟺ identical distributions

Quantifying label shift across sites

Useful summaries:

• Pairwise JSD matrix (0 ≤ ð½ðð· ≤ log 2)

• Mean JSD per site:

1 ð¾−1 -\!"\#

ð½ðð· ð\# ∥ ð\!

• JSD of each site to the global mixture

\# samples at site ð ð$%&'(% ð¦ + =-\#)\*ðð \#ð\#(ð¦)

\*(

ð(

Quantifying label shift across sites

From centralised learning to distributed optimisation

• Centralised empirical riskmin\! ð¹ ð = ð 1)"\#$%

ℒ ð\! ð¥" ,ð¦"

• Stochastic Gradient Descentð&'$ = ð& − ð∇ð¹( ð&

∇ð¹( ð& = 1ðµ )

)),+) ∈(where ðµ is a minibatch

Assumes:

• Data drawn from a single distribution ð(ð¥, ð¦)

• All data accessible centrally

∇ℒ ð\! ð¥" ,ð¦"

Distributed SGD

Distributed SGD: 1. Broadcast ð? 2. Workers compute gradients 3. Server aggregates

Parameter Server Model

Workers ð=1,…,ð¾

Each worker holds data shard ð·%

∇ð¹ ð B = '\!@Aðð \!∇ð¹\! ð

Communication Bottleneck

Problem:

• Synchronising every gradient step is expensive

• Stragglers slow training

• Communication dominates compute

Communication cost

Stragglers

Communication cost: Local Update SGD

Communication Bottleneck

Solution (Local Update SGD):

• Each worker performs ð¸ local steps before synchronisation

Stragglers: Asynchronous SGD

Local Update SGD

• Worker initialisation:

ð(\*,, = ð\*

• Local (worker) update rule:

ð(\*,-.& = ð(\*,- − ð∇ð¹( ð(\*,- for ð = 0, … , ð¸

• After ð¸ steps:

ð(\*.& ≔ ð(\*,/

• Server aggregation:

ð\*.& = \*(0&\! ð(ð ð(\*.&

• If ð¸=1 and data are IID → centralised SGD

• If ð¸\>1 → approximation error

Now Change the Constraint

New setting:

• Data are siloed (hospitals, phones)

• Cannot be centralised

• May not be IID

• Participation may be partial

• Privacy constraints apply

Site 3

The objective is the same. The constraints are different.

Site 1

Local data

Local data

Local data Site ð

Site 2

Local data

Federated Learning Objective

min\! ð¹ ð % = ("\#$ðð "ð¹"(ð)

where

ð¹" ð = 1ð" (

&-,(- ∈\*.

ℒ ð\! ð¥+ ,ð¦+

Constraints:

• Data decentralised

• Non-IID

• Communication limited

• Privacy-sensitive

Global model

Σ

Site 1

Site ð

Local data

Local data

Local data

Site 2

Local data

Federated Learning: One communication round

Step 1: Server broadcasts current model

Global server

Current server parameters, ð\*

Data never leaves local sites.

Site 1

Site ð

Local data

Local data

Local data

Site 2

Local data

Data never leaves local sites.

Step 2: Selected clients perform local SGD

Global server

Current server parameters, ð\*

Federated Learning: Local SGD

Site 1

Site ð

Local data

Local data

Local data

Site 2

Local data

Step 3: Server aggregates updates

Global server

Σ

Data never leaves local sites.

Federated Learning: Server aggregation

Update server parameters, ð\*.&

Site 1

Site ð

Local data

Local data

Local data

Site 2

Local data

Why Local Steps?

• Instead of:

• One SGD step per round

• We allow:

• ð¸ local steps before aggregation

• Benefit:

• Fewer communication rounds

• Trade-off:

• Increased client drift under heterogeneity

Communication Efficiency

Site ð

Local data

Image credit

FedAvg Update

Local updates

Global update

McMahan et al, Communication-Efficient Learning of Deep Networks from Decentralized Data, AISTATS, 2016

Challenges in Federated Learning

First-Order Challenges

Statistical & Systems Constraints

Data heterogeneity (Non-IID)

ð\! ð¥, ð¦ ≠ ðO(ð¥, ð¦)

• Uneven resources

• Dropouts

• Client drift

• Slower convergence

→ asynchronous participation

Compute heterogeneity

Second-Order Challenges

• Large models

• Limited bandwidth

→ Local updates → Compression

Scalability & Security

Communication Cost

• Gradient leakage

• Model poisoning

• Backdoor attacks

→ DP → secure aggregation → robust aggregation

Security & privacy threats

ð

• Client updates are aligned

• Averaging ≈ global gradient step

IID vs. Non-IID: Geometry of Client Drift

IID Data

ð&\* ð&\*.&

ð'\* ð'\*.&

∇ð¹% ð ≈ ∇ð¹(ð)

∑B \!@A PP ,∇ð¹\! ð =∇ð¹ð but ∑B \!@A PP ,ð\!?QA ≠ð? − ð∇ð¹ ð?

ð&∗ð\* ð\*.& ð∗ ð'∗

ð

ð

Local model

Global model

Local optima

Global optima

ð&\* ð&\*.&

ð'\* ð'\*.& ð&∗ð&∗ð

ð\* ð\*.&

ð∗ ð\* ð\*.& ð∗ ð'∗ð'∗

• Client updates are aligned

• Averaging ≈ global gradient step

IID vs. Non-IID: Geometry of Client Drift

IID Data

Non-IID Data

∇ð¹% ð ≈ ∇ð¹(ð) ∇ð¹% ð ≉ ∇ð¹(ð)

• Local objectives differ

• Multiple local steps → client drift

• Averaging ≠ descent on ð¹

∑B \!@A PP ,∇ð¹\! ð =∇ð¹ð but ∑B \!@A PP ,ð\!?QA ≠ð? − ð∇ð¹ ð?

ð

ð

ð&\*.&

ð&\*

ð'\*

ð'\*.&

ð

FedProx: Controlling Client Drift

Problem (Non-IID + Multiple Local Steps)

Local update solves:min ð¹( ð

After ð¸ steps:ð(\*.& may drift far from ð\*

FedProx: Controlling Client Drift

Problem (Non-IID + Multiple Local Steps)

Local update solves:min ð¹( ð

After ð¸ steps:ð(\*.& may drift far from ð\*

FedProx

Each client solves instead:

min ð¹( ð + ð2 ð−ð\* '

Gradient:

∇ð¹( ð +ð ð−ð\*

FedProx: Controlling Client Drift

Problem (Non-IID + Multiple Local Steps)

Local update solves:min ð¹( ð

After ð¸ steps:ð(\*.& may drift far from ð\*

FedProx

Each client solves instead:

min ð¹( ð + ð2 ð−ð\* '

Gradient:

∇ð¹( ð +ð ð−ð\*

Interpretation

• Proximal regularisation around global model, ð\*

• Limits deviation from global model

• ð=0⇒ FedAvg

FedProx: Bound on drift

Let ð(∗ be the client-k minimiser of the FedProx local objective

ð(∗ = argmin2 ð¹( ð + ð2 ð−ð\* '

The first-order optimality condition gives:

∇ð¹( ð(∗ +ð ð(∗ − ð\* = 0 ⟹ ð(∗ − ð\* = − 1ð ∇ð¹( ð(∗

Taking norms and then the client-wise second moment (or variance) yields the bound

ð(∗ − ð\* ≤ 1ð ∇ð¹( ð(∗ ⟹ ð¼( ð(∗ − ð\* ' ≤ 1ð' ð¼( ∇ð¹( ð(∗ '

So the spread (and hence variance) of client updates is scaled down by a factor &3$

FedAvg vs FedProx

ð&∗ð'∗

ð\!∗ − ð? = −ð1∇ð¹\! ð\!∗ FedAvg (Non-IID)

ð

ð

Larger ð ⟹ smaller displacement ð&\*.&

ð&\*

ð\*.& ð\* ð∗ ð'\* ð'\*.&

ð

FedProx

ð

ð&∗ð\*.& ð∗ ð'∗

ð

ð ð−ð%

Global optima

What federated learning does:

• Keeps raw data local

• Shares model parameters or updates

What federated learning does NOT guarantee:

• Updates may encode information about local data

• Gradients depend directly on individual examples

∇ð¹% ð = 1ð% 7\!∈(&

∇ℒ ð) ð¥\! ,ð¦\!

Federated Learning is not automatically private

Avoiding data centralisation does not imply formal privacy guarantees.

Example:

Two datasets

• Dataset A: Health records

• Dataset B: Voter registration

• Overlap on ZIP, DOB, and sex

Intersection of quasi-identifiers → unique identification possible

Why informational privacy is insufficient

Removing identifiers is not enough:

• Re-identification via linkage attacks

• Unique anatomical features in patient images

• Auxiliary datasets enable deanonymisation

Even if we remove:

• Name

• DOB

• NHS Number

The dataset may still contain quasi-identifiers

Privacy risk depends on external auxiliary information, not only on the released dataset.

Example:

• MRI contains facial structure

• Reconstruction can recover identifiable features

• “Defacing” and metadata removal:

• Cropping metadata

• Removing facial pixels

Removing identifiers is not enough:

• Re-identification via linkage attacks

• Unique anatomical features in patient images

• Auxiliary datasets enable deanonymisation

Limitation: They do not provide a quantifiable bound on information leakage.

Why informational privacy is insufficient

Metadata in header file:

Differential Privacy

Differential Privacy

Dataset Model Probability of smoking

ð·ð¦ = 0.55

ð·′

Scenario 1

ð¦4 = 0.57

ððð y′y

The scenario with the highest Scenario 2

ð¦4 = 0.87 value indicates that there

has been a privacy leak Patient ð

• Key idea:

ððð 0.57

0.55 \< ððð 0.87 0.55

• The outcome of any analysis is essentially equally likely, independent of whether any individual joins, or refrains from joining, the dataset

Credit: Mukul Rathi Definition of Differential Privacy

Datasets ð· and ð·4 differ by one record Possible set of outcomes

Pr ℳ ð· ∈ ð ≤ e, Pr ℳ ð·′ ∈ð

A mechanism, ℳ, is ð-differential privacy if for any two adjacent datasets, ð· and ð·’ (differing in just one entry), a similar prediction will be achieved.

Dwork, C and Roth, A. The algorithmic foundations of differential privacy, Foundations and Trends in Theoretical Computer Science, 2014

Credit: Mukul Rathi Definition of Differential Privacy

log Pr Pr ℳ ℳ ð·′ ð· ∈ ð

∈ð ≤ ð

Privacy budget

ð=0 Nothing learned

ð = ℎððℎ Learn more

ð = ððð¤ More private

Dwork, C and Roth, A. The algorithmic foundations of differential privacy, Foundations and Trends in Theoretical Computer Science, 2014

Credit: Mukul Rathi ð-Differential Privacy

For show a mechanism that this inequality (or model) holds

ð to be ð-differentially private, log Pr Pr ℳ ℳ ð·′ ð· ∈ ð

∈ð

Dwork, C and Roth, A. The algorithmic foundations of differential privacy, Foundations and Trends in Theoretical Computer Science, 2014

Privacy budget ≤ ð

Pr ℳ ð· ∈ ð ≤ e, Pr ℳ ð·′ ∈ð

Formal definition: ℳ gives ð-differential privacy if for all pairs of datasets, ð· and ð·’ differing in the data of one person, and all events ð

Credit: Mukul Rathi (ð-ð¿)-Differential Privacy

Relaxed inequality:

Pr ℳ ð· ∈ ð ≤ e, Pr ℳ ð·′ ∈ð +ð¿

Failure probability

Formal definition: ℳ gives ð-differential privacy if for all pairs of datasets, ð· and ð·’ differing in the data of one person, and all events ð

Dwork, C and Roth, A. The algorithmic foundations of differential privacy, Foundations and Trends in Theoretical Computer Science, 2014

Interpretation

• Smaller ð → larger noise → stronger privacy

• Larger ð → smaller noise → weaker privacy

Mechanism

To release a statistic ð(ð·), add noise:

Ið ð· =ð ð· +ð¿ðð Δðð

• Δð: sensitivity (max change from one individual)

• ð: privacy budget

Calibrated Noise for Differential Privacy

Adjacent datasets ð· and ð·4

Sequential Composition Theorem

Theorem: Let ℳ+ each provide ð+-differential privacy. The sequence of ℳ+(ð·) provides ∑+ð+ -differential privacy.

ð·ð·

Sequential Composition Theorem

Theorem: Let ℳ+ each provide ð+-differential privacy. The sequence of ℳ+(ð·) provides ∑+ð+ -differential privacy.

ð·

ð&: ð&-DP

ℳ5(… (ℳ& ð· ) ℳ',…,ℳ… 56& ∑$ ð$-DP

ð·

ð&:ð&-DP

ð':ð'-DP max ð&,…,ð5 -DP ð5:ð5-DP

ℳ&(ð·)

Sequential composition

ð5: ð5-DP

Parallel composition

⋮

Privacy accounting during training

Iterative learning consumes privacy budget

Each DP-SGD step:

• Clips gradients

• Adds noise

• Uses part of privacy budget

In Federated Learning

Each communication round:

• Performs local updates

• ð&2&34 ≈ ∑6 5\#$ ð5

• Contributes to cumulative privacy cost

ððð¡ðð ðððð£ððð¦ ððð ð¡ ∝ ðð¢ðððð ðð ððððð¢ððððð¡ððð ððð¢ððð 

Over ð» training steps

ð\*+\*,- ≈ 7\*"\#.

ð\*

Privacy loss accumulates.

learning/deep-learning-differential-privacy/

Differentially-Private SGD

• Differentially-private stochastic gradient descent (DP-SGD)

Scale the gradient so that it has a max L2 norm of value ð¶

Credit: Mukul Rathi

learning/deep-learning-differential-privacy/

Differentially-Private SGD

• Differentially-private stochastic gradient descent (DP-SGD)

Add noise proportional to the clipping norm, C

Credit: Mukul Rathi

Trusted aggregator

Global model

Current model parameters, ð

Σ

DP-SGD in Deep Learning

Site 1

Site ð

Local data

Local data

Local data

Site 2

Credit: McMahan

Local data

From theory to practice: FL in Healthcare Systems

Example: FL in Healthcare

Dayan et al. Federated learning for predicting clinical outcomes in patients with COVID-19. Nature Medicine, 2021 Dinsdale et al. FedHarmony: Unlearning Scanner Bias with Distributed Data, MICCAI, 2022

• EXAM model

• 20 international hospitals

• 16,148 chest X-rays

• 34-layer ResNet

• FedAvg algorithm

Persistent Heterogeneity

• Scanner-dependent intensity distributions

• Demographic differences

• Label imbalance

ð% ð¥, ð¦ ≠ ð/ ð¥, ð¦

The Heterogeneity Problem Persists

FedHarmony: Distributed Domain Adaptation

• Federated adversarial domain adaptation

• Scanner-invariant representations

• No raw data sharing

Addressing scanner-induced heterogeneity

SFHarmony: Source-Free Domain Adaptation

• No access to source data

• Share only feature statistics

• Gaussian mixture modelling

• Bhattacharyya distance modelling

Attack surface

• Gradient inversion

• Feature reconstruction

• Membership inference

What is transmitted in FL?

∇ð¹% ð = ð1% 7\!∈(&

∇ℒ ð) ð¥\! ,ð¦\!

• Gradients depend directly on local samples

• High-dimensional updates encode structure

Model updates can leak information

Alternative Privacy Architecture: PATE

• Privacy Aggregation of Teacher Ensembles (PATE)

• Train teacher models on disjoint datasets

• Aggregate teacher predictions with noise

• Train student on noisy labels

Privacy Mechanism

Noisy majority vote ⟹ ð,ð¿ -DP

Key difference

Privacy via noisy aggregation, not via decentralised optimisation.

Image credit

Federated Learning as a Systems Problem

Decentralisation ⋅ Heterogeneity ⋅ Privacy

Approach Data Movement Optimisation Privacy Mechanism

FL Model updates Distributed SGD Optional DP

FL + DP Model updates DP-SGD Noise on gradients

PATE No data sharing Central training Noisy aggregation

SFHarmony Model + statistics Source-free DA Reduced exposure Privacy strategies

<https://p
