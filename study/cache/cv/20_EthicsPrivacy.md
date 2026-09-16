# Computer Vision — Ethics & Privacy
> Source: Google Drive file 1nPupFzreR5aJ4R0HJo8P7DnM87ISMUaR · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Ethics, Bias, Privacy

Computer Vision – Lecture 20

1

Further Reading

• Timnit Gebru and Emily Denton, CVPR 2020 Tutorial on FATE/CV

• Kate Crawford, “The Trouble with Bias”, NeurIPS 2017 Keynote

• Barocas, Hardt, Narayanan, “Fairness and machine learning”

• ACM Conference on Fairness, Accountability, and Transparency

• Law and Computer Science Course

• Oxford Internet Institute, Sandra Wachter

2

Why do we build ML systems?

Automate decision making, so machines can make decision instead of people.

Ideal: Automated decisions can be cheaper, more accurate, more impartial, improve our lives

Reality: automated decisions can encode bias, harm people, make lives worse

3

Case Study: COMPAS

1\. Person commits a crime, is arrested 2. COMPAS software predicts the chance that the person will commit another crime in the future (recidivism) 3. Recidivism scores impact criminal sentences: if a person is likely to commit another crime, shouldn’t they get a longer sentence?

Real system that has been used in New York, Wisconsin, California, Florida, etc.

4 Slide credit: J Johnson (this and following)

Case Study: COMPAS

2016 ProPublica article analyzed COMPAS scores for \>7000 people arrested in Broward county, Florida

Question: How many of these people ended up committing new crimes within 2 years?Source: https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm 5

Recap: Error Metrics

Prediction: Low Risk

Prediction: High Risk

Outcome: No Recidivism

False Positive (FP)

Outcome: Recidivated

True Negative (TN)

False Negative

True Positive (FN)

(TP)

6

Error Metrics: Error Rate

Prediction: Low Risk

Prediction: High Risk

Outcome: No Recidivism

False Positive (FP)

Outcome: Recidivated

True Negative (TN)

False

True Positive Negative (FN)

(TP)

Error Rate = ð»ðµ+ð­ð·+ð­ðµ+ð»ð· ð­ð·+ð­ðµ

How often is the prediction wrong?

7

Error Metrics: False Positive Rate

Prediction: Low Risk

Prediction: High Risk

Outcome: No Recidivism

True Negative (TN)

False Positive (FP)

Outcome: Recidivated

False Negative (FN)

True Positive (TP)

Error Rate = ðð+ð¹ð+ð¹ð+ðð ð¹ð+ð¹ð

How often is the prediction wrong?

False Positive Rate = ð­ð·+ð»ðµ

ð­ð·

How often were non-offenders predicted to reoffend?

8

Error Metrics: False Negative Rate

Prediction: Low Risk

Prediction: High Risk

Outcome: No Recidivism

True Negative (TN)

False Positive (FP)

Outcome: Recidivated

False Negative (FN)

True Positive (TP)

Error Rate = ðð+ð¹ð+ð¹ð+ðð ð¹ð+ð¹ð

How often is the prediction wrong?

False Positive Rate = ð¹ð+ðð

ð¹ð

How often were non-offenders predicted to reoffend?

False Negative Rate = ð­ðµ+ð»ð·

ð­ðµ

How often were offenders predicted not to reoffend?

9

Error Metrics: Different Stakeholders

Prediction: Low Risk

Prediction: High Risk

Outcome: No Recidivism

True Negative (TN)

False Positive (FP)

Outcome: Recidivated

False Negative (FN)

True Positive (TP)

Error Rate = ðð+ð¹ð+ð¹ð+ðð ð¹ð+ð¹ð

How often is the prediction wrong?

Defendants care about this

False Positive Rate = ð¹ð+ðð

ð¹ð

How often were non-offenders predicted to reoffend?

False Negative Rate = ð¹ð+ðð

ð¹ð

How often were offenders predicted not to reoffend?

10

Error Metrics: Different Stakeholders

Prediction: Low Risk

Prediction: High Risk

Outcome: No Recidivism

True Negative (TN)

False Positive (FP)

Outcome: Recidivated

False Negative (FN)

True Positive (TP)

Error Rate = ðð+ð¹ð+ð¹ð+ðð ð¹ð+ð¹ð

How often is the prediction wrong?

Defendants care about this

False Positive Rate = ð¹ð+ðð

ð¹ð

How often were non-offenders predicted to reoffend?

Judges care about this

False Negative Rate = ð¹ð+ðð

ð¹ð

How often were offenders predicted not to reoffend?

11

Case Study: COMPAS

Prediction: Low Risk

Prediction: High Risk

Outcome: No Recidivism

2681 (TN)

1282 (FP)

Outcome: Recidivated

1216 (FN)

2035 (TP)

Error Rate = ðð+ð¹ð+ð¹ð+ðð ð¹ð+ð¹ð

≈ 34.6%

False Positive Rate = ð¹ð+ðð ð¹ð

≈ 32.4%

False Negative Rate = ð¹ð+ðð ð¹ð

≈ 37.4%

Source: https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm

12

Case Study: COMPAS

Black Defendants

Prediction:

White

Prediction: High Risk

Defendants

Low Risk

Outcome: No Recidivism

Prediction: Low Risk

Prediction: High Risk

805 (FP)

Outcome: No Recidivism

Outcome: Recidivated

990 (TN)

1139 (TN)

349 (FP)

532

1369

Outcome: (FN)

(TP)

Recidivated

461 (FN)

505 (TP)

Source: https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm

13

Case Study: COMPAS

Black Defendants

Prediction:

White

Prediction: High Risk

Defendants

Low Risk

Outcome: No Recidivism

Prediction: Low Risk

Prediction: High Risk

805 (FP)

Outcome: No Recidivism

Outcome: Recidivated

990 (TN)

1139 (TN)

349 (FP)

532

1369

Outcome: (FN)

(TP)

Recidivated

Error Rate ≈ 36.2%

461 (FN)

505 (TP)

Error Rate ≈ 33.0%

Similar error rates between white and black defendants

Source: https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm

14

Case Study: COMPAS

Black Defendants

Prediction:

White

Prediction: High Risk

Defendants

Low Risk

Outcome: No Recidivism

Prediction: Low Risk

Prediction: High Risk

805 (FP)

Outcome: No Recidivism

Outcome: Recidivated

990 (TN)

1139 (TN)

349 (FP)

532

1369

Outcome: (FN)

(TP)

Recidivated

False Positive Rate ≈ 44.9%

461 (FN)

505 (TP)

Error Rate ≈ 36.2%

Error Rate ≈ 33.0%

False Positive Rate ≈ 23.5%

Black defendants have 1.9x higher False Positive Rate\!

Source: https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm

15

Case Study: COMPAS

Black Defendants

Prediction:

White

Prediction: High Risk

Defendants

Low Risk

Outcome: No Recidivism

Prediction: Low Risk

Prediction: High Risk

805 (FP)

Outcome: No Recidivism

Outcome: Recidivated

990 (TN)

1139 (TN)

349 (FP)

532

1369

Outcome: (FN)

(TP)

Recidivated

False Positive Rate ≈ 44.9%

False Negative Rate ≈ 28.0%

461 (FN)

505 (TP)

Error Rate ≈ 36.2%

Error Rate ≈ 33.0%

False Positive Rate ≈ 23.5%

False Negative Rate ≈ 47.7% White defendants have 1.7x higher False Negative Rate

Source: https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm

16

Case Study: COMPAS

Black Defendants

Prediction:

White

Prediction: High Risk

Defendants

Low Risk

Outcome: No Recidivism

Prediction: Low Risk

Prediction: High Risk

805 (FP)

Outcome: No Recidivism

Outcome: Recidivated

990 (TN)

1139 (TN)

349 (FP)

532

1369

Outcome: (FN)

(TP)

Recidivated

461 (FN)

505 (TP)

Surprising fact: COMPAS gives very different outcomes for white vs black defendants, but it does not use race as an input to the algorithm\!

Source: https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm

17

Source: https://fairmlbook.org/classification.html

No Fairness Through Unawareness

Even if a sensitive feature (e.g. race) is not an input to the algorithm, other features (e.g. zip code) may correlate with the sensitive feature

18

Formalizing Fairness

ð: Target variable (e.g. recidivism) ð: Classifier response (e.g. predicted recidivism) ð´: Sensitive attribute (e.g. race)

Fairness Definition 1: Independence The classifier response is independent (as a random variable) from the sensitive attribute

ð ð,ð´ = ð ð ð(ð´) = ð ð ð´)ð(ð´) (Chain Rule) ⟹ ð ð ð´) = ð(ð)

Barocas, Hardt, and Narayanan. “Fairness and Machine Learning”, https://fairmlbook.org/index.html

COMPAS predictions are not independent – different distributions for black vs white

Barocas, Hardt, and Narayanan. “Fairness and Machine Learning”, https://fairmlbook.org/index.html

Formalizing Fairness

Formalizing Fairness

ð: Target variable (e.g. recidivism) ð: Classifier response (e.g. predicted recidivism) ð´: Sensitive attribute (e.g. race)

Fairness Definition \#2: Separation The classifier response is conditionally independent from the sensitive attribute given the target

ð ð,ð´ ð = ð ð ð)ð ð´ ð)

Barocas, Hardt, and Narayanan. “Fairness and Machine Learning”, https://fairmlbook.org/index.html

Formalizing Fairness

Fairness Definition \#2: Separation The classifier response is conditionally independent from the sensitive attribute given the targetð ð,ð´ ð = ð ð ð)ð ð´ ð)

Error rate parity: Requires that all groups experience

• the same false negative rate.

• the same false positive rate. COMPAS scores

do not satisfy separation

Barocas, Hardt, and Narayanan. “Fairness and Machine Learning”, https://fairmlbook.org/index.html

Formalizing Fairness

ð: Target variable ð: Classifier response ð´: Sensitive attribute

Independence: ð ð,ð´ = ð ð ð ð´ Separation: ð ð,ð´ ð) = ð ð ð)ð ð´ ð)

Assume ð is binary, ð´ is not independent of ð, and ð is not independent of ð. Then, independence and separation cannot both hold.

(Proof in “Fairness and Machine Learning”)

Barocas, Hardt, and Narayanan. “Fairness and Machine Learning”, https://fairmlbook.org/index.html

Formalizing Fairness: Takeaways

There are multiple ways to formalize notions of fairness mathematically.

It is often impossible to achieve all notions of fairness at the same time

Fairness in ML is not only a technical problem\! We need to think about context, stakeholders, etc.

There are many notions of fairness: e.g. Arvind Narayanan, “21 fairness definitions and their politics”

Allocative Harms – Immediate Effect

• A system decides how to allocate resources

• If the system is biased, it may allocate resources unfairly or perpetuate inequality

• Examples:

• Sentencing criminals

• Loan applications

• Mortgage applications

• Insurance rates

• College admissions

• Job applications

Barocas et al, “The Problem With Bias: Allocative Versus Representational Harms in Machine Learning”, SIGCIS 2017 Kate Crawford, “The Trouble with Bias”, NeurIPS 2017 Keynote

Source: https://www.washingtonpost.com/technology/2019/10/22/ai-hiring-face-scanning-algorithm-increasingly-decides-whether-you-deserve-job/ https://www.hirevue.com/platform/online-video-interviewing-software Example Credit: Timnit Gebru

Example: Video Interviewing

Representational Harms

A system reinforces harmful stereotypes: denigration.

Barocas et al, “The Problem With Bias: Allocative Versus Representational Harms in Machine Learning”, SIGCIS 2017 Kate Crawford, “The Trouble with Bias”, NeurIPS 2017 Keynote Source: https://twitter.com/jackyalcine/status/615329515909156865 (2015, tweet no longer avaliable)

Representational Harms – Long Term

• Harder to quantify

• Cultural

Types

• Denigration: use of culturally disparaging terms

• Stereotype: reinforces stereotypes

• Recognition: a group is erased or made invisible

• Under-Representation: a group is under-represented

• Ex-Nomination: represent ideology as common sense28 Solon Barocas, Kate Crawford, Aaron Shapiro, Hanna Wallach, 2017 'The Problem With Bias: Allocative Versus Representational Harms in Machine Learning', SIGCIS Conference

Source: https://www.reddit.com/r/europe/comments/m9uphb/hungarian\_has\_no\_gendered\_pronouns\_so\_google

Hungarian does not use gendered pronouns

Hungarian -\> English Translation

English translation makes assumptions

DeepL

30

Source: https://www.bbc.com/news/newsbeat-32332603 , 2015

2021 results more diverse

2024

33

2025

34

Menon et al, “PULSE: Self-Supervised Photo Upsampling via Latent Space Exploration of Generative Models”, CVPR 2020 Example source: https://twitter.com/Chicken3gg/status/1274314622447820801

Image Super-Resolution

Input: Low-Resolution Face Output: High-Resolution Face

Representational Harms

denigration Stereotype Recognition Under-

representation

36 Ex-nomination

Image Search for “CEO” yields all white men on the first page

x x

Google Photo mislabels black people as “gorillas” x

YouTube speech-to-text does not recognize women’s voices

x x

HP Cameras’ facial recognition does not recognize Asian peoples’ faces

x x x

Amazon labels LGBTQ literature as ‘adult content’ and removes sales ranking

x x x

Word embeddings contain implicit biases \[Bolukbasi et al.\]

x x x x x

Searches for African-American-sounding names yields ads for criminal background checks \[Sweeney, 2013\]

x x x

Band-Aid Solutions

• Fairness & bias are often only an afterthought.

• Leads to band-aid solutions.

• E.g.: “let’s make everything as diverse as possible\!”

37 Source: https://www.theverge.com/2024/2/21/24079371/google-ai-gemini-generative-inaccurate-historical

Representational Harms

• Representational harms often transcend the scope of technical interventions.

• Technical approaches are necessary but not sufficient.

• Complicated political and cultural factors.

38

Ground-Truth: Soap Source: Nepal, $288/month

Azure: food, cheese, bread, cake, sandwich Clarifai: food, wood, cooking, delicious, healthy Google: food, dish, cuisine, comfort food, spam Amazon: food, confectionary, sweets, burger Watson: food, food product, turmeric, seasoning Tencent: food, dish, matter, fast food, nutriment

DeVries et al, “Does Object Recognition Work for Everyone?”, CVPR Workshops, 2019

Economic Bias in Visual Classifiers

Ground-Truth: Soap Source: UK, $1890/month

Azure: toilet, design, art, sink Clarifai: people, faucet, healthcare, lavatory, wash closet Google: product, liquid, water, fluid, bathroom accessory Amazon: sink, indoors, bottle, sink faucet Watson: gas tank, storage tank, toiletry, dispenser, soap dispenser Tencent: lotion, toiletry, soap dispenser, dispenser, after shave

Data Geolocation

• More data: increased diversity?

• Strong socio-economic bias on who has the means to access and upload data to the internet.

form DeVries et al., CVPRW ‘19

The Data Excuse

• It is tempting to dismiss these issues “of course the system is biased - this is just a training data issue”.

• As soon as our research affects people, this is not an excuse anymore.

• Affects people: publishing papers, open-source, used in applications, etc.\!

• We cannot only benefit from the hype, we need to also deal with the consequences.

41

Gender Bias

• Studying gender biases is complicated post-hoc.

• Ideal: ask subjects to specify their gender.

• Many datasets have been scraped from the internet.

• Many studies currently (knowingly) conflate: binary sex, gender, perceived gender.

• Known, obvious limitations, yet can still be useful in absence of annotations.

42

Multilabel Classification Person Umbrella Cat

Define “gender bias” of

\#(ð¶,ððð) object category C as:

\#(ð¶,ððð) + \#(ð¶,ððððð)

Example: “Snowboards” are 90% biased towards men

Zhao et al, “Men Also Like Shopping: Reducing Gender Bias Amplification using Corpus-level Constraints”, EMNLP 2017

COCO Dataset: Multi-label Classification

CNN predictions are more biased than their training data\!

Reducing bias in datasets is not enough

Zhao et al, “Men Also Like Shopping: Reducing Gender Bias Amplification using Corpus-level Constraints”, EMNLP 2017

Problem: Bias Amplification

Gender Shades: Intersectionality

MSFT Face++ IBM

40.0 35.0 e

t30.0 a25.0 Rr 20.0 or15.0 r10.0 E5.0 0.0

Buolamwini and Gebru, “Gender Shades: Intersectional Accuracy Disparities in Commercial Gender Classification”, FAT\* 2018

CelebA Dataset: 202k images labeled with 40 binary attributes

Liu et al, “Deep Learning Face Attributes in the Wild”, ICCV 2015

Think Critically about Datasets

Think Critically about Datasets

5\_o\_Clock\_Shadow Arched\_Eyebrows Attractive Bags\_Under\_Eyes Bald Bangs Big\_Lips Big\_Nose Black\_Hair Blond\_Hair Blurry Brown\_Hair Bushy\_Eyebrows Chubby

Double\_Chin Eyeglasses Goatee Gray\_Hair Heavy\_Makeup High\_Cheekbones Male Mouth\_Slightly\_Open Mustache Narrow\_Eyes No\_Beard Oval\_Face Pale\_Skin

Pointy\_Nose Receding\_Hairline Rosy\_Cheeks Sideburns Smiling Straight\_Hair Wavy\_Hair Wearing\_Earrings Wearing\_Hat Wearing\_Lipstick Wearing\_Necklace Wearing\_Necktie Young

Liu et al, “Deep Learning Face Attributes in the Wild”, ICCV 2015

Think Critically about Datasets

Many attributes seem subjective. Who chose the attributes? Why? How are they defined? Who labeled the images?

5\_o\_Clock\_Shadow Arched\_Eyebrows Attractive Bags\_Under\_Eyes Bald Bangs Big\_Lips Big\_Nose Black\_Hair Blond\_Hair Blurry Brown\_Hair Bushy\_Eyebrows Chubby

Liu et al, “Deep Learning Face Attributes in the Wild”, ICCV 2015

Double\_Chin Eyeglasses Goatee Gray\_Hair Heavy\_Makeup High\_Cheekbones Male Mouth\_Slightly\_Open Mustache Narrow\_Eyes No\_Beard Oval\_Face Pale\_Skin

Pointy\_Nose Receding\_Hairline Rosy\_Cheeks Sideburns Smiling Straight\_Hair Wavy\_Hair Wearing\_Earrings Wearing\_Hat Wearing\_Lipstick Wearing\_Necklace Wearing\_Necktie Young

Think Critically about Datasets

Almost no detail in the paper

Datasheets for Datasets

Idea: A standard list of questions to answer when releasing a dataset. Who created it? Why? What is in it? How was it labeled?

Gebru et al, “Datasheets for Datasets”, FAccT 2018

50

Model Cards

Idea: A standard list of questions to answer when releasing a trained model. Who created it? What data was it trained on? What should it be used for? What should it not be used for?

Mitchell et al, “Model Cards for Model Reporting”, FAccT 2019

51

https://github.com/openai/CLIP/blob/main/model-card.md https://modelcards.withgoogle.com/object-detection Adopted by Google, OpenAI (sometimes)

Model Cards

Model Cards

53 https://github.com/openai/CLIP/blob/main/model-card.md

Some models are just for research and not to be deployed. Make it clear\!

Model Cards

• CLIP Model Card: do not use in a deployed system.

• LAION-5B dataset: filtered with CLIP to remove “bad” images.

54

Consent vs Copyright

• Datasets often scraped from the internet without regard for copyright or consent.

• Even if the image has a permissive copyright license, consent of the subjects is still missing\!

• Many datasets are being withdrawn, taken offline.

Birhane and Prabhu, “Large Image Datasets: A Pyrrhic Win for Computer Vision?”, WACV 2021

The Dataset Crisis

56

The future of datasets and models

• Datasheets for Datasets \[Gebru et al, FAccT ‘18\]

• Ethics checks/boards

• Ethics, limitations and social impact statements

• Synthetic Datasets \[Carla, Dosovitsky, CoRL’17\]

• Remove, replace and open \[Asano et al., NeurIPS D\&B’21\]

• Obfuscate humans/faces \[Yang et al., ICML’22\]

• Consent \[Ego4D, Graumann et al., CVPR’22\]

57

\[Asano et al.; NeurIPS Datasets\&Benchmarks ‘21\]

PASS Dataset

58

PASS Dataset

59

ing

Specially designed input that elicits a desirable response

Christian Rupprecht 60

61

Prompt Engineering

T. Kojima et. al 2022 Large Language Models are Zero-Shot Reasoners

62

Prompt Engineering

Christian Rupprecht 63

T. Kojima et. al 2022 Large Language Models are Zero-Shot Reasoners

64 Rob Borovsky, Cater news

65 https://huggingface.co/openai/clip-vit-large-patch14

66 Rob Borovsky, Cater news

https://huggingface.co/openai/clip-vit-large-patch14

67

Annotating with a red circle

68

69

Using VLMs for zero-shot inference

on

Referring expressions comprehension Nam

A

A / Q

Q / AQ The VLM VLM

ear

eye

. . .

bear

nos of a b

70

The cub on the right

. . .

• Generate images with a circle in different locations

• Observation: adding a red circles steers the global descriptor to the annotated region

• Choose the image with the highest correlation to the text

Model Size

Model size only matters when trained on very large datasets

71

Bias Considerations

age of Ranking a 3. 4 missing classes person

– man, 3. woman, man

missing person, murderer

3\. murderer 4. murderer

4\. woman

4\. man

1\. woman

an

1\. murder

1\. murderer

erer

1\. missing

1\. missing person his is an

2\. man

2\. missing

2\. missing person

ing person

2\. woman

2\. woman age of a

3\. missing person

ing person

3\. man

3\. man

3\. murde

3\. murderer 4. murderer

derer

4\. woman

4\. woman

an

4\. man

4\. man

Bias from (unknown\!) training data reflected in the model

72

ing person

erer

3\. man 4. woman

an

3\. murde 4. man

Keeping Bias in Mind

When building a system, ask yourself

• who will benefit and

• who will be harmed.

Act accordingly, be transparent, be clear with limitations.

73

Thanks\!

74

<https://sites.google.com/view/fatecv-tutorial/home>   
<https://www.youtube.com/watch?v=fMym_BKWQzk>   
<https://fairmlbook.org/>   
<https://facctconference.org/>   
<https://www.cs.ox.ac.uk/teaching/courses/2024-2025/LawandCS/>   
<https://www.oii.ox.ac.uk/people/profiles/sandra-wachter/>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/WI2022/598_WI2022_lecture25.pdf>   
<https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm>   
<https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm>   
<https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm>   
<https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm>   
<https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm>   
<https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm>   
<https://www.propublica.org/article/how-we-analyzed-the-compas-recidivism-algorithm>   
<https://fairmlbook.org/classification.html>   
<https://fairmlbook.org/index.html>   
<https://fairmlbook.org/index.html>   
<https://fairmlbook.org/index.html>   
<https://fairmlbook.org/index.html>   
<https://fairmlbook.org/index.html>   
<https://www.youtube.com/watch?v=jIXIuYdnyyk>   
<https://www.washingtonpost.com/technology/2019/10/22/ai-hiring-face-scanning-algorithm-increasingly-decides-whether-you-deserve-job/
