# IntroML (CMP 466) — 02 Data
> Source: Google Drive file 1tb6auiylHe6LH80KdCRHKh9Jwbj_Mf87 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP466- Machine Learning and Data Mining

Chapter 2: Data

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

• A$ributes and Objects

• Types of Data

• Data Quality

• Data Preprocessing (Aggrega\>on, Sampling, Discre\>za\>on and Binariza\>on, A$ribute Transforma\>on)

• To be discussed later:

• Similarity and Distance Measures

• Data Preprocessing (Dimensionality reduc\>on, feature selec\>on and scaling, ..)\* can have errons

How do we correct

it ? -\>more than

one way bot a

Problem

2

What is Data?

Collec\>on of data objects and their a+ributes

An a+ribute is a property or characteris\>c of an object

◦ Examples: eye color of a person, temperature, etc.

◦ A$ribute is also known as feature, variable, Peld, characteris\>c, or dimension

A collec\>on of a$ributes describe an object

◦ Object is also known as record, point, case, sample, en\>ty, or instance

\* people belong

to two classes

\-> -\>yes Binary or no

cassification seatores -ad

&ใ

Attributes

s tcejbOclass

Tid Refund Marital Status

Taxable Income Cheat

1 Yes Single 125K No

2 No Married 100K No

3 No Single 70K No

4 Yes Married 120K No

5 No Divorced 95K Yes

6 No Married 60K No

7 Yes Divorced 220K No

8 No Single 85K Yes

9 No Married 75K No

10 No Single 90K Yes

10

Attribute Values

A+ribute values are numbers or symbols assigned to an a$ribute for a par\>cular object

Dis\>nc\>on between a$ributes and a$ribute values ◦Same a$ribute can be mapped to diRerent a$ribute values

◦ Example: height can be measured in feet or meters

◦DiRerent a$ributes can be mapped to the same set of values

◦ Example: A$ribute values for ID and age are integers

◦ But proper\>es of a$ribute values can be diRerent

. neIs

201

4

Types of data

There are diRerent types of a$ributes

◦Numerical: represented as numbers. Further classiPed to discrete or con\>nuous.

◦Categorical: represented as classes or labels. Further classiPed to nominal (no order) or ordinal (order ma$ers).

◦Others: Unstructured data (text, audio, video, etc…)

↳ pictre -no clear data, pixels

5

Types of data

orde eno

\->has orde ↳Eye color lorder

matters)

d

GPA, IB

6

Types of data

Nominal: categorical data, order doesn’t ma$er

◦ Examples: gender, eye color, zip codes, marital status

"

ospenfiorder \*No priority

can

have

F or fn

\->adi,

its just dof types

7

Types of data

Ordinal: categorical data, order ma$ers

◦ Examples: star ra\>ng, rankings (e.g., taste of potato chips on a scale from 1-10), le$er grades (A to F), height {tall, medium, short}, pain level (scale from 1-10)

\->you can arder

the sample

based

On the feature

8

Types of data

っ%ㆁInterval Order Examples:

\-Eatdllantwo

↳ ↳ and when like scales: exact someone the whose is exact diRerences numeric taller a l6s diff cn seateaset Har between between the values are the values • Celsius temperature Iso in cre which the diRerence known -\> 1 . 65-1 . s are both -\>trat known.

\- well know Interval Temp- \> 20° 190 Today yesterdy between each -\> value if you is can the quantity From -\> interval 3 2-S

hours same. For example, the diRerence between 60 and 50 degrees is a -\>Interval measurable 10 degrees, as is the diRerence between 80 and 70 degrees.

• Time in which the increments are known, consistent, and measurable.

• Calendar dates

Interval scales are useful in sta\>s\>cal analysis. For example, central tendency\* can be measured by mode, median, or mean; standard devia\>on can also be calculated.

\* Central tendency: the tendency for the values of a random variable to cluster round its mean, mode, or median. Called also center of distribu\>on.

9

\* -\>interval

\+need its⇌Another of example

just sith -\> an thats Height interval,

above E not a Nation

average (my absolute reference

Point is not

zwo anote ref a true tero Point) ithas a meaning , Types of data Ra\>o: numeric

Ra\>o scales are the ul\>mate nirvana (ideal) when it comes to measurement scales because they tell us about the order, the exact value between units, AND have an absolute zero (clear dePni\>on of zero).

for height/weight O is a ref value Ra\>o variables can be meaningfully added, subtracted, mul\>plied, divided (ra\>os).

• Examples:

Height ⑮and weight

interval

Every but ratio every -\> interval interval

• Temperature in Kelvin not (for sures ratio . • Time

• Age

• Counts Ra\>o scales provide a wealth of possibili\>es when is a

Yost ·

theheezing point- \>itsis

reference

\-273

referentthe £ent

it comes me"absolute zuo" to sta\>s\>cal analysis (both descrip\>ve and inferen\>al sta\>s\>cs), e.g. Central tendency.

10

why this is imp to know \* Imp for encoding (category) \*What numeical Stuff yor

can apply

why knowing its not a ratio is imp

Anmed 1 Ali s cm above 10 Im above guy

any

\=\> I can't say Ali is twice ahmed cause my

rey point is notG

if aug 160

Ahmed -\>16S -\> Ho is not double

Ali -\> 170 las \* Same for temp in celius (yes in k mo

Difference Between Ratio and Interval

Is it physically meaningful to say that a temperature of 10 ° is twice that of 5° on

◦ the Celsius scale?

◦ the Fahrenheit scale?

◦ the Kelvin scale? Consider measuring the height above average

◦ If Bill’s height is three inches above average and Bob’s height is six inches above average, then would we say that Bob is twice as tall as Bill?

◦ Is this situaDon analogous to that of temperature?

11

Properties of Attribute Values

The type of an aGribute depends on which of the following four properDes/operaDons it possesses:

◦ DisDnctness: = 

◦ Order: \< \>

◦ DiOerences are meaningful: + -

◦ RaDos are meaningful: \* /

◦ Nominal aGribute: disDnctness

◦ Ordinal aGribute: disDnctness & order

◦ Interval aGribute: disDnctness, order & meaningful diOerences

◦ RaDo aGribute: all 4 properDes/operaDons

features o human :dNominal, order worde

\-> for interval an apply

but not \* / G ー

Eye called ↳ ↳Cant color- can distinctness \> only apply nominal compare addition/subtraction (no - Is order) two po which colormose people eye

have same Educationb

\- PHD, masters.

BachelorsHigh ↳ has orde School

,

eye Color

an

PHDX

↳ can apply +,

\-

, \*, Can 후 Someone edu can do cationdistincuess see has Masters al if a

Height ↳intervalo above average

cman,a weight statio ↳AB -\>Since lo0kyYanses interval

A x2B

\-> since ratio

12

Types of data: Summary

\* Everythingconverted

in \#'s to be used -\> But still Ordinal & nominal you want be able to apply stuff like

mean , diff.

cause wont make

sense

\->most frequent

\->value in middlecan't be sored

\*mcanbecurred - can't add

letters

13

Discrete and Continuous Attributes

Discrete A\*ribute

◦ Has only a Ynite or countable inYnite set of values

◦ Examples: zip codes, set of words in a collecDon of documents

◦ O\\en represented as integer variables.

◦ Note: binary aGributes are a special case of discrete aGributes

Con0nuous A\*ribute

◦ Has real numbers as aGribute values

◦ Examples: temperature, height, or weight.

◦ PracDcally, real values can only be measured and represented using a Ynite number of digits.

◦ ConDnuous aGributes are typically represented as \_oaDng-point variables.

14

More ID numbers: Complicated (Nominal, ordinal, Examples

\-> interval, Basedonor raDo)?

admissies

^ Can be nominal (if order doesn’t maGer), or ordinal (if order maGers like IDs at AUS)\!

\-> usually for used

distincness

Number of cylinders in an automobile engine (Nominal, ordinal, Can be ordinal interval, as order or raDo)?

maGers (smaller -\> \# cars of Cylinders have smaller \~ matters

number ordinal, of like we

use it cylinders).

fo

compare

cars  Depends on your purpose. What type of operaDon do you care about? order? AddiDon/subtracDon? Division (raDo)? ...

15

Key Messages for Attribute Types

The types of operaDons you choose should be “meaningful” for the type of data you have

◦ DisDnctness, order, meaningful intervals, and meaningful raDos are only four properDes of data

◦ The data type you see – o\\en numbers or strings – may not capture all the properDes or may suggest properDes that are not there.

◦ Analysis may depend on these other properDes of the data

◦Many staDsDcal analyses depend only on the distribuDon

◦ Many Dmes what is meaningful is measured by staDsDcal signiYcance.

◦ But in the end, what is meaningful is measured by the domain.

16

Types of data

Text: unstructured data

o Examples: email contents, sender/receiver Yeld in email, web chats, news arDcle, etc.

\-> not features the dataset , about

ves spuctvedsor andmcuored .

not

GabarE

a ,-\> -\>

\-> Fee basmesh Email, To stucture

appletes watered text Mcsed siäctue i inside it

deesnt nave a Ideal for like table Stuchte.. -\> post on linkedin ML

\_ \_ -\>Pic/videos

alsodarenbations

17

Types of datasets

Record (Tabular format)

◦ Data Matrix

◦ Document Data

◦ TransacDon Data

Graph

◦ World Wide Web

◦ Molecular Structures

Ordered

SequenDal Data GeneDc Sequence Data SpaDal Data Temporal Data

18

Record Data

Data that consists of a collecDon of records, each of which consists of a Yxed set of aGributes

Tid Refund Marital Status

Taxable Income Cheat

1 Yes Single 125K No

2 No Married 100K No

3 No Single 70K No

4 Yes Married 120K No

5 No Divorced 95K Yes

6 No Married 60K No

7 Yes Divorced 220K No

8 No Single 85K Yes

9 No Married 75K No

10 No Single 90K Yes

10

19

Data Matrix

If data objects have the same Yxed set of numeric aGributes, then the data objects can be thought of as points in a mulD-dimensional space, where each dimension represents a disDnct aGribute

Such data set can be represented by an m by n matrix, where there are m rows, one for each object, and n columns, one for each aGribute

Projection Projection

Projection Projection Distance Distance Load Load Thickness Thickness of of x x Load

Load

of of y y load load

10.23 10.23 5.27 5.27 15.22 15.22 2.7 2.7 1.2 1.2 12.65 12.65

6.25 6.25 16.22 16.22 2.2 2.2 1.1 1.1

20

Document Data

Each document becomes a ‘term’ vector

◦ Each term is a component (aGribute) of the vector

◦ The value of each component is the number of Dmes the corresponding term occurs in the document.

◦ Also called Bag-of-Word representa0on

Document 1

Document 2

Document 3

\* Need feature canServerMicrosรหั apply extractionwords like features → Team -\> appearedS O times in DOC 1 DO22 , DOC3 care abouaenh

words \#t 3 ofoccuaneneed 0 5 to mentionof

timearead in earl

0 2 6 0 2 0 2

00

7 0 2 1 0 0 3 0 0

1 0 0 1 2 2 0 3 0

21

Transaction Data

A special type of record data, where

◦ Each record (transacDon) involves a set of items.

◦ For example, consider a grocery store. The set of products purchased by a customer during one shopping trip consDtute a transacDon, while the individual products that were purchased are the items.

TID Items 1 Bread, Coke, Milk 2 Water, Bread 3 Water, Coke, Diaper, Milk 4 Water, Bread, Diaper, Milk 5 Coke, Diaper, Milk

22

Graph Data Examples: Generic graph, a molecule, and webpages

5

2

1 25

Benzene Molecule: C6H6

23

Ordered Data

Sequences of transacDons

Items/Events

An element of the sequence

24

Ordered Data

Genomic sequence data

GGTTCCGCCTTCAGCCCCGCGCC CGCAGGGCCCGCCCCGCGCCGTC GAGAAGGGCCCGCCTGGCGGGCG GGGGGAGGCGGGGCCGCCCGAGC CCAACCGAGTCCGACCAGGTGCC CCCTCTGCTCGGCCTAGACCTGA GCTCATTAGGCGGCAGCGGACAG GCCAAGTAGAACACGCGAAGCGC TGGGCTGCCTGCTGCGACCAGGG

25

Ordered Data

SpaDo-Temporal Data \_」 Dataset information diff duff has of locations points in at

hme

Average Monthly Temperature of land and ocean

26

Bad Data Quality

\-o data ↳ wrong decisions

EX: Banks , if you give

people stable

not loan income with

\-> Big Problem Poor data quality negaDvely aOects many data processing eOorts

“The most important point is that poor data quality is an unfolding disaster.

◦ Poor data quality costs the typical company at least ten percent (10%) of revenue; twenty percent (20%) is probably a better estimate.”

Thomas C. Redman, DM Review, August 2004

Data mining example: a classiYcaDon model for detecDng people who are loan risks is built using poor data

◦ Some credit-worthy candidates are denied loans

◦ More loans are given to individuals that default

27

Data Quality

\-> Datasmatare }-\>Biased putting or data

randomly resporteswrong , rest → Gor Either use remove it , or certain algorithms↳ Records

that are the same

Ex : he - when sensors oura Gifts "data impote the data , fillmemissingemain can tat workwiteng data wrong OR date eniry

OR

so many missing values -\>Drop one ofFan , What kinds of data quality problems? How can we detect problems with the data? What can we do about these problems?

Examples of data quality problems:

◦ Noise and outliers

◦ Wrong data

◦ Fake data

◦ Missing values

◦ Duplicate data

a keep the most recent/4 Quality one

28

Data Cleaning -\>Handeling

problems dataset

Data cleansing/cleaning:

• is the process of detecDng and correcDng (or removing) corrupt or inaccurate records from datasets.

• idenDfying incomplete, incorrect, inaccurate or irrelevant parts of the data and then replacing, modifying, or deleDng the dirty or coarse data.

29

Random Noise

↳ Domain dependant DIS unwanted for Signals single tren images tren tablar.....For objects, noise is an extraneous object

For aGributes, noise refers to modiYcaDon of original values

◦ Examples: distorDon of a person’s voice when talking on a poor phone and “snow” on television screen

◦ The Ygures below show two sine waves of the same magnitude and diOerent frequencies, the waves combined, and the two sine waves with random noise

◦ The magnitude and shape of the original signal is distorted

Pattern -\> Distoreddisappered

1

Two sine waves

3Observed signal (sum of the two sine waves)

3Observed signal with noise

by the Noise

0.80.6 220.4 11e dutingam-0.20.2 0

\-0.4

edutingam-10e dutingam-10-0.6 -2-2-0.8

\-1

0 0.1 0.2 0.3 0.4 0.5 -30 0.1 0.2 0.3 0.4 0.5 -30 0.1 0.2 0.3 0.4 0.5 time (seconds)

time (seconds)

time (seconds)

30

\*for each feature need to Outliers

\-> Either noise or interested Print info.

histogram

Outliers are data objects with characterisDcs that are considerably diOerent than most of the other data objects in the data set

◦ Case 1: Outliers are noise that interferes with data analysis

◦ Case 2: Outliers are the goal of our analysis

◦ Credit card fraud

◦ Intrusion detecDon

Causes? Recording error, data entry error, real values of interest\!

31

Missing Data

Reasons for missing values

◦ InformaDon is not collected -\> Decline to (e.g., people decline to give their age and weight)

report Certain

daten

Handling ◦ AGributes (e.g., annual missing may income not values

be is applicable not applicable to all to cases children)

\->Ifasd the a while Field

about a income

required

its

◦ Eliminate data objects or variables

◦ EsDmate missing values (imputaDon)

◦ Example: Dme series of temperature

◦ Example: census results

◦ Ignore the missing value during analysis

32

Missing Values Imputation SkLearn

import numpy as np \#Import the class from sklearn.impute import SimpleImputer \#Create the object imp = SimpleImputer (missing\_values = np.nan, strategy = 'mean') X = \[\[np.nan, 2\], \[6, np.nan\], \[7, 6\]\] X\_new = imp.fit\_transform(X) X\_new

Parameters: missing\_values: The placeholder for the missing values. All occurrences of missing\_values will be imputed. In Output array(\[\[6.5, pandas’ dataframes, missing\_values can be set to

2\. \],

either np.nan or pd.NA. default=np.nan

\[6. , 4. \],

Strategy: The imputation strategy. It can be “mean”, \[7. , 6. \]\])

“median”, “most\_frequent”, “constant” where missing values are replaced with a fill\_value., default=’mean’

33

Duplicate Data

Dataset may include data objects that are duplicates, or almost duplicates of one another.

◦ Major issue when merging data from heterogeneous sources.

Examples:

◦ Same person with mulDple email addresses.

Data cleaning

◦ Process of dealing with duplicate data issues.

◦ Involve studying the quality of each value and keep the one with higher quality factor and certainty.

When should duplicate data not be removed?

34

Data Preprocessing • AggregaDon

• Sampling

• DiscreDzaDon and binarizaDon

• AGribute TransformaDon

• Dimensionality ReducDon

• Feature subset selecDon

To be discussed later

• Feature creaDon

35

Aggregation

Combining two or more aGributes (or objects) into a single aGribute (or object)

Purpose

◦ Data reducDon - reduce the number of aGributes or objects

◦ Change of scale/granularity of analysis (from Yne-scale to coarser-scale)

◦ CiDes aggregated into regions, states, countries, etc.

◦ Days aggregated into weeks, months, or years

◦ More “stable” data - aggregated data tends to have less variability

reductios Datanging scale -\> from combining

Line-ecoarse

↳ if manager wants to know mostsequently can bought we item

tell ? OR which ↑salesstore has

?

\-> The a each dataset is

row fore

item, image how huge this is -\> The manager

want be able to

determine -\> we need

to aggregation

based do on need

\-> If whichhas most store

sales

for Jan. ↳ Aggregate

location by

& sules Store nmareserf ocation Zahia /Month/ san sany feb Total sales

, ミ -\> -\> now This (can manager makes be per can the 36 year data compare

stabie

tool

more

Exercise:

Aggregate the dataset in Figure 2.4 per each of the following features:

\- Item

\- Store LocaDon

\- Day

\- Month Show the dataset a\\er aggregaDon:=\>sales \_ water I Battery

\_ -\> Day)

sales shoes ㅣ

√-\> Moni Sales

37

Aggregation- Example

This example is based on precipitaDon in Australia from the period 1982 to 1993.

The next slide shows

◦ A histogram for the standard deviaDon of average monthly precipitaDon for 3,030 0.5◦ by 0.5◦ grid cells in Australia, and

◦ A histogram for the standard deviaDon of the average yearly precipitaDon for the same locaDons. The average yearly precipitaDon has less variability than the average monthly precipitaDon. All precipitaDon measurements (and their standard deviaDons) are in cenDmeters.

38

Aggregation- Example

For each cell we have: - Daily precipitaDon over the period Thus, we can calculate - The average monthly precipita0on - The average yearly precipita0on

Taking all the cells, for each cell we can calculate: - The std of the average monthly precipita0on over the years - The std of the average yearly precipita0on over the years

1982 . . .

1993

39

Aggregation- Example

VariaDon of PrecipitaDon in Australia

Standard Deviation of Average Monthly Precipitation

Standard Deviation of Average Yearly Precipitation

40

Sampling

• Sampling is the main technique employed for data reducDon. - It is o\\en used for both the preliminary invesDgaDon of the data and the Ynal data analysis.

• StaDsDcians o\\en sample because obtaining the enDre set of data of interest is too expensive or Dme consuming.

• Sampling is typically used in data mining because processing the enDre set of data of interest is too expensive or Dme consuming.

41

Sampling

The key principle for eOecDve sampling is the following:

◦Using a sample will work almost as well as using the enDre data set, if the sample is representaDve

◦A sample is representaDve if it has approximately the same properDes (of interest) as the original set of data

42

Sample Size

8000 points 2000 Points

500 Points

43

Types of Sampling

 Simple Random Sampling

◦ There is an equal probability of selecDng any parDcular item

◦ Sampling without replacement

◦ As each item is selected, it is removed from the populaDon

◦ Sampling with replacement

◦ Objects are not removed from the populaDon as they are selected for the sample.

◦ In sampling with replacement, the same object can be picked up more than once  StraDYed sampling

\-> make sure ◦ Split the data into several parDDons; you also take from minority the

then draw random class samples from each parDDon

44

Determining the Proper Sample Size

Requires a methodological approach:

◦ Take a small sample of data points, compute the pairwise similariDes between points and then form groups of points that are highly similar.

◦ The desired set of representaDve points is then obtained by taking one point from each of these groups.

◦ To follow this approach, we need to determine a sample size that guarantee, with high probability, the desired outcome (that is at least one point will be obtained from each cluster).

45

What sample size is necessary to get at least one object from each of 10 equal-sized groups.

The probability a sample contains points from each of the 10 groups6xnee -\> very low

\-> If we have

to groups of the

dataset tren take at least

Ex of the dalas

\-> 6x2 + Si of sample should

e に

0 -10 balls ㆁ

likehood of taking Starten as% all groups starts

increasing

For 10 zero almost \# of balls for-\> probability X

Determining the Proper Sample Size

Ten groups of points

46

Discretization

DiscreDzaDon is the process of converDng a conDnuous aGribute into an ordinal aGribute

◦A potenDally inYnite number of values are mapped into a small number of categories

◦DiscreDzaDon is used in both unsupervised and supervised sewngs

47

re width \_ - lther grade discritization interval -\> group each has same interval \*Equal

\*K-means -\> cusing calculates distance

me metrics) points distance discritization with outiers so similarity puts smallest

in -\> Not Smart , ㅇ same

group σ

Since mre dark bive are supposed to be in one group but tren f \* Eaval frequency discritization

\-> same\# of samples

in one Group uo Some points one will go to grapsome groa

not best Data consists of four groups of points and two outliers. Data is one- dimensional, but a random y component is added to reduce overlap.

Unsupervised Discretization

One group one graup ↳ Deciding

48

Unsupervised Discretization

Uniform (equal interval width) discreDzaDon: divides the range of aGributes into a user-speciYed number of intervals each having the same width.

49

Unsupervised Discretization

QuanDle (equal frequency) discreDzaDon: tries to put the same number of objects into each interval.

50

Unsupervised Discretization

K-means discreDzaDon: uses k-means clustering approach. It is the best among the discreDzaDon methods

\-> Best

51

Unsupervised Discretization

\* we sepearte X & \] features in one array from sklearn.preprocessing results in import one KBinsDiscretizer

array α name libray of X = \[\[-2, 1, -4, -1\],

\[-1, 2, -3, -0.5\], \[ 0, 3, -2, 0.5\],

\]

\->↳ samples \*import Create Object

train transform Ja transform fit 로 \[ 1, 4, -1, 2\]\] est strategy='uniform’)

\= KBinsDiscretizer(n\_bins=3, ⇌ ↳ \# encode='ordinal',

of groups \_↳ assume Hhere

est.fit(X)

Youo want create iorder Xt = est.transform(X) Xt Strategy is used to define the widths of the bins.

•‘uniform’: All bins in each feature have identical widths.

•‘quantile’: -\>Equal All bins brequeng

in each feature have the same number of points.

•‘kmeans’: Values in each bin have the same nearest center of a 1D k-means cluster.

52

Discretization in Supervised Settings

◦ DiscreDzaDon approaches that use class labels o\\en produce beGer classiYcaDon.

◦ A conceptually simple approach is to place the splits in a way that maximizes the purity of the intervals (the extent to which an interval contains a single class label)

◦ Entropy-based approaches are the most promising ones.

53

Juntlabel Pvesimpeverynhingnoshe t

' s se

MS 업s(

\<2)(2 함

\> ) -\> Must label encode &

( - Desauit

encoding 2)- \> custom 임\>(0) anything not A

' s

encode

\=

applied toOrdinalnatures -\> has -\>vey order Can't be to Suth not similar to

Ordinal like eye color)

label . Assume we ↳ Just to attributes three that (

categories. has orde have by Default alphesatically it'll be taken O. - It ≥ , make 2 …

doesn't sense always So

w do some custom order -\> Also Ordinal , Encoding Categorical Features and Labels In many cases, features and labels are not given as numerical values but as categorical values.

To input features and labels to machine learning algorithms, they need to be presented as numbers, i.e., encoded as integers.

Types of Encoders:

◦ Ordinal Encoders: {0, 1, 2, ..}

◦ for ordinal aGributes

◦ One Hot Encoding: Binary Encoding

◦ for nominal aGributes and can be used for ordinal aGributes

◦ Label Encoders: {0, 1, 2, ..}

but for labels -\> cause if by

◦ similar to ordinal encoders but applied to labels.

If 2 3 Can be -\> non needed applied encoding ordinal to since just ordinals date for ordinal

ordinal data

labels + 0 , 1 Deful- labers alphabetically 50 , 1 , 2

default - Als Will think its has 「 education tren BS

54

Feature Encoding: Ordinal Encoding

For example, a person could have features:

◦ Gender: \[‘male’, ‘female’\],

◦ Income: \[‘low income’, ‘middle income’, ‘high income’\],

◦ EducaDon: \[‘high school’, ‘BS’, ‘MS’, ‘PhD’\].

Using ordinal encoders, such features can be e}ciently coded as integers. Recommended encoding examples:

◦ ‘low income’ as 0

◦ ‘middle income’ as 1

◦ ‘high income’ as 2 And

◦ ‘high school’ as 0

◦ ‘BS’, as 1

◦ ‘MS’, as 2

◦ ‘PhD’ as 3

For ranks, where 1st place is of higher importance than 3rd place, recommended encoding is:

• ‘first place’ as 2

• ‘second place’ as 1

• ‘third place’ as 0 -\> alphabatically will be is hi l , m } -\> must be custom-\>1st takes ↑ will since be O & importance,

which is

real

55

Feature Encoding: Ordinal Encoding

import numpy as np \#Import the class from sklearn.preprocessing import OrdinalEncoder \#Create the object enc = OrdinalEncoder() X = \[\['male', 'low income', 'BS'\], \['female', 'high income', 'high school'\], \['female', 'middle income', ‘MS'\]\]

enc.fit(X) \#categorical values will be encoded based on the alphabetical order (not appearance)

enc.transform(\[\['male', 'high income', 'MS'\], \['female', 'middle income', 'high school'\]\])

Output

Gender Income Educa0on

male high income MS

female middle income high school

Gender Income Educa0on

1 0 1

0 2 2

array(\[\[1., 0., 1.\], \[0., 2., 2.\]\])

How come ‘middle income’ was encoded to a higher value than ‘high income’? And ‘high school’ was encoded to higher value than ‘MS’?

56

Feature Encoding: Ordinal Encoding

The previous examples showed that encoding is done in an alphabetical order by default. How to customize import numpy as it?

np \#Import the class from sklearn.preprocessing import OrdinalEncoder

\#Define the custom order custom\_order = \[\['female', 'male'\],\['low income', 'middle income', 'high income'\],\['high school', 'BS', 'MS', 'PhD'\]\] \# Custom order for the features

\#Create the object enc = OrdinalEncoder(categories=custom\_order)

X = \[\['male', 'low income', 'BS'\], \['female', 'high income', 'high school'\], \['female', 'middle income', 'MS'\]\]

enc.fit(X) enc.transform(\[\['male', 'high income', 'MS'\], \['female', 'middle income', Output array(\[\[1., 'high 2., 2.\], school'\]\]) \[0., 1.,

0.\]\])

57

Binarization

BinarizaDon maps a conDnuous or categorical aGribute into one or more binary variables Called one-hot encoding in SkLearn

\->sordeoneencodinousiedi

BetteOrdinates Ordina a

then one-not

lowesae should n have qwresorpocat

rating " o

awful poor OK good great creates Cos for each Categones

1 for acc con-redundant one, If o for not So many categories , we willㄱ&↑ gsodimensionality selectionsindorrel

dataset nee

With class final .

58

Feature Encoding: One-Hot Encoding import numpy as np

\#Import the class from sklearn import preprocessing \#Create the object enc = preprocessing.OneHotEncoder() X = \[\['male', 'from US', 'uses Safari'\], \['female', 'from Europe', 'uses Firefox'\]\]

enc.fit(X)

enc.transform(\[\['female', 'from US', 'uses Safari'\], \['male', 'from Europe', 'uses Safari'\]\]).toarray()

Output Gender \_Female Gender \_Male Country \_Europe Country \_US Browser \_FireFox Browser \_Safari

1 0 0 1 0 1

0 1 1 0 0 1

Gender Country Browser

Female US Safari

Male Europe Safari

59

Label Encoding

LE.transform(\['Iris-virginica', 'Iris-setosa'\])

LE.inverse\_transform(\[1, 1, 2, 0\])

Works similar to ordinal encoding

from sklearn.preprocessing import LabelEncoder LE = LabelEncoder() y = \['Iris-versicolor', 'Iris-setosa', 'Iris-setosa', 'Iris- virginica'\] LE.fit(y) print(LE.classes\_) \#ordered alphabetically, which is fine

Output

Output

Output

60

Attribute Transformation

An aGribute transform is a funcDon that maps the enDre set of values of a given aGribute to a new set of replacement values such that each old value can be idenDYed with one of the new values ◦Simple funcDons: xk, log(x), ex, |x|

◦NormalizaDon or standardizaDon

◦ The goal is to make an enDre set of values have a parDcular property.

◦ A tradiDonal example in staDsDcs, it refers to subtracDng oO the mean and dividing by the standard deviaDon. This will create a new variable that has a mean of 0 and a standard deviaDon of 1.

61

Height : 1 .SM-2 .2 mData Normalization or Scaling \_행o mals

ㅋ roarage "'sn

‰in Quantity Why

oe "

30 - 10 Transform features by scaling each of them (even if to a given range.

to 0 . 7 (nDiOerent scalers can be used.

Examples:

◦ Standariza0on: rescaling the data to have a mean of 0 and a standard deviaDon of 1. StandardScaler in Sklearn

◦ Min-Max Scaling: rescales the data to falls in the \[0, 1\] range. MinMax Scaler in Sklearn

So , S3) 굽 omp. \[ -\> some So in alg

it only focuses If we ranges compare Price its huge big range On range the - huge

not which good Pred . age small range noaac .:

need to apply normalization

where x is the original value, is the mean of the feature values, σ is the standard deviation of the feature values, and x’ is the value of x after transformation.

62

Data Normalization or Scaling: MinMax Scaler

from sklearn.preprocessing import MinMaxScaler import numpy as np

X = np.array(\[\[ 1., -1., 2.\], \[ 2., 0., 0.\], \[ 0., 1., - 1.\]\])

min\_max\_scaler = MinMaxScaler()

X\_new = min\_max\_scaler.fit\_transform(X)

X\_new

Output

63

Data Normalization or Scaling: Standard Scaler

from sklearn import preprocessing import numpy as np

X = np.array(\[\[ 1., -1., 2.\], \[ 2., 0., 0.\], \[ 0., 1., -1.\]\])

standard\_scaler = preprocessing.StandardScaler()

X\_new = standard\_scaler.fit\_transform(X)

X\_new

Output

64

Feature Scaling in SKLearn

65

Learning Outcomes

1\. Perform machine learning steps including data prepara0on, task idenDYcaDon, model selecDon, and evaluaDon.

2\. Employ mathemaDcal methods to explain the theoreDcal aspect of machine learning and data mining techniques.

3\. Select appropriate supervised learning methods including classiYcaDon and regression for given problems and datasets.

4\. Use unsupervised learning methods such as clustering and associaDon rule mining to discover paGerns and relaDonships in datasets.

5\. Apply feature selecDon and dimensionality reducDon methods.

6\. Use state-of-the-art so\\ware to explore and solve pracDcal machine learning problems.

66
