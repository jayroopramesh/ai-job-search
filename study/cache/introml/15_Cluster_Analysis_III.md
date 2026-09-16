# IntroML (CMP 466) — 15 Cluster Analysis III
> Source: Google Drive file 110dHgTH_DNOJbvgV5XZLO6xBpQ3uz329 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466- Machine Learning and Data Mining

Chapter 7- Cluster Analysis: Basic Concepts and Algorithms III

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

• Clustering concept

• Clustering methods

• Clustering in SKLearn\!

2

Density-based Clustering

Basic idea

◦ Clusters are dense regions in the data space separated by regions of lower density.

◦ A cluster is defined as a maximal set of density connected points.

◦ Density-based clustering are able to discover clusters of arbitrary shape Methods

DBSCAN: Density-Based Spatial Clustering of Applications with Noise

3

DBSCAN Clustering

DBSCAN is a density-based algorithm.

• Density: number of points within a specified radius Eps (ε).

• High Density: ε -Neighborhood of an object contains at least MinPts of objects.

Density-

\> number

I molecules are closer each Pact , Can't Other-more

really to

compress

circle centered

\_

\_ by a point , with radius Ʃ

\*we set a treshold o determine , d circle where

P is the Min Pts, densits noase e ⑥ ⑧ ·-Dense · d is circle the E wherecenter is a 후 radiug center of mut E the (Eps) circled radius is

⇌ G Phigh - 니 비 q w

→ 3

4

DBSCAN Clustering

◦ A point is a core point if it has at least a specified number of points (MinPts) within Eps

◦ These are points that are at the interior of a cluster

◦ Counts the point itself

◦ A border point is not a core point, but is in the neighborhood of a core point

◦ A noise point or outlier is any point that is not a core point nor a border point

\=\> core point that is a its point

has the E-neighborhood min \# of points ↳ Able to identify noise points , Unlike K-means Or more -\>Denge

region

\=\> P = with minpt its here =4 neighborhood are pos

① within its neighborhood less Butinof me coreneighborhood

4 -point pis \[3)

( P)

↳ ↳isolated b

in Not there its in neighborhood is \# the of small \< Threshold neighborhood points Ofnot

inneighborhoodกอ int

enough pointe

.

⑧ O ⑥ 0 ⑥ EBorder = (Burendcore

vel

ㆁ of a core ·

point

MinPts = 5

5

DBSCAN Clustering mists = 10 \* All circles have 0 : If we make if we decrease, A

sEps same - same size mindt = 10 is it easier harder to

a core or be point : Harder easier

nore only= poit 7 not points Q : If we makes = if we increase ,MinPts = 7 easier easy Eps it Smallerbeharde , easier will to orbecome

core harder

Poit ? 后 become core point ㅇ

ㆁ ㆁ· ㆁㆁ ㆁ ↳outlier Border d a \< 7 d core point

카드카

6

DBSCAN: Core, Border and Noise Points

soutlier

↓ Border, close to core dore -\> within their its Original Points Kreshold & Point types: core,

area dense, border and noise

many neighbors

ε = 10, MinPts = 4

7

DBSCAN Algorithm

Form clusters using core points, and assign border points to one of its neighboring clusters

1: Label all points as core, border, or noise points.

2: Eliminate noise points.

3: Put an edge between all core points within a distance Eps of each other.

4: Make each group of connected core points into a separate cluster.

5: Assign each border point to one of the clusters of its associated core points

borde ? not cove ? - =\> Done in a loop

↳ unlabelled

\=\> so core points within the same neighborhood 어each =\> connected are some cluster ,da strer

connect

Tem

8

When DBSCAN Works Well

\&noise

cerdusters closea

Original Points

isoordeClusters

chol - Course Edust "

• Can handle clusters of different shapes and sizes

• Resistant to Noise

9

When DBSCAN DOES NOT Work Well

• Cannot handle varying densities

• Very sensitive to parameters especially in high-dimensional data

↳ Works

weh =\> Density of eaon Shapes, structure,

Cluster not is the same =\>varying , sizes bot

densities

no5

② ㉙ good

ー℃-\>6

① ③ ^ hyper--// Parameters Original Points

How select try to

tem ? multiple go with result best

\[)

\->outliers →lo loof

datclusters noise a of t ↳ small change affects

a lot esp with ↑ deminsional data

(MinPts = 4, ε =9.75) → results in 3 different clusters, rest of points were identified as noise.

(MinPts=4, ε =9.92) → results in 3 clusters.

10

DBSCAN: Determining Parameters

• Idea is that for points in a cluster, their kth nearest neighbors are at roughly the same distance

• Noise points have the kth nearest neighbor at farther distance

• So, plot sorted distance of every point to its kth nearest neighbor

1\) we set min pts to att

and the adjust we E try to 2)The we try with a

digg min pts

\~O • set ε based on this

\=\>what 엉 within there is 2 the that mat are size E 4 pts Set \* So Mirpls Eps if we

\=

\=

So The highlighted Points wit pin

0

Core points Minptsadaist-O = 4 \[ S £ -\> will in ime neighborhood

for sure

core poinls poink

osou

theea ,be Border

& \~ neighbor isoimin a dists

can

oultiers

11

DBSCAN: Determining Parameters

• Idea is that for points in a cluster, their kth nearest neighbors are at roughly the same distance

• Noise points have the kth nearest neighbor at farther distance

• So, plot sorted distance of every point to its kth nearest neighbor

• set ε based on this

noise I s Consideredborder we E point= consider

10 a points , , bwim tre Neighbarhood ofcorepoinis beCove menpts =e

000o \# all thepointt,eo nearest neighbor

, below its Gmu

is ↳around Points 2so will be core with in distance a

alo cM 11 So 10cm points4th farthest them all Neighbor, -\> these

is core meir within from

PtS

,

Cluster Validity

For supervised classification we have a variety of measures to evaluate how good our model is

◦ Accuracy, precision, recall, f-measure

For cluster analysis, the analogous question is how to evaluate the “goodness” of the resulting clusters?

But “clusters are in the eye of the beholder”\!

◦ In practice the clusters we find are defined by the clustering algorithm

Then why do we want to evaluate them?

◦ To avoid finding patterns in noise

◦ To compare clustering algorithms

◦ To compare two sets of clusters

◦ To compare two clusters

\-> how to evaluate

clustering = not like classification,

but if have

Youround truth & with is same he

way blike 18 you have labels you measure classification

like

12

Clusters found in Random Data

1

0.90 0 0.2 0.4 0.6 0.8 1 x

1

0.90.8 0.8

0.7

0.7 Random

0.6

0.6

DBSCAN Points

0.5

y

0.5

0.4

0.4

0.3

0.3

0.2

0.2

0.1

0.1

0

0 0.2 0.4 0.6 0.8 1 x

1

1

0.90.9K-means

0.8

0.8

Complete 0.7

0.7

Link

0.6

0.6

0.5

y

0.5

0.4

0.4

0.3

0.3

0.2

0.2

0.1

0.1

0

0 0.2 0.4 0.6 0.8 1 0

0 0.2 0.4 0.6 0.8 1 x

x

13

Measures of Cluster Validity

Numerical measures that are applied to judge various aspects of cluster validity, are classified into the following two types.

◦ Supervised: Used to measure the extent to which cluster labels match externally supplied class labels.

◦ Entropy

◦ Often called external indices because they use information external to the data

◦ Unsupervised: Used to measure the goodness of a clustering structure without respect to external information.

◦ Sum of Squared Error (SSE)

◦ Often called internal indices because they only use information in the data You clusters can use or clusterings

supervised or unsupervised measures to compare =\> measure distance between point & the aug Centroidof cluster,

,

The smaller SSE

better

14

Unsupervised Measures: Cohesion and Separation

\=\>Dist2(X,m ,) Can be Eucedian, manhattan =\> Distance of me squared between dit x & M Distance measure any point Cluster and C1 the , & Internal measure/Index: Used to measure the goodness of a clustering structure without respect to external information. o Useful when the ground truth labels are unknown. Cluster Cohesion/compactness: Measures how closely related are objects in a cluster. Example: SSE Cluster Separation/isolation: Measure how distinct or well-separated a cluster is from other clusters. Example: Squared Error

◦ Cohesion is measured by the within cluster Sum of Squares (SSE)

between ððð¸ =

ð¥ − ð

∈

◦ Separation is measured in the

by the cluster Sum of Squares Between clusters

Assume aSquare centroid Medissfor adding C7 tatof ae , ðððµ = ð¶ ð − ð

\=\> (Cildis +

Global mean, s aug of m all points in dataset eacn Do it clostefor .

Where ð is the centroid of cluster ð, ð is the global mean (avg of all points in the dataset), ð¶ is the size of cluster ð

2 (M ,Mi)=\> find Mi distance = Centroid aug squared or of centroid each between clusterof cluster i

md allClustea them . . We multiply by those

size

C (m

\- M =)

2

\+ G2 (M

\- m2)2 ...

cluster each 어i.

15

Unsupervised Measures: Cohesion and Separation

Two scenarios: K=1 cluster:

( 1 - 3)\~ ← (2

\- 3)\~

× ( 4

\- 332

\+(S - 3)2m

∅ ×1 2 3 4 5 1t = 3 ððð¸ = 1 − 3 + 2 − 3 + 4 − 3 + 5 − 3 = 10

ðððµ = 4 × 3 − 3 = 0

SSB = 4 (3

\_3) = 0 ððð¡ðð = 10 + 0 = 10

กอ separation

φ2 = G ' S

\-> Better K=2 clusters:

ððð¸ = 1 − 1.5 + 2 − 1.5 + 4 − 4.5 + 5 − 4.5 = 1 些= 1 s ðððµ = 2 × 3 − 1.5 + 2 × 4.5 − 3 = 9

S8E SSB = ( + I SSE -Is)\~+ = constant

ððð¡ðð ( 2 m × × × 1 m1 2 3 4 m2

5 A \<IO

\= 1 + 9 = 10 - 1 s)2

t ( 4 - a . s)

R

\+ LS

\- u

. s)㎡= =\> since

5(= 2(3

\- 1 . 5)"+ 0. S + o

. 5 =1 2(u . S

\- 3)2

\= 9

Totcl =10 =) Better separation -

POinHS closer centroid are

아 here

16

Unsupervised Measures: Cohesion and Separation

Two scenarios:

SSE- it each point SSE

\= 0

SSB + SSE = constant

s

considered Guster · O ㆁ ㆁ SSB = 1 C (3 -( K=1 cluster:

m ×1 2 3 4 5 ððð¸ = 1 − 3 + 2 − 3 + 4 − 3 + 5 − 3 = 10

ðððµ = 4 × 3 − 3 = 0

1)2 +(3

\- 2)2 + ððð¡ðð = 10 + 0 = 10

m

3

\- 4 )

K=2 clusters:

ððð¸ = 1 − 1.5 + 2 − 1.5 + 4 − 4.5 + 5 − 4.5 = 1 ðððµ = 2 × 3 − 1.5 + 2 × 4.5 − 3 = 9 ððð¡ðð = 1 + 9 = 10

2 + (3- s)≈10 × × × = 1 m1 2 3 4 m2

5

16

Determining the Correct Number of Clusters

SSE curve for a more complicated data set

1 2

3

5

6

4

SSE aßest

cet

ss=ㅋ

7

\=\>you des { ·ks until good K

see stops here

SSE of clusters found using K-means

31

Unsupervised Measures: Cohesion and Separation

A proximity graph-based approach can also be used for cohesion and separation.

◦ Cluster cohesion is the sum of the weight of all links within a cluster.

◦ Cluster separation is the sum of the weights between nodes in the cluster and nodes outside the cluster.

cohesion separation

17

Measures of Cluster Validity

\- Silhouette coefficient combines ideas of both cohesion and separation, but for individual points, as well as clusters and clusterings

i

For an individual point, i

Distances used to calculate aCalculate a = average distance of i to the points in its cluster Calculate b = min (average distance of i to points in another cluster) The silhouette coefficient for a point is then given by

ð  = max(ð,ð)

ð − ð

Value can vary between -1 (incorrect clustering) and 1 (highly dense clustering), 0

means overlapping with no separation… Typically ranges between 0 and 1. The closer to 1 the better. - Can calculate the average silhouette coefficient for a cluster or a clustering - The score is higher when clusters are dense and well separated, which relates to a standard concept of a cluster.

Distances used to calculate b

18

Example

Assume you have the following clusters:

Cluster 1 ={{1,0},{1,1}} Cluster 2 ={{1,2},{2,3},{2,2},{1,2}}, Cluster 3 ={{3,1},{3,3},{2,1}}

Find silhouette coefficient for this clustering and interpret your results. Use Euclidian Distance.

19

Example

To calculate silhouette coefficient for each point in the dataset, you need to calculate a and b for each point.

point a b s (1,0) a=sqrt( (1-1)^2 +

(0-1)^2 ) = 1

We calculated only one distance, so it is the average.

\= min (avg distance to cluster2, avg distance to cluster3)

\= min ( \[(sqrt(1-1)^2 + (0-2)^2) + (sqrt(1-2)^2 + (0-3)^2) + (sqrt(1-2)^2 + (0-2)^2) +(sqrt(1-1)^2 + (0-2)^2) \]/4 ,\[(sqrt(1-3)^2 + (0-1)^2) + (sqrt(1-3)^2 + (0-3)^2) + (sqrt(1-2)^2 + (0-1)^2)\]/3 )//ends min = b1

s1= (b1 – 1)/ max(1,b1)

(1,1) a= 1 (1,2) (2,3)

20

Example

Take a point {1,0} in cluster 1 Calculate a, which is its average distance to all other points in it’s cluster, i.e. cluster 1

point a b s (1,0) √( (1-1)^2 + (0-1)^2)

\=√(0+1)=√1=1 Now for the point {1,0} in cluster 1, calculate b, which is its average distance from all the objects in cluster 2 and cluster 3. Of these take the minimum average distance.

So for cluster 2: {1,0} ----\> {1,2}, distance = √((1-1)^2 + (0-2)^2) =√(0+4)=√4=2 {1,0} ----\> {2,3}, distance = √((1-2)^2 + (0-3)^2) =√(1+9)=√10=3.16 {1,0} ----\> {2,2}, distance = √((1-2)^2 + (0-2)^2) =√(1+4)=√5=2.24 {1,0} ----\> {1,2}, distance = √((1-1)^2 + (0-2)^2) =√(0+4)=√4=2

Therefore, the average distance of point {1,0} in cluster 1 to all the points in cluster 2 = (2+3.16+2.24+2)/4 = 2.35

21

Example

Similarly, for cluster 3: {1,0} ----\> {3,1}, distance = √((1-3)^2 + (0-1)^2) =√(4+1)=√5=2.24 {1,0} ----\> {3,3}, distance = √((1-3)^2 + (0-3)^2) =√(4+9)=√13=3.61 {1,0} ----\> {2,1}, distance = √((1-2)^2 + (0-1)^2) =√(1+1)=√2=1.41

Therefore, the average distance of point {1,0} in cluster 1 to all the points in cluster 3 = (2.24+3.61+1.41)/3 = 2.42

Now, the minimum average distance of the point {1,0} in cluster 1 to the other clusters 2 and 3 is b = min (2.35 , 2.42) = 2.35.

So the silhouette coefficient of point 1 is: ð 1 = max(ð1,ð1) ð1 − ð1

\= 2.35 2.35 − 1

\= 0.574

point a b s (1,0) √( (1-1)^2 + (0-1)^2)

\=√(0+1)=√1=1

min (2.35 , 2.42) = 2.35 0.574

22

Example

In a similar fashion you need to calculate the silhouette coefficient for all points.

You can take the average silhouette coefficient for each cluster separately by averaging the silhouette coefficient of each of its points. Of these, the cluster with the greatest average silhouette coefficient is the best as per evaluation.

point a b s Average s per cluster (1,0) s1 average (s1, s2) (1,1) s2 (1,2) s3 average (s3, s4, s5, s6) (2,3) s4 (2,2) s5 (1,2) s6 (3,1) s7 average (s7, s8, s9) (3,3) s8 (2,1) s9

23

Measures of Cluster Validity via Correlation

Two matrices

Proximity Matrix Ideal Similarity Matrix

One row and one column for each data point An entry is 1 if the associated pair of points belong to the same cluster An entry is 0 if the associated pair of points belongs to different clusters Compute the correlation between the two matrices

Since the matrices are symmetric, only the correlation between

n(n-1) / 2 entries needs to be calculated. High magnitude of correlation indicates that points that belong to the same cluster are close to each other.

Correlation may be positive or negative depending on whether the similarity matrix is a similarity or dissimilarity matrix Not a good measure for some density or contiguity based clusters.

24

Measures of Cluster Validity via Correlation

Correlation of ideal similarity and proximity matrices for the K-means clusterings of the following well- clustered data set.

1

0.9100.8 200.7 300.6

s tnioP400.5 500.4 600.3 700.2 800.1 90

0

0 0.2 0.4 0.6 0.8 1 100

20 40 60 80 100 x

Corr = 0.9235

Points

1

0.9

0.8

0.7

0.6

0.5

0.4

0.3

0.2

Similarity00.1

25

Measures of Cluster Validity via Correlation

Correlation of ideal similarity and proximity matrices for the K-means clusterings of the following random data set.

1

0.90.8

0.7

0.6

y

0.5

0.4

0.3

0.2

0.1

0

0 0.2 0.4 0.6 0.8 1 x

Corr = 0.5810 K-means

102030405060708090

100

20 40 60 80 100

Points

1

0.9

0.8

0.7

0.6

0.5

0.4

0.3

0.2

Similarity00.1

26

Judging a Clustering Visually by its Similarity Matrix

Order the similarity matrix with respect to cluster labels and inspect visually.

1

0.90 0 0.2 0.4 0.6 0.8 1 x 100.8 200.7 300.6 40y 0.5 500.4 600.3 700.2 800.1 90

100

20 40 60 80 100

Points

1

0.9

0.8

0.7

0.6

0.5

0.4

0.3

0.2

Similarity00.1

27

Judging a Clustering Visually by its Similarity Matrix

Clusters in random data are not so crisp

1

0.90 0 0.2 0.4 0.6 0.8 1 x

1

102030405060708090

100

DBSCAN

0.9

0.8

0.8

0.7

0.7

0.6

0.6

0.5

0.5

0.4

0.4

0.3

0.3

0.2

0.2

0.1

0.1

0Similarity

20 40 60 80 100

Points

28

Judging a Clustering Visually by its Similarity Matrix

1 2

3

5

1 234 5 6 7

500 6

1000

4

1500

2000

2500

7

3000

DBSCAN

1 2 3 4 5 6 7

500 1000 1500 2000 2500 3000

29

1

0.9

0.8

0.7

0.6

0.5

0.4

0.3

0.2

00.1

Determining the Correct Number of Clusters

SSE is good for comparing two clusterings or two clusters SSE can also be used to estimate the number of clusters

6

10

4982760E SS5-243-42-615 10 15

02 5 10 15 K

20 25 30

30

Supervised Measures of Cluster Validity: Entropy and Purity

32

Assessing the Significance of Cluster Validity Measures

Need a framework to interpret any measure.

◦ For example, if our measure of evaluation has the value, 10, is that good, fair, or poor? Statistics provide a framework for cluster validity

◦ The more “atypical” a clustering result is, the more likely it represents valid structure in the data

◦ Compare the value of an index obtained from the given data with those resulting from random data.

◦ If the value of the index is unlikely, then the cluster results are valid

33

Statistical Framework for SSE

Example

◦ Compare SSE of three cohesive clusters against three clusters in random data

1

0.9450.8 400.7 350.6 300.5 250.4 200.3 150.2 100.1 50

0 0.2 0.4 0.6 0.8 1 x

0.016 00.018 0.02 0.022 0.024 0.026 0.028 0.03 0.032 0.034 SSE

SSE = 0.005

Histogram shows SSE of three clusters in 500 sets of random data points of size 100 distributed over the range 0.2 – 0.8 for x and y values

34

Statistical Framework for Correlation

Correlation of ideal similarity and proximity matrices for the K-means clusterings of the following two data sets.

1

0.90 0 0.2 0.4 0.6 0.8 1 x

1

0.90.8 0.8

0.7

0.7

0.6

0.6

y

0.5

0.5

0.4

0.4

0.3

0.3

0.2

0.2

0.1

0.1

0

0 0.2 0.4 0.6 0.8 1 x

Corr = -0.9235 Corr = -0.5810

Correlation is negative because it is calculated between a distance matrix and the ideal similarity matrix. Higher magnitude is better.

Histogram of correlation for 500 random data sets of size 100 with x and y values of points between 0.2 and 0.8.

35

Final Comment on Cluster Validity

“The validation of clustering structures is the most difficult and frustrating part of cluster analysis.

Without a strong effort in this direction, cluster analysis will remain a black art accessible only to those true believers who have experience and great courage.”

Algorithms for Clustering Data, Jain and Dubes

H. Xiong and Z. Li. Clustering Validation Measures. In C. C. Aggarwal and C. K. Reddy, editors, Data Clustering: Algorithms and Applications, pages 571–605. Chapman & Hall/CRC, 2013.

36

Measures of Cluster Validity

Evaluating the performance of a clustering algorithm is not as trivial as counting the number of errors or the precision and recall of a supervised classification algorithm.

https://scikit-learn.org/stable/modules/clustering.html\#clustering- performance-evaluation

External measure/Index: Used to measure the extent to which cluster labels match externally supplied class labels.

Internal measure/Index: Used to measure the goodness of a clustering structure without respect to external information.

37

Clustering in SKLearn\!

Clustering Algorithms: https://scikit-learn.org/stable/modules/clustering.html

38

Learning Outcomes

1\. Perform machine learning steps including data preparation, task identification, model selection, and evaluation.

2\. Employ mathematical methods to explain the theoretical aspect of machine learning and data mining techniques.

3\. Select appropriate supervised learning methods including classification and regression for given problems and datasets. 4. Use unsupervised learning methods such as clustering and association rule mining to 
