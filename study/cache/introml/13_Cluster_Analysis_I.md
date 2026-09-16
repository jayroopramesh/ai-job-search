# IntroML (CMP 466) — 13 Cluster Analysis I
> Source: Google Drive file 1aQJqybPZ-k1BN-x5SztbF8iMDgO0dXMx · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466- Machine Learning and Data Mining

\-unsupenised Chapter 7- Cluster -\>grouping

Analysis: Basic Concepts and Algorithms I =\>Based on similarity Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

• Clustering concept

• Clustering methods

• Clustering in SKLearn\!

2

What is Clustering?

Given a set of objects, place them in groups such that the objects in a group are similar (or related) to one another and different from (or unrelated to) the objects in other groups -Distance betwee

n

dusesmall Inter-cluster Intra-cluster distances are

points within

distances are maximized same minimized

⑥ small -\> Distance Between clusters

slarge

3

Applications -\> of group Cluster similar Analysis

to understand helps understand

α

people -\>summanze Understanding

◦ Group related documents for

Discovered Clusters 1

Applied-Matl-DOWN,Bay-Network-Down,3-COM-DOWN, Cabletron-Sys-DOWN,CISCO-DOWN,HP-DOWN, DSC-Comm-DOWN,INTEL-DOWN,LSI-Logic-DOWN, Micron-Tech-DOWN,Texas-Inst-Down,Tellabs-Inc-Down,

Industry Group

Technology1-DOWN browsing, group genes and proteins that have similar functionality, or group stocks

Natl-Semiconduct-DOWN,Oracl-DOWN,SGI-DOWN, Sun-DOWN 2

Apple-Comp-DOWN,Autodesk-DOWN,DEC-DOWN, ADV-Micro-Device-DOWN,Andrew-Corp-DOWN, Computer-Assoc-DOWN,Circuit-City-DOWN, Compaq-DOWN, EMC-Corp-DOWN, Gen-Inst-DOWN, Motorola-DOWN,Microsoft-DOWN,Scientific-Atl-DOWN with similar price fluctuations

Summarization

\-> to get toHe◦ Reduce the size of large data sets

Poist instead

f one by one

4 Technology2-DOWN

3

Fannie-Mae-DOWN,Fed-Home-Loan-DOWN, MBNA-Corp-DOWN,Morgan-Stanley-DOWN Financial-DOWN 4

Baker-Hughes-UP,Dresser-Inds-UP,Halliburton-HLD-UP, Louisiana-Land-UP,Phillips-Petro-UP,Unocal-UP,

Schlumberger-UP Oil-UP

Clustering precipitation in Australia

What is NOT Clustering?

Simple segmentation

◦ Dividing by last name

students into or different By 5 registration groups alphabetically, Gender

Results ◦ Groupings of a query

are a result of an ←external specification

like age group ◦ Clustering is a grouping of objects based on the data ↳Similarity in all Supervised classification

tme features

◦ Have class label information

Notion of a Cluster can be Ambiguous

How many clusters?

↓ Ʃ

Six Clusters

Two Clusters

Four Clusters So how do we decide ?

\-> it can be a parameter You

↳ and tone go witdestegthaance

6

Types of Clusterings

A clustering is a set of clusters

Important distinction between partitional and hierarchical sets of clusters

Partitional Clustering

◦ A division of data objects into non-overlapping subsets (clusters) such that each data object is in exactly one subset

Hierarchical clustering

◦ A set of nested clusters organized as a hierarchical tree

7

Partitional Clustering

② ①

① Original Points A Partitional Clustering

8

Hierarchical Clustering

↳ you get of clusters You wantShows p1

nee- One nesting cluster p3

p4

p2

\->p1 ℃

p2 duste

↳ duster , p3 -cosest

p4 each past

\_aone

Traditional Hierarchical Clustering Traditional Dendrogram

9

Clustering Algorithms

• K-means clustering

• Hierarchical clustering

• Density-based clustering-\>similartoKnused -\> Distance based ,

but done

hierarchal

approach

↳ clusters are

dense region

10

K-means Clustering

• Partitional clustering approach

• Number of clusters, K, must be specified

• Each cluster is associated with a centroid (center point)

• Each point is assigned to the cluster with the closest centroid

• The basic algorithm is very simple

can be

a drawback ,

but you get to -try more You specify then in & σ choose

best perf.

·

11

Example of K-means Clustering

1 assume

iK = 3 Iteration 6 randomly -\>you chose

3

Points as re initial Centers

Iteration Iteration Iteration Iteration Iteration 1 2 3 4 5 3 3 3 3 3 3

2.52.52.52.52.52.52) So points we o assign centroid the closest the its too 2 2 2 2 2 2

3for each cluster

recompute the 1.51.51.51.51.51.5center, , average point =\>so acc in middle

1 1 1 1 1 1

어 cluster

λ

\->red centroid cdoses to it

Repeat 0.50.50.50.50.50.5=\> Step

centroids When the

0 0 0 0 0 0

don't change,

so with in assignment

Changes

\-2 -2 -2 -2 -2 -2 -1.5 -1.5 -1.5 -1.5 -1.5 -1.5 -1 -1 -1 -1 -1 -1 -0.5 -0.5 -0.5 -0.5 -0.5 -0.5 0 0 0 0 0 0 0.5 0.5 0.5 0.5 0.5 0.5 1 1 1 1 1 1 1.5 1.5 1.5 1.5 1.5 1.5 2 2 2 2 2 2 x x x x x x

12

Example of K-means Clustering

Iteration 1

Iteration 2

Iteration 3 3

2.5-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2 x

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

3

2.5x

3

2.52

2

2

1.51.51.5y

y

1

1

1

0.50.50.50

0

0

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

x

Iteration 4

Iteration 5

Iteration 6 3

3

3

2.52.52.52

2

2

1.51.51.5y

y

1

1

1

0.50.50.50

0

0

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2 x

x

x

13

K-means Clustering- Details Eudedian distance

(X 1, Yz) , (X2 ,Yn)

\-×=) + ( y-

(Y , Y, z ,) , ▪ Simple iterative algorithm

▪ Initial centroids are often chosen randomly.

(X\>, yz, zz)

▪ Clusters produced vary from one run to another.

'tsy. - y .,r

▪ The centroid is (typically) the mean of the points in the cluster, but other definitions are possible (see Table 7.2).

▪ ‘Closeness’ is measured by Euclidean distance, cosine similarity, correlation, etc.

▪ K-means will converge for common proximity measures with appropriately defined centroid (see Table 7.2).

▪ Most of the convergence happens in the first few iterations.

▪ Often the stopping condition is changed to ‘Until relatively few points change clusters’

▪ Complexity is O( n \* K \* I \* d )

▪ n = number of points, K = number of clusters, I = number of iterations, d = number of attributes

iy + (7 \# -\>o ate matters withg

\-> the time

complexity, running How long takes time

it

für

alg ∞

· -time complexity \* 3 centroids , 100 points ↳ 300 distances to call . a centroids -\> depends on \# of Points, \# 400 of distances Clusters,s it , to call \# of =\> tr

the centroidsmore

, the converge

more we 14

calculate

K-means Objective Function

A common objective function (used with Euclidean distance measure) is Sum of Squared Error (SSE)

◦ For each point, the error is the distance to the nearest cluster center

◦ To get SSE, we square these errors and sum them.

\=

∑∑ = ∈ ◦ x is a data cluster Ci

← KSum SSE xmdist 2 ),( -\>Distane all these sums togehe i =\> for each point closinghavein cluster 1 Cx mean Ci and mi is the 김 ata centroid (mean) for

◦ SSE improves in each iteration of K-means until it reaches a local or global minima.

between X 후 point se \]

\-> Distance each and 어 betreen

point

Center i

The cluster

i

De ; in lus a a mis point

belongs to men뿌quare men we Sum

me square Ex ne상g

distances beteen each point 회 we ofthemean cuse Belongs to

15

Example of K-means Clustering

Iteration 6 uestion:

Is it better

to have a SSD3 small SSE or Big SSE

Better to have small

SSE

) calc between distance Point =\> points becloseand should

each

E, te Center mesto centroid ensore represents bre =Bo 2) 3) square findsum

the dfs

Cluster well

SSD2

\-2 ↳SSrsud -1.5 £ -1 -0.5 θ

0 0.5 1 1.5 2 Iteration Iteration Iteration Iteration Iteration 1 2 3 4 5 3 3 3 3 3 3

2.52.52.52.52.52.52 2 2 2 2 2

1.51.51.51.51.51.51 1 1 1 1 1

0.50.50.50.50.50.50 0 0 0 0 0

\-2 -2 -2 -2 -2 -1.5 -1.5 -1.5 -1.5 -1.5 -1 -1 -1 -1 -1 -0.5 -0.5 -0.5 -0.5 -0.5 0 0 0 0 0 x x x x x x

0.5 0.5 0.5 0.5 0.5 SSE

1 1 1 1 1 1.5 1.5 1.5 1.5 1.5 2 2 2 2 2

12

Two different K-means Clusterings

3

2.52

Original Points

1.51

↳Shape ground is

poin

0.50

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

x

3

3

2.52.52 2

1.51.5y

1

0.50

ㅇ -\> not shoudsquare, be green

y

1

0.50

π =\> SSE large -2 -1.5 -1 -0.5 0 0.5 1 1.5 2

Optimal x

Clustering

↳ Better Since points

\-2 -1.5 -1 -0.5 exce x

0 0.5 가 Centroid

1 1.5 2 here Sub-optimal Clustering here are

o closeCentroid 16

Importance of Choosing Initial Centroids

Iteration Iteration Iteration Iteration Iteration Iteration 1 2 3 4 5 6 3 3 3 3 3 3

2.52.52.52.52.52.52 2 2 2 2 2

1.51.51.51.51.51.51 1 1 1 1 1

0.50.50.50.50.50.50 0 0 0 0 0

\-2 -2 -2 -2 -2 -2 -1.5 -1.5 -1.5 -1.5 -1.5 -1.5 -1 -1 -1 -1 -1 -1 -0.5 -0.5 -0.5 -0.5 -0.5 -0.5 0 0 0 0 0 0 0.5 0.5 0.5 0.5 0.5 0.5 1 1 1 1 1 1 1.5 1.5 1.5 1.5 1.5 1.5 2 2 2 2 2 2 x x x x x x

17

Importance of Choosing Initial Centroids

Iteration 1

Iteration 2

Iteration 3 3

2.5-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2 x

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

3

2.5x

3

2.52

2

2

1.51.51.5y

y

1

1

1

0.50.50.50

0

0

x

Iteration 4

Iteration 5

Iteration 6 3

2.5-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2 x

3

2.5x

3

2.52

2

2

1.51.51.5y

y

1

1

1

0.50.50.50

0

0

x

18

Importance of Choosing Initial Centroids …

Iteration Iteration Iteration Iteration Iteration 1 2 3 4 5 3 3 3 3 3

2.52.52.52.52.52 2 2 2 2

1.51.51.51.51.51 1 1 1 1

0.50.50.50.50.50 0 0 0 0

\-2 -2 -2 -2 -2 -1.5 -1.5 -1.5 -1.5 -1.5 -1 -1 -1 -1 -1 -0.5 -0.5 -0.5 -0.5 -0.5 0 0 0 0 0 0.5 0.5 0.5 0.5 0.5 1 1 1 1 1 1.5 1.5 1.5 1.5 1.5 2 2 2 2 2 x x x x x

19

\=\> Importance of Choosing Initial Centroids …

cause random final the

resteared Iteration 1

Iteration 2 3

2.5-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2 x

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

3

2.52 2

1.51.5y

y

1

1

0.50.50 0

x

Iteration 3

Iteration 4

Iteration 5 3

2.5-2 -1.5 -1 -0.5 0 0.5 1 1.5 2

\-2 -1.5 -1 -0.5 0 0.5 1 1.5 2 x

3

2.5x

3

2.52

2

2

1.51.51.5y

y

y

1

1

1

0.50.50.50

0

0

x

20

f 10 Clusters Example

444422220000-2-2-2-2-4-4-4-4Starting with two initial centroids in one cluster of each pair of clusters

21

10 Clusters Example

Starting with two initial centroids in one cluster of each pair of clusters

Iteration 1

Iteration 2 8

6420-2-4-60 5 10 15 20

0 5 10 15 20 x

0 5 10 15 20

8

642y y 0-2-4-6Iteration 3

Iteration x

4 8

6420-2-4-60 5 10 15 20

x

8

642y y 0-2-4-6x

22

\= 10 Clusters Example

positions daff

Starting with some pairs of clusters having three initial centroids, while other have only one.

S cento ,ds 4444

② ② ② ② ③

22220000-2-2-2-2-4-4-4-4=\> firstStep final result

affects

SM

23

10 Clusters Example

Starting with some pairs of clusters having three initial centroids, while other have only one.

Iteration 1

Iteration 2 8

6420-2-4-60 5 10 15 20

0 5 10 15 20 x

0 5 10 15 20

8

642y y 0-2-4-6Iteration 3

Iteration x

4 8

6420-2-4-60 5 10 15 20

x

8

642y y 0-2-4-6x

24

Solutions to Initial Centroids Problem

\-> Multiple runs

◦ Helps, but probability hy with CSO multiple diff rAs

initials)

is not on your side

\=\> select

result Use select ◦ In SKLearn, some among strategy KMeans these to algorithm initial select centroids

the has k this initial option centroids Glowest (n\_init)

↳ How and many with Se times then You waving

Centrois repeat ind with ←

◦ ◦ Select ◦ Use K-means++ hierarchical most is widely a robust clustering separated

way of doing to determine this selection

initial -Only centroids

goodest -\> kmears

then

Ste

Similar Bisecting to idea K-means

oC ++ -\> keep dividing ◦ acquire K clusters, split the set of some points into points two clusters, choose one of these clusters to split, etc., until K clusters have been produced.

◦ Not as susceptible to initialization issues

set until of you reach clusters

A of

you want

25

its K-means++ \# choose where

\-> choose the to min centroid one

distance 1) Assume that Biggerwith eenrad you you have a dataset want to cluster into To select a set of initial centroids, 후

3 clusters ↳ C, first → perform randomly K =3 cluster , you select the the other following

two Centroid s sophisticated done way

1\. Select an initial point at random to be the first centroid 2. For k – 1 steps

\->remaining two

3\. For each of the N distance to the currently points, selected xi, i.e.,min d2( Cj, xi )

\=\> we haveononeeed chosen distance , to that point

\#Point of ↳ point min now distance we for cak each

squared the

' k++

1 ≤ i ≤ N, find the minimum squared centroids, C1, …, Cj, 1 ≤ j \< k, 4. Randomly select a proportional to ∑ new d2( centroid Cj, xi )

d2( Cj, xi )

by choosing a point with probability

5\. End For

For each data point compute its distance from the nearest, previously chosen centroid.

Select the next centroid from the data points such that the probability of choosing a point as centroid is directly proportional to its distance from the nearest, previously chosen centroid. (i.e. the point having maximum distance from the nearest centroid is most

10 selecway detect =\> 1

Spoinis diff to likely to be selected next as a centroid)

custers to centroid =\> Point with be squared selected ↑ next the

Distance will as centroid

\=\> maximum \>me-distance dosest 26

Jenecentroid si

\* pro ProbDistancel-s)

sincee neroid a randomly selected as

first \_ ㆁ Centroid For each we calc ー we o·ดDX - 4 - Jum a :ตอน

3\. Point ⑥ มี

The dist. to me dosest centroid \!

squared

calc squared The to CI \*need repeat C3 process → ㆁ α C3

\_ Sum -\> togethersquare each we wom distance add . all distance by mem & thesered

Divide surm

をX :

m3dist 어

squared withthe Aprobis Better

one

K-means++

This approach can be slower than random initialization, but very consistently produces better results in terms of SSE

• The k-means++ algorithm guarantees an approximation ratio O(log k) in expectation, where k is the number of centers By following the K-means++ for initialization: - we pick up centroids that are far away from one

another. - This increases the chances of initially picking up

centroids that lie in different clusters.

27

K-means++ Example

1)2)Choose Calc 3) 4) Now each Then the again mepointpoint find to distance the , Centroids to for that =\>centroid the distance mat & that each that the centroid centroid maximum new between centroid =\>matis& is has point hasea closest to tat know the

centroid

both min sind

point

which

distance distance thea

to

cdoso Bot mis쏠

paene poinsarrestraon

.re . ℃ 3 →-\>oc alsum I doset

28

K-means++ Example

I 2etewisosom -ㅋ →웩\* next -Xo Centroid

3

28

K-means++ Example

final centroid,

28

Bisecting K-means

Bisecting K-means algorithm

◦ Variant of K-means that can produce a partitional or a hierarchical clustering

//start with 1 cluster containing all points

//start with the cluster that has the highest SSE

↳ we have only so we

select it -\> Dividete into twoClustermeans, 1)initial trow centroids

t

K = 2 -add them of to clusters list 2)Divide this

cluster in

two Clustr

1)select anomer cluster from with the list

ISSE CLUTO: http://glaros.dtc.umn.edu/gkhome/cluto/cluto/overview

2)Divide into two duster

3\) add to list\> repect

29

Bisecting K-means Example

30

Bisecting K-means Example

30

Bisecting K-means Example

ΔΔ

77

30

00

P

50:49

Bisecting K-means Example

30

01:06:44

P

40 1.5x

Bisecting K-means Example

I

H

30

▷ P

52:03

Bisecting K-means Example

\~

Ь

30

01:06:44

P

40

1.5x

\<\<

00

P

51:57

Bisecting K-means Example

\~

Ь

30

01:06:44

P

độ 1.5

COK

\>\>

▷ P

52:07

Bisecting K-means Example

Ь

30

01:06:44

P

40

1.5x

\<\<

Di §problem of Olves

initial Bisecting

KC-means centroid between 12-means - - 1) 2 throw apply 1) Start men random k-means

with repeat 1, 10 throw till centroids

2 You centroids

reachoCentroids

Bisecting K-means Example

30

K-means Example ④7123 = 53③C1- Consider the following one-dimensional dataset with one feature x: {7, 10, 20, 28, 35}

Consider the absolute difference as the distance measure ð·(ð,ð) = |ð¥ − ð¥ |

Assume K = 2, and initial centroids were 10 and 35

\> 12 . 3 10123 =23 22 - 31

. 5 20

\-12 . 28-12 . 3 = コー 7 3 = IS .7 39

\-12 . 3 = 22

.7

화장, 2 급2②

① 7.31 . 10 -31

20- 28

\- S = zu . S

31

31

. = . S S“ 리유35 - 31

\- s

\-s

s

ミ = 3 S ⑤7, 10, 20 e C -\>manhattan distance 28 , 35 -22 ① · ⑥ -Converge,

· O ①

Stop

커 =3 7

\- 3S = 28

( O

\-10 = 0 10

\- 3 s = 2s

20 28

t0 -10 =10 = 18 20 -3s = 1 S

28 - 3s = ヲ

35

\- 10 = 25 35

\-3S = 0

31

K-means Example

Step 1: Compute distances from samples to centroids

10 35

Sample (x)

Distance to Centroid 1

Distance to Centroid 2 7 3 28 10 0 25 20 10 15 28 18 7 35 15 0

↑

32

K-means Example

Step 2: Assign samples to closest centroids

10 35

Sample (x)

Distance to Centroid 1

Distance to Centroid 2

Assigned to centroid 1

7 3 10 0 28 25 20 10 15 Assigned to centroid 2

28 18 35 15 7 0

33

K-means Example

Step 3: Re-compute centroids of each clusterCentroid1 = Average (7, 10, 20) = 12.3

Centroid2 = Average (28, 35) = 31.5

Repeat Steps 1 & 2: Compute distances to centroids and assign to closest centroid 12.3 31.5

Sample (x)

Assigned to centroid 1

Assigned to centroid 2

Distance to Centroid 1

Distance to Centroid 2 7 5.3 24.5 10 2.3 21.5 20 7.7 11.5 28 15.7 3.5 35 22.7 3.5

34

K-means Example

Stop since there is no assignment difference so centroids won’t change → algorithm converged.

12.3 31.5

Assigned to centroid 1

Assigned to centroid 2

Distance to Centroid 1 Sample

Distance to (x)

Centroid 2 7 5.3 24.5 10 2.3 21.5 20 7.7 11.5 28 15.7 3.5 35 22.7 3.5

35

Limitations of K-means

K-means has problems when clusters are of different

← σ

G◦Sizes

◦Densities

◦Non-globular shapes -\> not arcular K-means or when it has is not problems scaled. when Solution:

the data \* contains outliers, o Remove ^

outliers before clustering o Scale the data

36

Limitations of K-means

Different Sizes

r cause K-means distance -so take doesn't intoe based

consideration spaces shapesna L -not goot it everywhere went ↑Poste

in datthe

a

Original Points K-means (3 Clusters)

37

Limitations of K-means

Different Density

a =\> nor clusters good ④

⑮

based

doseness

Original Points K-means (3 Clusters)

38

Limitations of K-means

Non-globular Shapes

Original Points

\=\>vey baddata =\>Sn shapes ㆁ12 - mวตกง ㆁ

K-means (2 Clusters)

39

Overcoming K-means Limitations I can 2) & choose another \# of clusters \&as alg post-processing combinetogethe

\=\> merge clusters cosest Centroid with

togetver ∞

Original Points K-means Clusters

One solution is to find a large number of clusters such that each of them represents a part of a natural cluster. But these small clusters need to be put together in a youdo post-processing step.

it , diff code for it

40

Overcoming K-means Limitations

Original Points K-means Clusters

One solution is to find a large number of clusters such that each of them represents a part of a natural cluster. But these small clusters need to be put together in a post- processing step.

41

Overcoming K-means Limitations

Original Points K-means Clusters

One solution is to find a large number of clusters such that each of them represents a part of a natural cluster. But these small clusters need to be put together in a post- processing step.

42

Pre-processing and Post-processing

Pre-processing

◦ Scale/Normalize the data

\->need to since based

distance

◦ ◦ Eliminate Fill missing outliers

values or -\> eliminate woulddevia records ee with get rid missing o will feature

affect of quale dustering

a

values

↳like kNN

Post-processing

◦ Eliminate small clusters that may represent outliers

◦ Split ‘loose’ clusters, i.e., clusters with relatively high SSE

really

far zom each awcy

Other

◦ Merge clusters that are ‘close’ and that have relatively low SSE

43

Learning Outcomes

1\. Perform machine learning steps including data preparation, task identification, model selection, and evaluation.

2\. Employ mathematical methods to explain the theoretical aspect of machine learning and data mining techniques.

3\. Select appropriate supervised learning methods including classification and regression for given problems and datasets. 4. Use unsupervised learning methods such as clustering and association rule mining to discover patterns and relationships in datasets. 5. Apply feature selection and dimensionality reduction methods.

6\. Use state-of-the-art software to explore and solve practical machine learnin
