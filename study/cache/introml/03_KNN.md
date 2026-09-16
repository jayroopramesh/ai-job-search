# IntroML (CMP 466) — 03 KNN
> Source: Google Drive file 1PoJV0BLzFYYTD-c_aURuZ4kFt5Tx7_wA · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466- Machine Learning and Data Mining Classification: K-Nearest Neighbors

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

• K-Nearest Neighbor Classi3er (KNN) concept

• KNN example

• KNN in SKLearn\!

2

K-Nearest Neighbor Classifier

Simple algorithm for classi3ca@on.

Stores all the available training samples and classi3es the new samples based on the similarity measure (e.g., distance func@ons).

Basic idea: If it walks like a duck, quacks like a duck, then it’s probably a duck.

Training Records

Compute Distance

Test Record

Choose k of the “nearest” records

3

Unknown KNN- How it works?

record  Requires three things

– The set of labeled records – Proximity metric to compute

distance/similarity between a pair of records

– e.g., Euclidean distance – The value of k, the number of

nearest neighbors to retrieve – A method for using class

labels of K nearest neighbors to determine the class label of unknown record (e.g., by taking majority vote)

KNN- How it works?

To classify an unknown record:

– Compute distance to other training records – Iden@fy k nearest neighbors – Determine the class from the k-nearest neighbors

– Take the majority vote of class labels among the k-nearest neighbors – Weight the vote according to distance

weight factor, w = 1/d2

5

K-Nearest Neighbor Example

Given the following dataset. Predict the class of the green record?

6

K-Nearest Neighbor Example

Record\# Age Loan Class

Calculate distance between the unknown record and every other 1 25 $40,000 Non-Default

record, according to the 2 35 $60,000 Non-Default

Euclidean distance measure 3 45 $80,000 Non-Default 4 20 $20,000 Non-Default

Find 3 nearest neighbors 5 35 $120,000 Non-Default 6 52 $18,000 Non-Default 7 23 $95,000 Default 8 40 $62,000 Default 9 60 $100,000 Default 10 48 $220,000 Default 11 33 $150,000 Default 12 48 $142,000 ?

Distance 102000 82000 62000 122000 22000 124000 47000 80000 42000 78000 8000

Classify the record using KNN?

23

1With K=3, there are two samples of class Y and one sample of class N. The predic@on for the unknown record is Default = Y according to the majority vote.

7

K-Nearest Neighbor Example

Euclidean \!(",\#)=distance √∑$ measure: ("$−\#$)2

where i correspond to the feature number in the features list.

Example of calcula@ng the Euclidean distance between the unknown record (record 12) and record 11:

8

KNN- Effect of the value of k

Choosing the value of k:

◦ If k is too small, sensi@ve to noise points

◦ If k is too large, neighborhood may include points from other classes

X

9

KNN- Effect of the value of k

X X X

(a) 1-nearest neighbor (b) 2-nearest neighbor (c) 3-nearest neighbor

K-nearest neighbors of a record x are data points that have the k smallest distances to x

KNN- Effect of the value of k

Best value for k is found by tesDng a range of values and Ending the value that maximizes the tesDng accuracy

Error

K

11

KNN- Effect of the value of k

What is a valid range for k? Example: In the 3gure, is k = 20 a valid value? and why? No, it is not, because with k=20, the predicted class of any test sample will be always the purple circle class regardless of the features (loca@on) of the test sample.  k should not exceed double the size of the smaller class, in this example, \[1, 15\] is a valid range, (16 will result in a random guess). The best k value can be found by tes@ng this valid range and 3nding the value that maximizes the tes@ng accuracy (as discussed in the previous slide).

'

\-…「

12

KNN- Preprocessing needed

Data preprocessing is oMen required Afributes may have to be scaled to prevent distance measures from being dominated by one of the afributes.

◦ Example:

◦ height of a person may vary from 1.5m to 1.8m

◦ weight of a person may vary from 90lb to 300lb

◦ income of a person may vary from $10K to $1M

◦Time series are ohen standardized to have 0 means and standard devia@on of 1

13

Example: Trying to determine Adam’s shirt size

Training set Test set Amir Lena Adam 175 lbs 115 lbs 140 lbs 5.9 h 5.2 h 6.1 h Large Small ?

What size should Adam wear? Small or Large? Based 1-NN, Adam is closer to Lena (small shirt)

KNN - Feature Scaling Example

ー\\ DCAdam , Amir) = \#Tiiff height2 + (D, fg weight)

\_ - No

\- 17s)2 + (6 .1

\- S .9)2 D(Adam , Lenas = nn+ 2 ("

\-> we will find

diff betreen

Adam & Lena

is small so we think Adam

should wear

like lina- \> which is

wrong

\-> So Prediction

not acc .

cause

weight is domainating since diff in height seems wrong

ICNN +Savees, pred

14

Example: Trying to determine Adam’s shirt size

Training set Test set Amir Lena Adam 175 lbs 115 lbs 140 lbs 5.9 h 5.2 h 6.1 h Large Small ?

Who is Adam closer to in (height + weight) as a new feature?

Same  Lena (small shirt)

KNN - Feature Scaling Example

15

KNN - Feature Scaling Example

Feature MinMax Scaling formula

Value for new (re-scaled) feature: Going back to the example: Find min and max based on the training data: Weightmin = 115 lbs, Weightmax = 175 lbs Heightmin = 5.2 h, Heightmax = 5.9

Apply to test data:

Weight’Adam = Height’Adam = .286

Iscaling

เหย -IIS = 0.41E weight = neignt -IS

\=\_5. z

\= 1

. 286

‰ max

16

Aher Scaling:

Training set Test set Amir Lena Adam 175 lbs  1 115 lbs  0 140 lbs  0.471 5.9 h  1 5.2 h  0 6.1 h  1.286 Large Small ?

AMer scaling the features, who is Adam closer to:

Amir (Large shirt)

KNN - Feature Scaling Example

17

ex ↑

Prev KNN- Effect of Distance Metric

we used Eucedian metrics Here is manhattan also distance

For documents, Euclidean distance may not be the best distance metric. Let’s consider the Pair following 1 (very similar example documents, of two documents:

Pair 2 (very dimerent documents, -\> first doc word 2 with Document 10 common 1:

words out of 12) with no common words) -\> vest not -\> last word "ต้อ keywords ∅ Document 2:

in

notr

in both

in doch not docz Degree O Similarity low

1-exists sout f ㅁ o-Doesnt words Euclidean distance (Pair 1) Euclidean distance (Pair 2) Using Cosine similarity:

\= = = = 10 are \\->Doc ↳

\-> Degree of sima are common

vey similar

Cosine similarity (Pair 1) = =

Cosine similarity (Pair 2) = =

Cosine similarity is befer with text\!

Document 1: 1 1 1 1 1 1 1 1 1 1 1 0

vs

0 0 0 0 0 0 0 0 0 0 0 1 Document 2: 0 1 1 1 1 1 1 1 1 1 1 1

1 0 0 0 0 0 0 0 0 0 0 0

same result for

A-on +10 c 2-\*\#+1010 -0x + (1 -0)2

\* Endledian -\> not appropriate

both 라\] pairs\! ∞ → with This not

isa fext

Scalligiseared ActonRSariy

degree , althought

not acc.

18

\-> KNN- Effect of & Distance Metric

most right use one

For documents, Euclidean distance may not be the best distance metric. Let’s consider the following example of two documents: Pair 1 (very similar documents, Pair 2 (very dimerent documents, with Document 10 common 1:

words out of 12) with no common words)

Document 2:

Euclidean distance (Pair 1) = =

Euclidean distance (Pair 2) = =

Using Cosine similarity:

→ cos( o ) Cosine similarity (Pair 1) = =

Document 1: 1 1 1 1 1 1 1 1 1 1 1 0

vs

0 0 0 0 0 0 0 0 0 0 0 1 Document 2: 0 1 1 1 1 1 1 1 1 1 1 1

1 0 0 0 0 0 0 0 0 0 0 0

same result for both pairs\!

\=r EB.

Cosine similarity (Pair 2) = =

Cosine similarity is befer with text\!

Pair (0)? I t Ca()a7 ' t ( .←

… :(I)(O ) -IOLIJC)a91%

Pair 2 = +a=

(0)(2 ) +10 (0 )0%

18

K-Nearest Neighbor in SKLearn

from sklearn.neighbors import KNeighborsClassi3er \#features: X = \[\[1,1\],\[1,1.5\],\[1,2\],\[2,1\],\[2,2\], \[3,1\],\[3,2\],\[2,3\],\[1,3\],\[1,4\],\[1,5\]\] \#labels y = \[0,0,0,0,0,1,1,1,1,1,1\] X\_test = \[\[1.5,1.5\],\[1,4.5\]\] y\_true = \[0,1\]

classi3er = KNeighborsClassi3er(n\_neighbors = 6) classi3er.3t(X,y)

classi3er.score(X\_test, y\_true)

y\_pred = classi3er.predict(X\_test) y\_pred

from sklearn.metrics import accuracy\_score accuracy\_score(y\_true, y\_pred)k Neighbors Regresser

firstrecord -\> class O →

second , third , forth , Fifth-Class 0

\-> Doesn't really do anything accuracy - (in reg -\> R2 score)

where -\> cal done

19

K-Nearest Neighbor for Regression?

The process for using KNN for a regression task involves the following steps:

– Compute distance to other training records //same as classi3ca@on – Iden@fy k nearest neighbors //same as classi3ca@on – Aggregate target value: takes the average (or median) of the target value of the k- nearest neighbors. //speci3c to regression – Predict: This average/median target value price is the predic@on for the new test record //speci3c to regression

for green, Using3NNทอน

o

ClassiEcaDon Regression

∝ 3NNpredicts star

vs Regression ",inin ""bn G‰we predic

⑨ \_

I M ?

"

c

\# if Dot Area

here aug (1M +20012 + NNes,

Predicted target: Mean / median of the

ส ' -\> woold 3NN chouse

k-nearest neighbors target values

Predicted target: Majority class of the k-nearest neighbors

goocStar since majorits star )

o Tocalculate distance \#HOW -\> find 3NN NN -\> Take aug

(200 class, we

do or majority based on 20

weights

kNN Curse good of simple Dimensionality

als but suffers from I \*Big dataset

me distance Will become all ves similar,

it becomes ecodistance. So

•In high-dimensional spaces (many features), the concept 3NN of distance sense Want 8. make

กา

becomes less meaningful because all points tend to become Similar dist approximately equidistant from each other.

•In high dimensions, the volume of the space grows exponen@ally, so data points become very sparse, and the nearest neighbors may not be “close” in a meaningful way.

As a result, k-NN struggles to 3nd truly nearest neighbors, leading to poor performance. In short, k-NN suRers from the curse of dimensionality because the no@on of "closeness" between data points degrades in high dimensions.

21

\-> Curse of Dimensionality

\*withkNNfeature

Selection 4 -

samples become

ecodistance

• At low dimensionality, the ra@o is very small, showing that the far points are indeed much farther apart than the close points.

• As the dimensionality increases, the ra@o approaches 1, showing that the dis@nc@on between close and far points diminishes, and all points become similarly distant from one another.

• k-NN struggles because all points are roughly equidistant, making it diucult to iden@fy meaningful neighbors.

\>-ses

Biggest

\-> 0 . 2 -\>But if ratio 1 all - close means {

not smart to us

เพ

22

\- K-Nearest Neighbor

\*At the time of

Prediction you do work -\> lazy learner -\>Don't ahead prepare of time Other Alg , Prepare model during training a. - especially during prediction , everything Advantages o The model is very easy to understand. o Building a k-NN model is fast. No explicit learning step. The work is done during the predic@on phase. o Works as a good baseline method Disadvantages o Lazy Learner – Non parametric. o Computa@onally expensive (slow), depends on the size of the datasets and o o number of features. Since done Sensi@ve Selec@on to of the right scale proximity of the measure data. -\> Dat is essen@al. not scaledTowrong wer Prediction o Can produce arbitrarily shaped decision boundaries o Redundant (irrelevant) afributes can create problems o Missing afributes are hard to handle \> -can't o Sumers from the curse of dimensionality.

have unclear

daten

23

Learning Outcomes

1\. Perform machine learning steps including data prepara@on, task iden@3ca@on, model selec@on, and evalua@on.

2\. Employ mathemaDcal methods to explain the theoreDcal aspect of machine learning and data mining techniques.

3\. Select appropriate supervised learning methods including classiEcaDon and regression for given problems and datasets.

4\. Use unsupervised learning methods such as clustering and associa@on rule mining to discover paferns and rela@onships in datasets.

5\. Apply feature selec@on and dimensionality reduc@on methods.

6\. Use state-of-the-art soMware to explore and solve pracDcal machine learning problems.

24
