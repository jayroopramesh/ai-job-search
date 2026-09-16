# IntroML (CMP 466) — 05 Model Overfitting
> Source: Google Drive file 1vQU42GjO3J97niaPmhTxHcOiy7tX2Xt_ · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466- Machine Learning and Data Mining

Chapter 3: Model Overfitting

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

Outline

• Model Overfitting

• Model Selection

• Model Evaluation

Example Da

2

Example Data Set

Loading…

4

Two class problem:

\+ : 5200 instances

• 5000 instances generated from a Gaussian centered at (10,10)

• 200 noisy instances added

o : 5200 instances

• Generated from a uniform distribution

10 % of the data used for training and 90% of the data used for testing

Increasing number of nodes in Decision Trees

\-> hebigger neemalle the error

5

10%O

Decision Tree with 4 nodes

X2

X1

Loading…

6

Decision boundaries on Training data

Decision Tree with 50 nodes

Decision boundaries on Training data

so splits=\> classify all

points =\> JThen Est =\> ree

boundries The is date

ve like + ceptPrev

correctly creating points cdosse in , circle region

Traing shoul guidanc bespecific sample providenot = more complicated but the smaller 4 nodes&

error

training

evillaeamento much =\>Trying to dassify data correctly \*4 nodes So more nodes general

better Coptimistic)

training enor

7

Model Over

Which tree is better?

Decision Tree with 4 nodes Decision Tree with 50 nodes

Which tree is better ?

Betti Ma acirce

いmis region wouldpredict,u品barbiirde

& is -\> not well for testing prop.

↳ 4 nodes

8

Model Overfitting

Model Over

Overfitting: when model is too complex, training error is small but test error is large

Underfitting: when model is too simple, both training and test errors are large

·edttirhi, testine ee ↑Boten

in/

osimpleeedmrn onnfaccundypredict 옮며

9

Model Overfitting

Model Over

Double of 20% ) amount date . F maining 810%

↳ more trainggdata abeese

Using twice the number of data instances

10

Model Overfitting

Using twice the number of data instances

Reasons for

• If training data is under-representative, testing errors increase and training errors decrease on increasing number of nodes

• Increasing the size of training data reduces the difference between training and testing errors at a given number of nodes

Decision Tree with 50 nodes Decision Tree with 50 nodes

↑Stillsustiteedatee

11

Reasons for Model Overfitting

Not enough training data High Model Complexity

Notes on O

Loading…

12

↳ less data ↳model too complex

Notes on Overfitting

• Overfitting results in decision trees that are more complex than necessary

• Training error does not provide a good estimate of how well the tree will perform on previously unseen records

• Need ways for estimating generalization errors

Model Selec

\_↳how tree will do on

testing error

13

Model Selection

Performed during model building

Purpose is to ensure that model is not overly complex (to avoid overfitting)

Need to estimate generalization error

◦Using Validation Set

◦Incorporating Model Complexity

Model Selec

\=\>need to apply

earlyStopping Criteria =\>play withhyperparameeeeene

14

Model Selection: Using Validation SetDivide training data into two parts:

◦Training set:

◦ use for model building

◦Validation set:

◦ use for estimating generalization error

◦ Note: validation set is not the same as test set

Drawback:

◦Less data available for training

Model Selec

\->we don'ttouch

testing data

\-> testing error & based

on that

choose hyperparameter based -\>optimizing

On his set

15

\->Model Incorporating Selection: Model preser cause better simple Complexity

erran

at models

testies date

Rationale: Occam’s Razor- also called the “law of parsimony”: is a mental model which states that “it is futile to do with more what can be done with fewer”—in other words, the simplest explanation is most likely the right one. In machine learning:

◦Given two models of similar generalization errors, one should prefer the simpler model over the more complex model

◦A complex model has a greater chance of being fitted accidentally

◦Therefore, one should include model complexity when ex . evaluating a model

ㅂ of nodes

\_ Dongudar

S

Gen. a I Error(Model) eralization err = Train.Error(Model, training α enror

Train.Data) + x Complexity(Model)

Estimating Trees

16

I8 O s δ gen err =

Train error

IS I → \[ -\> gen error

gen error =

Train error

teenodes 28

Totcel I oJ records

let More fro y α Better wher comeraining o

erron -Better generaltee slescomplex,conknrHogen err

0 7 539 ↓ alu 021133 "4

2µ 증

\- 금

\+ 0어류

classification enori M

4 =overall training error: 装 4/24 →剥芸な ()装

s set always

a30 대 1 2a for 1T-

4이고a for RT ef \< to penalize complexity

\=\> optimistic assesment

ofthtreeat (like home)

Model Selection for Decision Trees

Pre-Pruning (Early Stopping Rule)

◦Stop the algorithm before it becomes a fully-grown tree

◦Typical stopping conditions for a node:

◦ Stop if all instances belong to the same class

◦ Stop if all the attribute values are the same

◦More restrictive conditions:

◦ Stop if number of instances is less than some user-specified threshold (min\_samples\_splits in SKLearn)

◦ Stop if class distribution of instances are independent of the available features (e.g., using 2 test)

◦ Stop if expanding the current node does not improve impurity measures (min\_impurity\_decrease in SKLearn)

◦ Stop if estimated generalization error falls below certain threshold (ccp\_alpha in SKLearn)

Model Selec

\* CCP(x)

\->cost

complexity -used fur

minimal cost -\> Default complex in

pruning -\> trying to ensure min complexit

\-> Default : 0

, so biggest free but not bestbree

20

Model Selection for Decision Trees

Post-pruning

◦Grow decision tree to its entirety

◦Subtree replacement

◦ Trim the nodes of the decision tree in a bottom-up fashion

◦ If generalization error improves after trimming, replace sub-tree by a leaf node

◦ Class label of leaf node is determined from majority class of instances in the sub-tree

◦Subtree raising

◦ Replace subtree with most frequently used branch

Example of

21

Setting a is imp , if \< would split cause traing model always cal errord error & deades

When to Stop

gen(error) =

\+o

\= 10

. 5/30

\=Before splitting better, aly stops wont Split error: trainig - 9/30

\=\> 오 + 0 s/%) ㆀ

"/30

Entropee/-

\> not to decide to Genee ↳ Split or not

mey choose which

attribute to Split at

To Split or not- gen error

\=ys set early stopping criteria

To prevent oursittingenoughdanaa

trying to avoid complex

models which one

will make -\> if smaller min-impurity-decrease

tree less Nee ↳ can set to 10% this means if Split cause overfitted impurityd by may than 10 % =\> Split else not - avoidOf

Model Evaluation Purpose:

◦To estimate performance of classifier on previously unseen data (test set)

Two approaches:

1\. Holdout

◦Reserve k% for training and (100-k)% for validation

◦Random subsampling: repeated holdout

Cross-valida

\->Divide dataset

into training & Op testing Divide inw

training 후

Validation

23

Cross-validation Example

2\. k-fold cross-validation (CV)

o It is a test where the training set is split into k smaller sets. For

each of the k "folds":

o A model is trained using k-1 of the folds as training data;

o The resulting model is validated on the remaining k part of

the data

o The performance measure reported by k-fold cross-validation is

then the average of the values computed in the loop.

o This approach can be computationally expensive.

"This approach involves randomly dividing the set of observations into k groups, or folds, of approximately equal size. The first fold is treated as a validation set, and the method is fit on the remaining k-1 folds" An Introduction to Statistical Learning, 2013, Page 181

24

Cross-validation Example

Example of 3-fold cross validation

• Model1: Trained on Fold2 + Fold3, Tested on Fold1

• Model2: Trained on Fold1 + Fold3, Tested on Fold2

• Model3: Trained on Fold1 + Fold2, Tested on Fold3

Example of 5-fold cross validation

Cross-valida

Go arameter with hyperp ← →

that maximizes train

/ Then n ↳ we do cross validation d -\>split data into Chunks/folds asso me acrameathen test model all doesnt C see it

train modelfolds Cunseentodel)

on greenon 후 test Bue fold =\>Do that pmodevas

never rained . until eaccomes =\>Do this to get & accuracy sad ↳ makesSure

a split after a fold , results balance

to ensure you

train moder on all data and test on all data

25

Cross-validation Example

Number of folds depend on:

Number of samples, classes and computation time capacity

Cross-valida

Site of data \# Of samples) & \#o classes

\=\> must divide correctly

\_↳ morefolds

more runs

\=\> most do it

smarty

\\

26

Cross-validation Example

Repeated cross-validation

◦Perform cross-validation a number of times

◦Gives an estimate of the variance of the generalization error Stratified cross-validation

◦Guarantee the same percentage of class labels in training and test

◦Important when classes are imbalanced and the sample is small Use nested cross-validation approach for model selection and evaluation

Cross Valida

one class 30%

other -\>very important for imbalanced datasets 1 70%

ㅛ make sure후 training testing

are represent- ative

27

Cross Validation in SKLearn

Cross Validation in SKLearn:

from from sklearn.model\_selection sklearn.model\_selection import import cross\_validate cross\_validate

from sklearn.model\_selection import cross\_val\_score

28

Learning O

for eachcan report -Bered e

runmyf resub acasae

precision

\=\> just tell

now many foldsdces it

everything & gives \# of sads results =\>Gives metrics

you are intested

in

Learning Outcomes

1\. Perform machine learning steps including data preparation, task identification, model selection, and evaluation.

2\. Employ mathematical methods to explain the theoretical aspect

of machine learning and data mining techniques.

3\. Select appropriate supervised learning methods including classification and regression for given problems and datasets.

4\. Use unsupervised learning methods such as clustering and association rule mining to discover patterns and relationships in datasets.

5\. Apply feature selection and dimensionality reduction methods.

6\. Use state-of-the-art software to explore and solve practical machine learning problems.

29

Loading…
