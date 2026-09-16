# DL4H — L1: Why DL for Healthcare
> Source: Google Drive file 13uX4KbEl8aFCbfj5o-dOUrrVOwF6ffmp · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L1\_why\_DL\_for\_healthcare 

Deep Learning in Healthcare

Course Introduction

Ana Namburete Department of Computer Science University of Oxford

Welcome\!

• Part A/B course on Deep Learning (DL) in Healthcare

• Learning Objectives

• Knowledge and fluency in state-of-art DL algorithms

• Develop practical ability to design and train neural networks

• Understand how to adapt models to diverse types of healthcare data

• Understand practical considerations and domain-specific challenges associated with the use of medical data

• Today:

• Deep Learning in Healthcare: Unique Data, Unique Challenges

• Course logistics

Clinical Exam Notes

Unique data, unique challenges

Several modalities, formats

Images

Vital Signs

Lab Results

Signals have different meaning

Magnetic Resonance Imaging (MRI)

Ultrasound

Data explosion in healthcare

1953 Watson and Crick discover double-helix structure of DNA

Wearable Sensors

Patient-generated health data

2009 Fitbit 1950s

EEG

1972 Peter Mansfield develops magnetic resonance imaging (MRI) for computerised imaging of internal body structures

1977 Fred Sanger sequences the first full genome of a virus

1990 - 2003 Human Genome Project sequences full human genome

2007 First iPhone

2006 - UK Biobank is launched to collect genetic, imaging, and environmental (e.g. lifestyle) data from 500,000 volunteers

Great promise, open challenges

Biases and fair representation Ensuring equal prediction performance, regardless of e.g. patient demographic

Explainability How to interpret the prediction? Can we understand the decision- making process of the neural network?

Privacy and security Medical data is sensitive and personally- identifying. Not easily shared. Protected by legislation (i.e. GDPR)

Module 1: DL Foundations & Medical Data Context

Unique data, unique challenges

Neural network fundamentals & training principles Improving training stability & generalisation

Module 2: DL Architectures & Medical Data

CNNs for images

Advanced CNNs (segmentation & vision transformers) Sequence models & transformers for clinical data

Module 3: Advanced topics & real-world deployment

Low-data regimes, representation learning, domain- specific losses

Explainability, trust, & fairness

Data-private learning (federated learning, differential privacy)

The scaffold for the course

Definitions and historical context

• Artificial intelligence (AI):

• Broad umbrella term

• Narrow AI

• Task-specific systems

• Deep learning

• Representation learning with neural networks

Why does this distinction matter in healthcare?

Symbolic AI

• Explicit rules

• Interpretable

• Brittle and hard to scale

• Rules learned from data

• Flexible and scalable

• Intrinsically opaque

Key implication for healthcare:

Accountability cannot be inferred from model structure It must be enforced through evaluation and governance

Connectionist AI

e.g., Deep Learning

Early AI in Healthcare

• Rule-based expert systems

• Strong performance in narrow domains

• Failed to scale or generalize

• Held back by legal and ethical issues

• Early neural networks

• Limited data

• Poor cross-site generalisation

• Minimal workflow integration

Expert systems (e.g. MYCIN): Feigenbaum (1970s, ’80s)

Early AI in Healthcare

• Early computer-aided diagnosis (CAD) systems in radiology

• Limited data

• Poor cross-site generalisation

• Minimal workflow integration

Neural network-based CAD: (1990s, early 2000s)

Why deep learning re-emerged

Digitisation of healthcare data (imaging, EHRs, genomics, wearables) Data

Compute

Algorithms Digitisation, memory, storage

GPUs Computer Scientists, Engineers Increased compute capacity Parallelisation Advances in

representation learning; libraries

What hasn’t changed:

Data quality varies systematically More data does not remove bias

The unique nature of healthcare data

Routine health data and the UK context

• Data not collected for research

• Generated across many trusts, services, and care pathways

• Different systems, coding practices, and standards

• Follow patients across institutions over time

• Governance obligations

Routine data are not research data

• Data is produced by clinical decisions

• Tests are ordered selectively

• Measurements reflect clinical judgement

• Absence of data can be informative

Clinical judgement

Test ordered No test

Missing value Data observed

Data quality and missingness

• Missingness is informative

• Missing Not At Random(MNAR)

• Whether data is missing depends on its unobserved value

• Labels are imperfect

• Expect disagreement

• Retrospective or proxy outcomes

• Carry intrinsic uncertainty

In healthcare, absence and uncertainty are part of the signal.

Provenance and heterogeneity

• Heterogeneity is the default

• Different sites, scanners, protocols

• Changes over time

• Systematic, not random, variation

Site effects Batch effects Distribution shift

Bias, Fairness, and Value Alignment in Healthcare

Bias as a value-alignment problem

• Bias is not a bug. It is a design outcome\!

• Models optimise proxy objectives (e.g., loss functions)

• Proxies encode value judgements

• Misalignment leads to systematic harm

Bias arises when model objectives diverge from clinical and/or societal values.

Where bias enters the healthcare ML lifecycle

• Problem specification

• What is being predicted, and why?

• Data generation

• Who is measured, when, and how?

• Modelling & validation

• Which metrics define “success”?

• Deployment

• Feedback loops and behaviour change

Suresh, Guttag. A framework for understanding sources of harm throughout the machine learning life cycle, EAAMO, 2021

Ascertainment and measurement bias

• Who gets measured is not random

• Measurement depends on access to care

• Surveillance intensity varies across groups

• Absence of data can be informative

Healthcare consequence:

Observed data ≠ underlying health status

Image source

Fairness metrics: unavoidable trade-offs

• Fairness is not a single number

• Multiple, incompatible definitions

• Equal accuracy ≠ equal error rates

• Thresholds encode inductive risk

Fairness requires contextual judgement

Why bias persists even with “good” data

• Historical data reflects structural inequalities

• “Representative” data can still encode injustice

• Learning from biases systems reproduces bias

Chen et al. Algorithmic fairness in artificial intelligence for medicine and healthcare, Nature Biomed Eng, 2023

Bias mitigation as an engineering discipline

Explainability, Transparency, and Informational Asymmetry

Transparency ≠ Explainability

• Transparency:

• knowing how a system is built

• Explainability:

• understanding why a decision was made

• A system can be transparent but not explainable

Clinicians need explanations, not source codeExplainability How to interpret the prediction? Can we understand the decision- making process of the neural network?

Informational asymmetry

• AI introduces informational asymmetry

Clinicians reason with context and intent

Risk: Decisions without shared understanding

Models operate on data abstractions

Patients see only outcomes

Explainability as a governance tool

• Explainability supports accountability, not reassurance

• It enables:

• Contestation: clinicians can challenge outputs

• Oversight: auditors and regulators can assess behaviour

• Error analysis: systematic failures can be identified

• Scope control: limits of safe use are explicit

Explainability is a system property

Prediction, intervention, and inductive risk

• Prediction ≠ Decision-making

• Prediction: what will happen under current practice

• Decisions: what should we do differently

• Treatments induce confounding

• Errors have asymmetric consequences

• False positives and false negatives differ in harm

• Thresholds encode value judgements

• Accepting a model output is a moral choice

Inductive risk

Treatment

Delegation, incentives, and feedback

• Delegation

• Patients and clinicians are principals

• Models act as agents

• Objectives are delegated, not identical

• Feedback

• Labels reflect past actions, not latent health states

• Deployment changes behaviour

• Behaviour changes future data

Principal-agent lens

Risk: Misaligned intentions and silent degradation

Practical consequences for model design

• Design discipline

• Careful target definition

• Explicit threshold justification

• Conservative deployment strategies

• Continuous monitoring

There is no single metric or architecture that guarantees safety.

Governance as a pipeline

• Before training:

• Pre-specify targets and evaluation criteria (metrics)

• Before deployment:

• Validate on data that reflects real deployment conditions

• After deployment:

• Monitor continuously

• Retain the ability to intervene or withdraw

Governance mirrors the model lifecycle.

Trusted Research Environments (TREs)

• TREs invert traditional data-access model

• Data stays in secure environments

• Researchers bring code to the data

• Access, computation, and outputs are governed

UK examples: NHS Secure Data Environments OpenSAFELY

Governance enables trust, not speed

Regulatory reality Engineering constraints

• GDPR (UK/EU)

• Design requirements for • HIPAA (USA)

models:

• Auditability

• Accountability

• Data minimisation

• Continuous monitoring

• Ability to intervene or withdraw

Regulation does not sit outside the DL pipeline: it defines non-negotiable design constraints.

Why DL in healthcare?

“We demonstrate performance in making a referral recommendation that reaches or exceeds that of experts on a range of sight- threatening retinal diseases after training on only 14,884 scans.”

Gurovich et al, 2019

De Fauw et al, 2018

Summary

• Why deep learning in healthcare is challenging

• Objectives are proxies

• Data reflects decisions

• Errors have asymmetric consequences

• Deployment changes behaviour

From theory to the bedside

Course Logistics

Course Organisation

• Structure:

• 16 lectures, 4 practicals, 4 problem sheets (and classes)

• Location and Time:

• Weeks 1-8: Tuesday and Wednesday @ 10:00– 11:00; Tony Hoare Room

• Course webpage: https://www.cs.ox.ac.uk/teaching/courses/2025-2026/dlhealthcare/

• Content queries: ana.namburete@cs.ox.ac.uk

Practicals

Yicheng Gao Yannik Schnitzer

Week Content

3 Foundations and classification

4 Training CNNs for image segmentation

5 Regularisation techniques

7 Federated Learning

Location: Wolfson Bldg, Room 379 Weeks: 3, 4, 5, 7

Group 1: Thurs @ 15:00 - 17:00 Group 2: Mon @ 10:00 - 12:00

Problem Sheet

• 4 problem sheets

• Classes:

• Weeks: 4, 5, 7, 8

• Group 1: Thurs @ 15:00 - 17:00 Wolfson Bldg, Room 379

• Group 2: Mon @ 10:00 - 12:00 Wolfson Bldg, Room 379

Ikboljon Sobirov

Hazel Kim

Examination

• Take-home mini-project

• Opportunity to gain in-depth experience of developing DL-based approach to a healthcare problem

• Detailed project guidelines will be released in Week 8

Release date: Friday 8th week of HT @12pm

Submission date: Monday (-1)st week of TT

15th April 2024 @ 12pm

Deep Learning

Goodfellow, Bengio, Courville. MIT Press, 2016

\<link\>

• Acknowledgements

• Serena Yeung, Mitesh Khapra, Kosta Derparnis

Reading Materials

• Reading material

• Lecture notes (incl. references and useful links at the end)

• List of influential papers \<link\>

• Textbooks

Dive into Deep Learning

Zhang, Lipton, Li, Smola, et al. Amazon, 2019 (online, interactive book)

\<link\>

<https://blog.geneticsupportfoundation.org/index.php/2024/06/20/causation-versus-susceptibility-alzheimers-disease-genetics-apoe/>   
<https://www.cs.ox.ac.uk/teaching/courses/2023-2024/dlhealthcare/>   
<https://www.cs.ox.ac.uk/teaching/courses/2023-2024/dlhealthcare/>   
<https://www.cs.ox.ac.uk/teaching/courses/2023-2024/dlhealthcare/>   
[mailto:ana.namburete@cs.ox.ac.uk](mailto:ana.namburete@cs.ox.ac.uk)   
<https://sh-tsang.medium.com/overview-my-reviewed-paper-lists-tutorials-946ce59fbf9e>   
<https://www.deeplearningbook.org/>   
<https://d2l.ai/>   
