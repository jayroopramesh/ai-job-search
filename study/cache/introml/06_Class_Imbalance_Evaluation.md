# IntroML (CMP 466) — 06 Class Imbalance and Evaluation
> Source: Google Drive file 1w06wFqMjMwoF9H7-xSOA1J6MVOt87Z_h · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466- Machine Learning and Data Mining

Chapter 4: Class Imbalance Problem and Evaluation

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

Outline

• Imbalanced classes

• Confusion Matrix

• Classification (accuracy) Measure

• Alternative measures

• Model Evaluation

• Handling Class Imbalanced Problem

• Model Evaluation in SKLearn

Class Imbal

2

Class Imbalance Problem

Lots of classification problems where the classes are skewed (more records from one class than another)

◦Credit card fraud

◦Intrusion detection

◦Defective products in manufacturing assembly line

◦Early screening for breast cancer detection

Key Challenge:

◦Evaluation measures such as accuracy are not well- suited for imbalanced class 3

Problem wi

Loading…

Problem with Accuracy

Evaluation measures such as accuracy is not well-suited for imbalanced class Consider a 2-class problem

◦Number of Class NO examples = 990

◦Number of Class YES examples = 10 If a model predicts everything to be class NO, accuracy is 990/1000 = 99 %

◦This is misleading because the model does not detect any class YES example

◦Detecting the rare class is usually more interesting (e.g., frauds, intrusions, defects, diseases, etc.)

4

Confusion M

\= Its misleading specially anance

↑ imb dasses

Theandpred

\-> would expect perfect model , when its

acc ahorrible model

Confusion Matrix

Confusion Matrix:

PREDICTED CLASS

ACTUAL CLASS

Class=Yes Class=No

Class=Yes a b

Class=No c d

a: TP (true positive)

b: FN (false negative)

c: FP (false positive)

d: TN (true negative)

5

Accuracy

hae

"a,d

c -100 \>foJ Loading… samples 0 =\>PredictionTrue ㆁ Positive ↳actual

predicted in when

Dot

class

0-

his O of when

predicted in σ aasS enotindasis

→Bener

Accuracy

PREDICTED CLASS

Class Yes

Class=No

Class=Yes

ACTUAL

CLASS Class=No

Most widely-used metric:

Correctly classified samples

a

b

(TP)

(FN)

C

d

(FP)

(TN)

a+d

TP+TN

Accuracy =

\=

a+b+c+d

TP+TN+FP+ FN

Accuracy

Most widely-used metric:

Correctly classified samples

PREDICTED CLASS

ACTUAL CLASS

Class=Yes Class=No

Class=Yes a

(TP)

b (FN)

Class=No c

(FP)

d (TN)

6 Which mod

accuracy =dall

Bad model

99 % ↑ that immediates doe had, since soo doWhich model F8 a device is better? dangerous surgenwill

↑

although accuracy

& wrong not good atall not or neede surgen

繼 s99%

If some we detect I cancerboth need need , with

has

models

If

B to

응. s 0. Alternative =

Since detect positiveBetter false Jasse will all cases

. Doest miss any Love sample. to delect positivethen (-vel

. Even in realfecause rey de noen als

50%

AB

PREDICTED

ACTUAL

Class=Yes Class=No

Class=Yes 0 10

Class=No 0 990

PREDICTED

ACTUAL

Accuracy: 99%

Class=Yes Class=No

Class=Yes 10 0

Class=No 500 490

Accuracy: 50%

7

\=\>accray : Generic

\-> Outoftroee a mayareaceθ -outpredicted yes as yes how many were caught. identified

↳ aug of

two

s how many llg nodass

Alternative Measures

Example: we have a pond with known number of fish within. Our goal is to build a model that catches red fish. The precision metric, is about exactness and quality: how many of the fish caught are red. The recall metric is about the quantity: how many of the red fish we caught.

High precision (all fish caught are red) Low recall (we missed many red fish)

10 High recall (we caught most of the red fish) Low precision (we also caught many blue fish)

Alternative

Precision -\> our of trose

red , now many

accred.

Recall -\> how caught many red \_acred + not Caught

red\_ red + nod recaf

caught 6 p 2↑ 듦

→

\_

\_ 、

I blue

\-

←

M

\_

โ

\_

^ ^

f 떼-\> 6/x7

ㅿ

auss yes :\_Recall.=1 10

\+0 precision:toto

\-> 0S의recal :a80-980 + 10 =\> 98199

ver

Alternative Measures

PREDICTED CLASS

Class=Yes Class=No

ACTUAL CLASS

Class=Yes

10

0

Class=No

10

980

For class No

980

Precision (p)

\=

\= 1

980 +0

980

\=

\= 0.99

Recall (r)

980 + 10

F-measure (F)

Accuracy

\=

2\*1\* 0.99

\=

1 +0.99

990

1000

\= 0.99

Precision (p)

\=

d

b+d

d

Recall (r)

c+d

2rp

\= 0.995

F-measure (F)

\=

r + p

12

\->Betzer model

Bod a precision: = 0 .

No : +形recall

\=t0="

↓armonic mean of recaystion

\- false positivene

↳ falsenegateae

Measures of Classification Performance

PREDICTED CLASS

Recall Sensitivity = TP Rate

Yes

No

ACTUAL CLASS

Yes TP

FN

No FP

TN

Specificity TN Rate =

TN

TN+FP

TP

TP+ FN

Example: Covid-19 PCR Test\* Sensitivity = TPR

FP Rate α =

FP

TN+FP

\= 1 specificity

80%

FN Rate = B =

FN

FN+TP

\= 1 sensitivity

FNR=1-TPR = 20%

If you have COVID→ there is an 80% chance test will come out positive, and 20% chance the test will come out negative (FNR)

Specificity TNR = 98%-99% FPR 1-TNR = 1%-2%

If you do NOT have COVID→ there is an 98-99% chance test will come out negative, and 1-2% chance the test will come out positive (FPR)

Thus, if you go to the lab and do a PCR test. If the result come out negative, how much you trust it? Look at the sensitivity.. The FNR is 20%, which means there is a 20% chance that you are positive but the test came out negative (you were positive but missed because of the 'relatively' low sensitivity of the test).

Similarly, if you go to the lab and do a PCR test. If the result come out positive, how much you trust it? Look at the specificity. The FPR is very low (1-2%), which means there is a very low probability (1-2% ) that you are negative but the test came out positive.. Which means if the result comes out positive then you are most probably positive.

\*Source: https://www.cap.org/member-resources/articles/how-good-are-covid-

19-sars-cov-2-diagnostic-pcr-tests

16

Example PCR Test -Predictor TPR ↳ 80% sensitivity -\> tre positive have , Covid so if you there is Fur b

20% an test 80% will chance be te can come as negative

TNR Specificity - 98-99 % of time if you don't have

Covid , it will come out negative FPR ↳ 1-2 % will come

as the

\=\> we must the positive result more

Sensitivity - The positive rate -\> 80% of time result will

come +ve FN2+ 20 %, I , there is a 20% Chance you are sick but result-re specificity -\> 98% -99 %, the negative

fPR -\> 1 % - 2% =\> So most likely all the positive is ACC positive

. Trust positive more \!\!\!

precision-

The thePrecision- 0 . 0 \_Predicted

as

(yes) -\>\> so

\-> 5o0o

(wo)

True \_ ↑ ‰ Predicted Yes

101s0 β→ Fre

Act

Tre

ってs1 so

쯤

suosso

s 웅

↳ only do 1 vs all

thecasdived↑ do buideen Basses to aerisalor 0prearcted nt . virginica

% 8 S

오 ↑. parts TN รวมO

Opmisama ㆁ -\> positive , Belongas

dass

evesting 8ltvel

\-ve ensebut

predictedascase

comes in exam

13 TP

Precision

\= TP Ip + FP te σ TP fN fN For Class Recal setosa

\= TP \_ TD+ fN

\-eCfp 5 P TN TN in in -\> Setusa (tre) , others (-ve) Precision=

TP =≈ — = 凸\_— Predicted Peccul ⼆正 )3+ 0 + 0 = 凸 = コ ㄧㄢ -. fP TN TP fNn e in

10 TP

Actual F - score == 吾

\= ュ

For versicolor

^ Precison

Precision = 正 Predicted

\= = 응= ⽫

≡ = 6 . 62s - ve ( ㆁ TW TN 印 = \_ a =0.8

IN TN FP gto ㆁ Recall

\=

twe

fN FN TP 응의 Recall = ⼀ Act P Trve ㆀ -- measure == 0 f measure atr

2\) find average & weighted Precision , recall

, 3

f-score

Aug precision = E+ 00 = 0. 167

weighted Precision

\= 13 (1) +(1) +go to

\=

0.76315789 + 0.14210s2s = 0.90S

Applications from Medicine

The blue region is the ground truth segmentation of a mitochondrion

The red region is the result obtained using an automated segmentation algorithm

TP is the intersection of red and blue regions, i.e. the correctly segmented piece of mitochondrion.

FN is the only blue area, i.e. the part of mitochondrion

FN

segmented as background.

FP is the only red area, i.e. the background segmented as mitochondrion.

TN

TN is the rest of the image, i.e. the correctly segmented

TP

background.

FP

Figure from:

Cetina, K., Buenaposada, J.M. & Baumela, L. Multi-class segmentation of neuronal structures in electron microscopy images. BMC Bioinformatics 19, 298 (2018). https://doi.org/10.1186/s12859-018-2305-0

22

ROC (Receiver Operating Characteristic)

A graphical approach for displaying trade-off between detection rate and false alarm rate

Developed in 1950s for signal detection theory to analyze noisy signals

ROC curve plots TPR against FPR

о

Performance of a model represented as a point in an ROC curve

23

ROC Curve

(TPR, FPR):

1

(0,0): declare everything to be negative class

(1,1): declare everything

to be positive class

(1,0): ideal

Diagonal line:

о

о

Random guessing

Below diagonal line:

prediction is opposite of the true class

True Positive

0.9

0.8-

0.7-

0.6

0.5-

0.4

0.3

0.2

0.1

n

L

n

0.1

0.2

0.3

0.4

T

T

T

0.5

False Positive

0.6 0.7 0.8 0.9

24

1

ROC Curve

A discrete classifier that returns only the predicted class gives a single point on the ROC space

To draw ROC curve, classifier must produce continuous- valued output

O

O

Outputs are used to rank test records, from the most likely positive class record to the least likely positive class record

By using different thresholds on this value, we can create different variations of the classifier with TPR/FPR tradeoffs

Many classifiers produce only discrete outputs (i.e., predicted class)

O

How to get continuous-valued outputs?

O

Decision trees, rule-based classifiers, neural networks, Bayesian classifiers, k-nearest neighbors, SVM

25

Example: Decision Trees

Decision Tree

x1 \<13.29

x2 \< 12.63

Continuous-valued outputs

x2 \< 12.63

x2 \< 17.35

x1 \< 13.29

x1 \< 6.56

x1 \<2.15 A

x1 \<6.56

\+

Ax1 \<7.24

Ax2 \< 8.64

\+

\+

x2 \<1.38

\+

O

\+

0.107

x1 \<12.11

x1 \<2.15 A

Ax2 \< 17.35

0.059

0.220

x1 \< 7.24

x2 \< 8.64

0.071

x1 \<12.11

x2 \<1.38 A

0.164

0.727

Ax1 \<18.88

0.143

0.669

о

\+

This score can be the percentage of \#samples of class o/total\# samples in that node

x1 \<18.88

0.271

0.654

0

ROC Curve Example

x2 \< 12.63

x1 \< 6.56

0.107

x1 \< 13.29

0.059

x1 \<2.15 A

x2 \< 17.35

x1 \< 7.24

x2 \< 8.64

0.071

x2 \< 1.38 A

0.164

0.143

0.669

0.220

x1 \< 12.11

0.727

Ax1 \<18.88

0.271

0.654

0

Training set

Predict as class "o" if the ratio of class "o" is greater then the threshold a

Predicted Class Class o Class +

a= 0.3

Predicted Class

α = 0.7

Class o

Class +

Actual

Class o

645

209

Actual

Class o

181

673

Class Class +

298

948

Class

Class +

78

1168

27

0.016

0.014

ROC Curve Example

0.012

Negative Class

0.01

TN

TP

0.008

0.006

0.004 H

0.002

1

0.9

0.8

Positive

Class

0.7

True Positive

0.6

0.5

0.4

0.3

FN

FP

0.2

\-20

\-15

\-10

\-5

0

5

10

15

20

t

0.1

Classifying the left part as negative,

and the right part as positive

0

0 0.1 0.2

0.3

0.4

At threshold t:

T

T

0.5 0.6 0.7 0.8 0.9 False Positive

1

When AUC is 0.7, it means there is a 70% chance TPR-0.5, FNR=0.5, FPR=0.12, TNR=0.88

that the model will be able to distinguish

between positive class and negative class.

Demonstration of ROC

https://arogozhnikov.github.io/2015/10/05/roc-curve.html

28

ROC Curve Example

Negative Class

Positive Class

TPR

AUC = 1

ROC

WAL

TN

0.5

Threshold

Red means positive population

TP

1

FPR

Green means negative population

Red distribution curve is of the positive class (e.g., patients with disease) and the green distribution curve is of the negative class (patients with no disease).

This is an ideal situation. When two curves don't overlap at all means model has an ideal measure of separability. It is perfectly able to distinguish between positive class and negative class.

Source: https://towardsdatascience.com/understanding-auc-roc-curve-68b2303cc9c5

29

ROC Curve Example

Negative Class Positive Class

0.5

Threshold

Red means positive population

Green means negative population

AUC = 0.5

ROC

TPR

0

0

FPR

.

This is the worst situation. When AUC is approximately 0.5, the model has no discrimination capacity to distinguish between positive class and negative class.

Source: https://towardsdatascience.com/understanding-auc-roc-curve-68b2303cc9c5

30

ROC Curve Example

Negative Class

Positive Class

TP

0

0.5 Threshold

Red means positive population

Green means negative population

AUC 0 TPR

TN

1

ROC

0

0

1

FPR

When AUC is approximately 0, the model is actually reciprocating the classes. It means the model is predicting a negative class as a positive class and vice versa.

Source: https://towardsdatascience.com/understanding-auc-roc-curve-68b2303cc9c5

31

How to Construct an ROC curve

\+

Use a classifier that produces a continuous-valued score for each instance

Instance

Score

True Class

1

0.95

2

0.93

\+

•

3

0.87

4

0.85

\-

5

0.85

6

0.85

\+

7

0.76

\-

8

0.53

9

0.43

\-

10

0.25

\+

\-

\+

·

•

The more likely it is for the instance to be in the + class, the higher the score

Sort the instances in decreasing order according to the score

Apply a threshold at each unique value of the score

Count the number of TP, FP,

TN, FN at each threshold

·

·

TPR = TP/ (TP + FN)

FPR = FP / (FP + TN)

32

How to Construct an ROC curve

Class

\+

27

\+

Threshold \>=

0.25

0.43

0.53

0.76

0.85

0.85

0.85

0.87

0.93

0.95

1.00

TP

5

4

4

3

3

3

3

2

1

0

FP

5

5

4

4

3

2

1

1

0

0

0

TN

0

0

1

1

2

3

4

4

5

5

5

FN

0

1

1

2

2

2

2

3

3

4

5

11

TPR

1

0.8

0.8

0.6

0.6

0.6

0.6

0.4

0.4

0.2

0

FPR

1

1

0.8

0.8

0.6

0.4

0.2

0.2

0

0

0

Classify samples as

\+ if score

is above

threshold

0.9

0.8

0.7

0.6

ROC Curve:

0.5

0.4

0.3

0.2-

0.1

0

0

0.1

J.2

0.3

04

0.5

0.7 08 0.9

33

True Positive Rate

Using ROC for Model Comparison

1

0.9

M

0.8

0.7

0.6

0.5

0.4

0.3

0.2-

M

0.1

0

0

0.1 0.2

0.3

0.4 0.5 0.6

0.7

0.8

0.9

1

False Positive Rate

T

No model consistently outperforms the other

OM, is better for

small FPR

M2 is better for large FPR

Area Under the ROC curve (AUC)

Ideal:

• Area = 1

Random guess:

• Area = 0.5

34

Dealing with Imbalanced Classes - Summary

Many measures exists, but none of them may be ideal in all situations

• Random classifiers can have high value for many of these measures

о

TPR/FPR provides important information but may not be sufficient by itself in many practical scenarios

• Given two classifiers, sometimes you can tell that one of them is strictly better than the other

C1 is strictly better than C2 if C1 has strictly better TPR and FPR relative to C2 (or same TPR and better FPR, and vice versa)

• Even if C1 is strictly better than C2, C1's F-value can be worse than C2's if they are evaluated on data sets with different imbalances

• Classifier C1 can be better or worse than C2 depending on the scenario at hand (class imbalance, importance of TP vs FP, cost/time tradeoffs)

35

Which Classifier is better?

T1

T2

Class Yes

ACTUAL CLASS

Class=No

PREDICTED CLASS

Class Yes

Class=No

50

50

1

99

PREDICTED CLASS

Class Yes

Class=No

Class Yes

99

1

ACTUAL

Class=No

10

90

CLASS

Precision (p) = 0.98

TPR = Recall (r) = 0.5

FPR = 0.01

TPR/FPR = 50

F measure = 0.66

Precision (p) = 0.9

TPR = Recall (r) = 0.99

FPR = 0.1

TPR/FPR 9.9

T3

PREDICTED CLASS

Class Yes

Class=No

Class=Yes

99

1

ACTUAL CLASS

Class=No

1

99

F-measure =

€0.94

Precision (p) = 0.99

Recall (r) = 0.99

TPR =

FPR = 0.01

TPR/FPR=99

F measure = 0.99

36

Which Classifier is better?

T1

T2

T3

PREDICTED CLASS

Class Yes

Class=No

Class Yes

50

50

ACTUAL CLASS

Class=No

10

990

PREDICTED CLASS

Class Yes

Class=No

Class Yes

99

1

ACTUAL CLASS

Class=No

100

900

PREDICTED CLASS

Class Yes

Class=No

Class Yes

99

1

ACTUAL

CLASS

Class=No

10

990

Medium Skew case

Precision (p) = 0.83

TPR = Recall (r) = 0.5

FPR = 0.01

TPR/FPR = 50

F-measure = 0.62

Precision (p) = 0.5

TPR = Recall (r) = 0.99

FPR = 0.1

TPR/FPR 9.9

F measure = 0.66

Precision (p) = 0.9

TPR Recall (r) = 0.99

FPR = 0.01

TPR/FPR = 99

F measure = 0.94

37

Which Classifier is better? High Skew case

T1

T2

T3

ACTUAL CLASS

Class Yes

Class=No

PREDICTED CLASS

Class Yes

Class=No

50

50

100

9900

PREDICTED CLASS

Precision (p) = 0.3

TPR = Recall (r) = 0.5

FPR = 0.01

TPR/FPR = 50

F-measure = 0.375

Precision (p) = 0.09

TPR = Recall (r) = 0.99

FPR = 0.1

TPR/FPR = 9.9

Class Yes

Class=No

Class Yes

99

1

ACTUAL

Class=No

1000

9000

CLASS

F

PREDICTED CLASS

\- measure = 0.165

Precision (p) = 0.5

\-

TPR Recall (r) = 0.99

FPR = 0.01

Class Yes

Class=No

Class Yes

99

1

ACTUAL CLASS

Class=No

100

9900

F

TPR/FPR=99

\- measure = 0.66

38

Handling Class Imbalance Problem

Many approaches to handle class imbalance:

Sampling-based approaches

Cost-sensitive classification

о

Misclassifying rare class as majority class is more expensive than misclassifying majority as rare class

39

Sampling-based Approaches

Modify the distribution of training data so that rare class is well-represented in training set

1\. Over-sampling the rare class: increase the number of

training samples of the rare class.

Advantages

• No information loss.

о

Outperforms under-sampling

Disadvantages

• Increases the likelihood of overfitting since it replicates the

minority class events.

40

Sampling-based Approaches

2\. Under-sampling the majority class: reduce the number.

of training samples of the majority class.

Advantages

о

Help improve run time and storage problems.

Disadvantages

• Can discard potentially useful information important to build the classifier.

• The sample set chosen by random under-sampling may be a biased set. May not be an accurate representative of the population, resulting in inaccurate results with the actual test dataset.

41

Handling Imbalanced Classes using implemented research methods

Imbalanced

learn

There are no built-in over/under-sampling methods in sklearn, but implemented methods are available in:

Oversampling:

https://imbalanced-learn.org/stable/over\_sampling.html

Undersampling:

https://imbalanced-learn.org/stable/under\_sampling.html

A combination of both

https://imbalanced-learn.org/stable/combine.html

42

Cost-sensitive classification

PREDICTED CLASS

Class Yes

Class=No

ACTUAL

CLASS Class Yes

f(Yes, Yes)

f(Yes,No)

Class=No

f(No, Yes)

f(No, No)

Class=No

Cost

PREDICTED CLASS

Matrix

C(i, j)

Class=Yes

Class Yes

ACTUAL

CLASS Class=No

C(No, Yes)

C(No, No)

C(Yes, Yes) C(Yes, No)

C(i,j): Cost of misclassifying class i sample as class j

Cost = ΣC(i, j)× f(i, j)

43

Computing Cost of Classification

Cost PREDICTED CLASS

Matrix

C(i,j) +

\-

ACTUAL CLASS

\+

\-1

100

1

Model PREDICTED CLASS

Model

M₁

M2

PREDICTED CLASS

\+

\-

\+

\-

ACTUAL CLASS

ACTUAL

\+

150

40

\+

250

45

CLASS

60

250

5

200

Accuracy =

150+250

150+40+60+250

\= 80%

Accuracy =

250+200

250+45+5+200

\= 90%

Recall: 0.79,

Recall: 0.85,

Precision: 0.71

Cost 150 (-1) + 40(100) + 60(1) + 250(0) = 3910

Precision: 0.98

Cost 250 (-1) + 45(100) + 5(1) + 200(0) = 4255

44

Handling Imbalanced Classes in SKLearn.

scikit

learn

In sklearn, you can adjust the class weights for unbalanced datasets by tweaking the class\_weight parameter:

class\_weight: dict, list of dict or "balanced", default=None

If 'balanced', class weights will be adjusted automatically, inversely proportional to class frequencies in the input data

as n\_samples/ (n\_classes\* np.bincount(y)).

If a dictionary is given, keys are classes and values are corresponding class weights. If None is given, the class weights will be uniform.

https://scikit-

learn.org/stable/modules/generated/sklearn.utils.class\_weight.compute\_class\_weight.ht

ml

45

Handling Imbalanced Classes in SKLearn

Using the "balanced" mode in:

class\_weight = 'balanced'

Consider a 2-class problem

• Number of Class NO examples = 990

• Number of Class YES examples = 10

scikit

learn

If 'balanced', class weights will be adjusted automatically, inversely proportional to class frequencies in the input data

as n\_samples/ (n\_classes\* np.bincount(y)).

Thus, class\_weight for class NO: 1000/(2\*990) =0.5

class\_weight for class YES: 1000/(2\*10) = 50

46

Evaluation Measures in SKLearn

scikit

learn

Classification metrics:

https://scikit-learn.org/stable/modules/model evaluation.html\#classification-metrics

f1 score(y\_true, y\_pred\[, labels, ...\])

confusion matrix(y\_true, y\_pred\[, labels, ...\])

precision score (y\_true, y\_pred\[, labels, ...

recall\_score(y\_true, y\_pred\[, labels, ...\])

precision\_recall fscore\_support(y\_true, y \_pred)

classification\_report(y\_true, y\_pred \[,...\])

Compute the F1 score, also known as balanced F-score or F-measure

Compute confusion matrix to evaluate the accuracy of a classification.

Compute the precision

Compute the recall

Compute precision, recall, F-measure and support for each class

Build a text report showing the main classification metrics

47

Evaluation Measures in SKLearn

scikit

Examples

\>\>\> from sklearn.metrics import confusion\_matrix

\>\>\> y\_true = \[2, 0, 2, 2, 0, 1\]

\>\>\> y\_pred \[0, 0, 2, 2, 0, 2\]

\>\>\> confusion\_matrix(y\_true, y\_pred) array(\[\[2, 0, 0\],

\[0, 0, 1\],

\[1, 0, 2\]\])

\>\>\> from sklearn.metrics import accuracy\_score

\>\>\> y\_pred

\>\>\> y\_true

\=

\[0, 2, 1, 3\]

\=

\[0, 1, 2, 3\]

\>\>\> accuracy\_score (y\_true, y\_pred)

0.5

\>\>\> accuracy\_score (y\_true, y\_pred, normalize=False)

2

learn

48

Learning Outcomes

1\. Perform machine learning steps including data preparation, task

identification, model selection, and evaluation.

2\. Employ mathematical methods to explain the theoretical aspect of

machine learning and data mining techniques.

3\.

4\.

Select appropriate supervised learning methods including classification and regression for given problems and datasets.

Use unsupervised learning methods such as clustering and association rule mining to discover patterns and relationships in datasets.

5\. Apply feature selection and dimensionality reduction methods.

6\.

Use state-of-the-art software to explore and solve practical machine learning problems.

49
