# IntroML (CMP 466) — 04 Decision Trees
> Source: Google Drive file 1lkPxAN50ffkLZNkdbIaVYSM-AXt7h6FG · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466- Machine Learning and Data Mining

Chapter 3: Decision Tree

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

• Decision Trees concept

• Decision Trees Classi2ca3on

• Decision Trees Parameters Tuning

• Over2:ng

• Decision Trees in SKLearn\!

2

Decision Trees Concept

Decision tree is tree structure used for classi2ca3on or regression. The tree has decision nodes and leaf nodes.

• Decision nodes represent ques3ons about features (e.g., Home Owner?), which have two or more branches (e.g., Yes and No).

• Leaf nodes (e.g., Defaulted Borrower --\> Yes, Defaulted Borrower --\> No) represents a classi2ca3on or decision.

• Decision trees can handle both categorical and numerical data.

ID Home Owner

Marital Status

Annual Income

Defaulted Borrower

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

Home Yes OwnerNo

NO

Marital Status

Single, Divorced Married \< 80K Income

\> 80K

NO

NO

YES

3

Is Decision Trees Concept

this data linearly separable? No\!Sun

Wind

gn督

影

4

Decision Trees Concept

Decision trees allows you to ask mul3ple “Linear ques3ons” to classify a non-linearly separable dataset

why do we build

it : windy

Sun

Sunny

cause now we have a Prediction model that allows Predict Os to labels directly Sunny? ees)ta ×

yee Λ no \_\_

⑦ X

Not

Prediction for sunny

Sonny not windy - look

not windy | windy

Winda Desicion tree -\> immediatel Not windy we say X can't surf

5

Decision Trees Concept

\_↳ There is an

algontuim convents

that Ds - Tree by equations Sample decision tree for this dataset\!

Sun

Windy?

Yes No

Sunny?Yes No

Wind

6

× 2 \< 2 Decision Trees Concept

ee/o × X 1 a 3

ses/ no

\* X2 se

yon .

Can we build the decision tree to classify this sample set? Hint: Start spli:ng using X1X2

5 - 4 -

Can we build a di\\erent decision tree? Hint: Start spli:ng using X2 3 - 2 - 1 -

We can have di\\erent

1 2 3 4 5

X1

decision trees for the same sample set.

7

Decision Trees Concept

Sample decision tree for this dataset\!

X1 \< 3? Yes No X2

X2 \< 2 ?

5 -

Yes No 4 - 3 - 2 - 1 -

1 2 3 4 5

X1

X2 \< 4 ? Yes No

8

Decision Trees

Impurity controls how DT decides where to spit the data Goal: Find features (split points) to make subset that are as pure as possible

X2

X2

purer subset

5 -

5 - 4 -

4 - 3 -

3 - 2 -

2 - 1 -

1 -

1 2 3 4 5

X1

1 2 3 4 5

X1

9

General Approach for Building Classification Model

Apply Model

Training Phase Tid Attrib1 Attrib2 Attrib3 Class

Learning 1 Yes Large 125K No

algorithm 2 No Medium 100K No

3 No Small 70K No

4 Yes Medium 120K No

Induction 5 No Large 95K Yes

6 No Medium 60K No

7 Yes Large 220K No

8 No Small 85K Yes

9 No Medium 75K No

10 No Small 90K Yes

10

Training Set

Tid Attrib1 Attrib2 Attrib3 Class

11 No Small 55K ?

12 Yes Medium 80K ?

13 Yes Large 110K ?

Deduction

14 No Small 95K ?

15 No Large 67K ?

Tes3ng and Evalua3on

10

Test Set

Phase Learn Model

Model

15

Example of a Decision Tree

categoricaclategorical

continuoucslass

Splitting Attributes ID Home Owner

Marital

Annual

Defaulted Status

Income

Borrower

1 Yes Single 125K No

Home 2 No Married 100K No

3 No Single 70K No

Owner Yes No

4 Yes Married 120K No

NO

MarSt

5 No Divorced 95K Yes

Single, Divorced Married 6 No Married 60K No

7 Yes Divorced 220K No

Income

NO

8 No Single 85K Yes

\< 80K \> 80K

9 No Married 75K No

NO YES 10 No Single 90K Yes

10

Training Data Model: Decision Tree

16

Another Example of Decision Tree

ID Home Owner

categoricaclategorical

continuoucslass Married

MarSt

DivorcedSingle,

Marital

Annual Status

Income

Home Owner

Income \< 80K \> 80K

NO YES There could be more than one tree that fits the same data\! Defaulted Borrower

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

NO

Yes No

NO

17

Apply Model to Test Data

Start from the root of tree.

Test Data Home

Marital

Annual

Defaulted Home

Owner

Status

Income

Borrower Yes Owner

No

No Married 80K ?

10 MarSt

Single, Divorced

Married

Income

\< 80K \> 80K

NO YES NO

How to use it

for prediction

NO

18

Apply Model to Test Data

MarSt

Income

NO

YES Defaulted Borrower

No Married 80K ? 10 Test Data Home Owner

Home Owner

Marital Status

Annual Income

Yes No

NO

Single, Divorced

Married NO

\< 80K \> 80K

19

Apply Model to Test Data

Defaulted Borrower

No Married 80K ? 10 Test Data Home Owner

Home

Marital

Annual Owner

Status

Income

Yes No

NO

MarSt

Single, Divorced Married Income

NO

\< 80K \> 80K

NO

YES

20

Apply Model to Test Data

Defaulted Borrower

No Married 80K ? 10 Test Data Home Owner

Home

Marital

Annual Owner

Status

Income

Yes No

NO

MarSt

Single, Divorced Married Income

NO

\< 80K \> 80K

NO

YES

21

Apply Model to Test Data

Defaulted Borrower

No Married 80K ? 10 Test Data Home Owner

Home

Marital

Annual Owner

Status

Income

Yes No

NO

MarSt

Single, Divorced Married Income

NO

\< 80K \> 80K

NO

YES

22

Apply Model to Test Data

Defaulted Borrower

No Married 80K ? 10 Test DataHome

Marital

Annual Owner

Status

Income

Home Yes Owner

No

NO

MarSt

Single, Divorced

Married Assign “No” Defaulted to Income

NO

\< 80K \> 80K

NO

YES

23

Decision Tree Classification Task

Tid Attrib1 Attrib2 Attrib3 Class

1 Yes Large 125K No

2 No Medium 100K No

Tree Induction algorithm

3 No Small 70K No

4 Yes Medium 120K No

5 No Large 95K Yes

6 No Medium 60K No

7 Yes Large 220K No

8 No Small 85K Yes

9 No Medium 75K No

10 No Small 90K Yes

10

Training Set

Tid Attrib1 Attrib2 Attrib3 Class

Apply Model

Decision Tree

11 No Small 55K ?

12 Yes Medium 80K ?

13 Yes Large 110K ?

14 No Small 95K ?

15 No Large 67K ?

10

Test Set

Induction

Deduction

Learn Model

Model

24

vor Decision Tree Induction

wise

Greedy algorimim s ohherones

Many ◦ Hunt’s Algorithms:

Algorithm (one of the earliest) ↳  in Uses each algorini a greedy shorrest step m search.

tre chooses cost/ benefit max He ◦ ID3  Uses Hunt’s algorithm. Select split aiributes using the informa3on gain criterion.

◦ C4.5  improvement over ID3. Handles missing aiributes and con3nuous aiributes. Performs tree post-pruning.

◦ CART  constructs binary trees. Select split aiributes using the GINI index.

^ early Stopping

↳ wanting g

◦ SLIQ  Sort the values for every airibute. Builds the tree certain

cepir “breadth-2rst“, not “depth-2rst“.

◦ SPRINT scalable parallel.

\-> recorssive alg X sopsiscompletely a are

pure or if ne data set points

have exactly same

features

Anst

25

Greedy General Structure of Hunt’s Algorithm

alg ↳ stops if you

reach a pure

set .

Hunt's algorithm grows a decision tree in a recursive fashion by par33oning the training records into successively purer subsets.  Let a node Dt be t

the set of training records that reach

 General Recursive Procedure :

–If class Dt contains records that belong the same

yt, then t is a leaf node labeled as yt –If than Dt contains records that belong to more

one class, use an airibute test to split the data into smaller subsets. Recursively apply the procedure to each subset.

ID Home Owner

Marital Status

Defaulted Borrower

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

Dt

?

Annual Income

26

Stopping Criteria of Hunt’s Algorithm

Hunt's algorithm terminates when

• All records in a node belong to the same class.

• All the records in a node have iden3cal airibute values. Even if records have di\\erent class labels, it is not possible to split these records any further.  The node is declared a leaf node with the same class label as the majority class of training records associated with this node.

27

Hunt’s Algorithm

Need Assume to the do selecHon:

best spli:ng airibute was Home Owner Majority of samples have class NO

ID Home Owner

Marital

Annual Status

Income

Number of samples in class NO

Assume the best spli:ng airibute here was Marital Status

Assume the best spli:ng airibute here was Annual Income

Defaulted Home

Borrower Owner

1 Yes Single 125K No

Defaulted = No

Yes No

2 No Married 100K No

(7,3)

Number of

Defaulted = No Defaulted = No

3 No Single 70K No

(a) samples class Yes

no inges nose-\>need

spore 4 5 Yes No Married 120K No

Divorced 95K Yes

need

6 No Married 60K No

7 Yes Divorced 220K No

8 No Single 85K Yes

9 No Married 75K No

10 No Single 90K Yes

10 Yes No

Marital Status Single, Divorced Married

(d)

0f

07

tospiteons to No \&stops

when ∞

pure

∞

둡 nou fantas in

(3,0) (b)

Noeyes (3 .0) d ... choose 엄디않 m Stop ,pore power best dataset Sub set

(4,3)

(3,0)

(1,3) (3,0)

(c)

Impure need to split\!

Home Owner

Home

Yes No Owner

Defaulted = No

Marital Status Defaulted = No

(3,0)

Divorced Single,

Married

Annual Income

Defaulted = Yes

Defaulted = No \< 80K \>= 80K

Defaulted = No

Impure need

(1,0) (0,3) to split\! All are pure. Done\!

Defaulted = No

(3,0)

Defaulted = Yes

28

Design Issues of Decision Tree Induction

 How should training records be split?

– Method for specifying test condiHon (spliOng aPribute)

 depending on airibute types – Measure for evaluaHng the goodness of a test condiHon How should the spli:ng procedure stop?

–Stop spli:ng if all the records belong to the same class or have iden3cal airibute values –Early termina3on

29

Methods for Expressing Test Conditions

 Depends on airibute types

– Binary – Nominal – Ordinal – Con3nuous

30

Test Condition for Nominal Attributes

• Mul3-way split:

– Use as many par33ons as dis3nct values.

• Binary split:

– Divides values into two subsets

↑ทดสอบชื่

∞

\-> on\#Starare

pina

Marital Status

Single Divorced Married

Marital

Marital

Marital Status

Status StatusOR OR

{Married} {Single,

{Single} {Married, Divorced}

Divorced}

{Single,

{Divorced} Married}

31

Test Condition for Ordinal Attributes

• Mul3-way split:

– Use as many par33ons as dis3nct values

• Binary split:

– Divides values into two subsets – Preserve order property among airibute values

\_↳ast alg Wilsere order

wherencode

we ordinal as

\-> Dont nominal encode

a ordinal cause limits digs the

type of grouping

canad

Shirt Size

Small

Medium Large Extra Large Shirt Size

{Small,

{Medium, Large, Medium}

Extra Large}

{Medium, Extra Large}

Shirt Size

{Large, {Small} Extra Large}

Shirt Size

{Small, Large}

This grouping violates order property

32

Test Condition for Continuous Attributes

• Binary Split: (A \< v) or (A  v)

◦ Consider all possible splits and 2nds the best cut

◦ Can be more compute intensive - equal equal • Mul3-way split (Discre3za3on) to form an ordinal categorical airibute Ranges can be found by equal interval bucke3ng, equal frequency bucke3ng (percen3les), or clustering.

◦ Sta3c – discre3ze once at the beginning

◦ Dynamic – repeat at each node Annual Income \> 80K?

Yes No

widte/ interval

Annual Income?

\< 10K

\> 80K

\[10K,25K) \[25K,50K) \[50K,80K)

(i) Binary split (ii) Multi-way split

33

How to determine the Best Split

4Before Splitting: 10 records of class 0,

10 records of class 1

서4

Which test condition is the best?

เสียSee aDAYresPoste

6

Gender

∠ Car

Type M F

\->stupid → quantatively esaraza

mis

C0: 6

C0: 1 C1: 4

C1: 0 s Yes No FamilyLuxury Sports

c1 c10

C0: 4

C0: 1

C0: 8

C0: 1

beter since subsetssoall purt aeit

C1: 6

Tamopore C1: 3

C1: BureAmosre 0

C1: 7

\-> So drop this secutrecausechooseaus

icterit

Customer ID

c11

c20

...

C0: 1 C1: 0

C0: 0 C1: 1 ...

C0: 0 C1: 1

34

How to determine the Best Split

• Greedy approach: – Nodes with purer class distribu3on are preferred

• Need a measure of node impurity:

C0: C1: 5 5 -applesze - Orange High degree of impurity Low degree of impurity

not nice C0: 9

sorance

nice

C1: 1

\-appie

ー↳ really bad

set

35

Measure of Impurity: GINI

Gini Index for a given node

Where is the relative frequency of class at node , and is the total number of classes

◦ Maximum of when records are equally distributed among all classes, implying the least bene2cial situa3on for classi2ca3on

◦ Minimum of 0 when all records belong to one class, implying the most bene2cial situa3on for classi2ca3on

◦ Gini index is used in decision tree algorithms such as CART, SLIQ, SPRINT

2 can Eassersa \[ Grigo -\>

GINF =

⼯ — (前

\+信 )》

\*Minimum GINI Maximum x=\> when GINI

we have \!"\#" (−1Op

more )"(\*)2 the distributed sample across the equally classes Ex $\#%&'=1−∑a : bag so a can't If bag orangesof I predict of so have

\>\> applesapples , its

I so, % incorr "=0

1

ー (

\+ u荒) エー () →約

\= 0

\- 586

36

\* Measure Max GINI = 0 . S for two of classes Max for Impurity: classes 3 = → ユー コー GINI

(法)㎡+(市 + ⽅ ( )←()

← 坊) マー予

→ 그를 s 2.1

\-> 0 .667 Gini Index for a given node t :

\!"\#" $\#%&'=1−∑(−1st·

of )"dasses (\*)2

cak for

Co : S 업α a mat metric quantiles ◦ For 2-class problem (p, 1 – p):

◦ GINI = 1 – p2 – (1 – p)2 = 2p (1-p)

Example:

Gini = Gini =

"=0 degree of impurity ㅇ

, ± CI : S

f lower

Gn = I Giu = -

0国巡 (1 - (0 . 81 + 0 .01) aegree =0.18 impunits 어 Gin = A - ( CO

\- S)'

\+ loss) ebest

o.

case plowdegeete C1 0

C1 1

C1 2

\= 1 - O

. S

C1 3

\= O

. S

C2 6

C2 5

C2 4

C2 3

\-> worst Gini= 0.000

Gini= 0.278

Gini= 0.444

Gini= 0.500

case

↑

tdegree of imp perfectlyPure

S Gin = -(응)로의 = 1 - ± -\> Min Gini- O ℃

37

\-> cal impurity Computing Gini Index of a Single Node \!"\#" $\#%&'=1−∑(−1)"(\*)2

"=0 C1 0 C2 6 Gini= 0.000

\= 0/6 = 0 = 6/6 = 1

Gini = 1 – P(C1)2 – P(C2)2 = 1 – 0 – 1 = 0

C1 1 C2 5

\= 1/6 = 5/6

Gini= 0.278

Gini = 1 – (1/6)2 – (5/6)2 = 0.278

C1 2 C2 4

\= 2/6 = 4/6

Gini= 0.444

Gini = 1 – (2/6)2 – (4/6)2 = 0.444

38

Computing Gini Index for a Collection of Nodes  When a node is split into par33ons (children)  weighted average of Gini index of children

where, = number of records at child ,

\= number of records at parent node .

 Choose the airibute that minimizes weighted average Gini index of the children.

\* we use GINI

to choose the

best split

. We need the data to Split

based

on one attribute. =\> we measure based

on each attribute E choose one with he

least

impunits

\!$+ $,)-"\*=∑. "=1\#"\# \!$+$(")

1□ GINT ㅅ\~ GINI GINI GINI ㄕ saity\~ 2ō GINI GINI =\> α =\> compare, & choose one with Split

weighted average of GINI

at each branch So \# of samples One branch\> branch it in

Other has a weight min GINI

39

\*Binary Attributes: Computing GINI Index

have IJ we

attr.

C-we

 Splits into two partitions (child nodes)

same would process

follow

 Effect of Weighing partitions:

GINI 그 = – Larger N1 : - ((주 )+()) 1 - . β. = 0

. 28

and purer GINISplit partitions ☆L ← sampie

( in w are GINI^ Total B? G型 )\~+ (告㎡)

그=-

(") Yes ten choose sought.

g

\# of samples No one with less GINI 'NI 告 ( GINI) N2

∞ Total 탈(.)발(') No = 니 a Node N1 Node N2

몲= 0

\-36

Gini = 0.486

Weighted Gini of N1 N2 = 6/12 \* 0.278 + 6/12 \* 0.444 = 0.361

Gini=0.361

Gini(N1) = 1 – (5/6)2 – (1/6)2 = 0.278

Gini(N2) = 1 – (2/6)2 – (4/6)2 = 0.444

Parent C1 7 C2 5

N1 N2 C1 5 2 C2 1 4

40

Categorical Attributes: Computing Gini Index

• For each dis3nct value, gather counts for each class in the dataset

• Use the count matrix to make decisions

CarType {Sports, Luxury} {Family} C1 9 1 C2 7 3 Gini 0.468

\-Binay Multi-way split Two-way split

(find best partition of values)

CarType

CarType

Family Sports Luxury C1 1 8 1

{Sports} {Family, Luxury} C1 8 2 C2 3 0 7

C2 0 10 Gini 0.163

Gini 0.167 GINIFam ニュー (亢

\+ 告) s 0

\-37 s Which of these is the best? The one that has the least Gini index GIWI sports = =

\- ((E)2) =\> 0 GINI l 0 xY = ュ - (店 、 +) u =\> Gini Split= (0.375) + (0

.2187s)

0

. 07s + 0 . 0875 41

\= 0 . 163

Continuous Attributes: Computing Gini Index ↳ If • Use Binary Binary Decisions Split based we on need Alg one will to value

choose choose minimizes a impurity value value

that

• Several Choices for the spli:ng value

\=\> chooses a

value that

Gives pure Subset –Number of possible spli:ng values = Number of dis3nct values

\=\>split My value mies 울 a Calc does

several

GINI split , a we

• itEach spli:ng value has a count matrix associated Choose with one GINI

min

Spirt

that

–Class counts in each of the par33ons, A \< v and A  v

• Simple method to choose best v –For each v, scan the database to gather count matrix and compute its Gini index –Computa3onally Inetcient\! Repe33on of work.

ID Home

Owner

Marital Status

Income Annual

Defaulted

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

Annual Income ?

≤ 80 \> 80

Defaulted Yes 0 3

Defaulted No 3 4

42

Continuous Attributes: Computing Gini Index...

 For etcient computa3on: for each airibute,

– Sort the airibute on values – Linearly scan these values, each 3me upda3ng the count matrix and compu3ng gini index – Choose the split posi3on that has the least gini index

Split Positions

Cheat No No No Yes Yes Yes No No No No

Sorted Values

Annual Income

60 70 75 85 90 95 100 120 125 220 55 \<= \> 6 65 \<= \> \<= s지\!

72 \> 80 87 \<= \> \<= \> \<= 에92 a\> \<= 빛.

97 \> 110 \! " \<= \> 122 0 \<= \> 172 n

230

\<= \> \<= \>

Yes No 0 3 0 0 7 1 3 6 0 2 3 0 5 85us 3 3 4 1 3 2 4 2 3 1 4 103여 3 3 0 3 0 4 4 3 3 5 0 ....

3 0 3 0

2 6 1 7 0

Gini 0.420 0.400 0.375 0.343 0.417 0.400 0.300 0.343 0.375 0.400 0.420

43

Continuous Attributes: Computing Gini Index...

 For etcient computa3on: for each airibute,

– Sort the airibute on values – Linearly scan these values, each 3me upda3ng the count matrix and compu3ng gini index – Choose the split posi3on that has the least gini index

Split Positions

Cheat No No No Yes Yes Yes No No No No

Sorted Values

Annual Income

60 70 75 85 90 95 100 120 125 220

55 65 72 80 87 92 97 110 122 172 230

\<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \>

Yes 0 3 0 3 0 3 0 3 1 2 2 1 3 0 3 0 3 0 3 0 3 0

No 0 7 1 6 2 5 3 4 3 4 3 4 3 4 4 3 5 2 6 1 7 0

Gini 0.420 0.400 0.375 0.343 0.417 0.400 0.300 0.343 0.375 0.400 0.420

44

Continuous Attributes: Computing Gini Index...

 For etcient computa3on: for each airibute,

– Sort the airibute on values – Linearly scan these values, each 3me upda3ng the count matrix and compu3ng gini index – Choose the split posi3on that has the least gini index

Split Positions

Cheat No No No Yes Yes Yes No No No No

Sorted Values

Annual Income

60 70 75 85 90 95 100 120 125 220

55 65 72 80 87 92 97 110 122 172 230

\<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \>

Yes 0 3 0 3 0 3 0 3 1 2 2 1 3 0 3 0 3 0 3 0 3 0

No 0 7 1 6 2 5 3 4 3 4 3 4 3 4 4 3 5 2 6 1 7 0

Gini 0.420 0.400 0.375 0.343 0.417 0.400 0.300 0.343 0.375 0.400 0.420

45

Continuous Attributes: Computing Gini Index...

 For etcient computa3on: for each airibute,

– Sort the airibute on values – Linearly scan these values, each 3me upda3ng the count matrix and compu3ng gini index – Choose the split posi3on that has the least gini index

Split Positions

Cheat No No No Yes Yes Yes No No No No

Sorted Values

Annual Income

60 70 75 85 90 95 100 120 125 220

55 65 72 80 87 92 97 110 122 172 230

\<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \>

Yes 0 3 0 3 0 3 0 3 1 2 2 1 3 0 3 0 3 0 3 0 3 0

No 0 7 1 6 2 5 3 4 3 4 3 4 3 4 4 3 5 2 6 1 7 0

Gini 0.420 0.400 0.375 0.343 0.417 0.400 0.300 0.343 0.375 0.400 0.420

46

Continuous Attributes: Computing Gini Index...

 For etcient computa3on: for each airibute,

– Sort the airibute on values – Linearly scan these values, each 3me upda3ng the count matrix and compu3ng gini index – Choose the split posi3on that has the least gini index

Split Positions

Cheat No No No Yes Yes Yes No No No No

Sorted Values

Annual Income

60 70 75 85 90 95 100 120 125 220

55 65 72 80 87 92 97 110 122 172 230

\<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \> \<= \>

Yes 0 3 0 3 0 3 0 3 1 2 2 1 3 0 3 0 3 0 3 0 3 0

No 0 7 1 6 2 5 3 4 3 4 3 4 3 4 4 3 5 2 6 1 7 0

Gini 0.420 0.400 0.375 0.343 0.417 0.400 0.300 0.343 0.375 0.400 0.420

47

Measure of Impurity: Entropy

 Entropy at a given node

Where is the relative frequency of class at node , and is the total number of classes  Maximum of when records are equally distributed among all classes, implying the least bene2cial situa3on for classi2ca3on

Minimum of 0 when all records belong to one class, implying most bene2cial situa3on for classi2ca3on – Entropy based computa3ons are quite similar to the GINI index computa3ons

\=\> Shanon

Entropy

/\#\*01)2=−∑catporits

(−1)"(\*)-132)"(\*) "=0

48

CI Computing Entropy of a : O C 2 : 6 thenerimpurity PreConti

\= O Single /\#\*01)2=−∑Node MAX- \> 1092C (−1)"(\*)-132)"(\*)

"=0

GINエ = ュー (路) =0 envopy = -( 号109号

\+ 号 103÷)

\= - foto) =0

CI : 그

C2 : S C1 0 C2 6

Entropy :

Gini -(-109: 0

. 28

,

\+5 109 , 5)

\=\> 0.6S

\=\>Not 0 . 28 Entropy : C1 : S GINI-O-S

czis - (늘 1og는

← 늘(0 s

C1 2 C2 4

\= 0/6 = 0 = 6/6 = 1

Entropy = – 0 log 0 – 1 log 1 = – 0 – 0 = 0

C1 1

\= 1/6 = 5/6

C2 5

Entropy = – (1/6) log2 (1/6) – (5/6) log2 (5/6) = 0.65

\= 2/6 = 4/6

Entropy = – (2/6) log2 (2/6) – (4/6) log2 (4/6) = 0.92

.1.)

그

\_

49

Computing Information Gain After Splitting

 Informa3on Gain:

Parent Node, , is split into par33ons (children)

is number of records in child node = number of records at parent node .

– Choose the split that achieves most reduc3on (maximizes GAIN)

– Used in the ID3 and C4.5 decision tree algorithms

– Informa3on gain is the mutual informa3on between the class variable and the spli:ng variable

how

learnt

model from

split Enkropy

9 paent bettera means ー much gand \!4"\#,)-"\*=/\#\*01)2())−∑. , modeearned a lot "=1ー mat \#"\# /\#\*01)2(")

weighted aug of entropy 9 chlcen ↳ Smaller

this causeyouthe better,

a ge

50

Computing Information Gain After Splitting

1\. Compute entropy before spli:ng; 2. Compute entropy aver spli:ng by:

•Compu3ng entropy for each child node, , where is the node number.

•Compu3ng the weighted entropy of the all child nodes 3. Choose the airibute test condi3on that produces the highest informa3on gain () or equivalently, the lowest weighted entropy aver spli:ng

51

Finding the Best Split

C0 N10 C1 N11

parent ^ Before Splitting:

C0 N00 C1 N01 P

A?

B?

Yes No

Yes No

Node N1 Node N2

Node N3 Node N4

C0 N20

C0 N30

C0 N40 C1 N21

C1 N31

C1 N41

M11 sende 1 M12 stychih

M21 M22

M1 -weignied Gug

M2 Gain = P – M1 vs P – M2

\> -One with garin, is

chosen

52

Problem with large number of partitions

Node impurity measures tend to prefer splits that result in large number of par33ons, each being small but pure

Enomid있 Gender

\-sovon gain small I Car

Good Gain info Type

M Fc11 C0: 6 C1: 4

–Customer ID has highest informa3on gain because entropy for all the children is zero

e Gain\&ise

Parent -\>Dont feed

\-> will

eelccted

C0: 1 C1: 0

Customer ID

Yes No FamilySports

Luxury c1 c10

c20

C0: 4

C0: 1

C0: 8

C0: 1 C1: 6

C1: 3

C1: 0

C1: 7

...

C0: 1 C1: 0

C0: 0 C1: 1 ...

C0: 0 C1: 1

53

Gain Ratio

\->ignous

 Gain Ra3o:

– Adjusts Informa3on Gain by the entropy of the par33oning ().

Higher entropy par33oning (large number of small par33ons) is penalized\! – Used in C4.5 algorithm – Designed to overcome the disadvantage of Informa3on Gain

Parent Node, , is split into par33ons (children)

is number of records in child node

\= number of records at parent node .

54

0.620 Gain Ratio

\->ignal

CarType {Sports, Luxury} {Family} C1 9 1 C2 7 3

, 0.72, 0.97

Parent Node, is split into par33ons (children) is number of records in child node

CarType Family Sports Luxury C1 1 8 1 C2 3 0 7

55

0.047

CarType {Sports} {Family, Luxury} C1 8 2 C2 0 10

0.609

Measure of Impurity: Classification Error - Have &  Classi2ca3on - error one a at bag -\> a single of node

you apple applessay Orange anorangewhen bag of \_–Maximum (1 - 1/c) when records are equally distributed among all classes, implying least interes3ng informa3on

–Minimum (0) when all records belong to one class, implying most interes3ng informa3on

ㆁ error S/1 os error soil ← σ CI : 0 -\> usuas you , have cause 어 generalization Or ra3o of the

C2 : 6 cassified as

C2 müsClasse, errorroses to%

one

\->minority

outnumbered Error Fois 2 classed e

/0010 (\*)=1− max

\_ " ⁡\[)"(\*)\]

↳ maximum incorrectly

classi2ed -\> so orange samples misclassified

ㅗ 'Frequensame

品□ 3/8- error"

& \_⼀← 0 .37s CI Ca classized . S : lo s

%

So - anything as minority -\>\> misclassified

56

Computing Error of a Single Node

/0010 (\* )=1− max " C1 0 C2 6

C1 2 C2 4

⁡\[)"(\*)\]

\= 0/6 = 0 = 6/6 = 1

Error = 1 – max (0, 1) = 1 – 1 = 0

C1 1

\= 1/6 = 5/6

C2 5

Error = 1 – max (1/6, 5/6) = 1 – 5/6 = 1/6

\= 2/6 = 4/6

Error = 1 – max (2/6, 4/6) = 1 – 4/6 = 1/3

57

Comparison among Impurity Measures

\=\> Graphy Symmetric so when cause two classes

P =0 =100 you Relative frequency get results

same- \> G CI : 0

\=\>C2 C2 : 100

as if P1 =100 , Pr =o

Gini : O-pure

enmory: ·

error: ↳noting misclassified Relative frequency -\> 20%CI : 20 C2 : So

Gini : entropy.

03 Zre

Error : 20%

\=\> calculation ↳ Gini & by

entropyequation Relative ct : so frequency { Entropy Gini : For a 2-class problem: : 1

)"0 (\* )

\-> relative hequensy classi, 50%

At at mode t c2 : so d 0. S

error : 50%

max

58

Misclassification Error vs Gini Index \#Doesn't improve

A?

b나 impunity Yes No improvesNode N1 Node N2

\=\>error 36% Becamepure

\#error still

30% =\>Emor cak

only misclassified samples

Parent C1 7 C2 3 Gini = 0.42

Gini(N1) = 1 – (3/3)2 – (0/3)2 = 0 Gini(N2) = 1 – (4/7)2 – (3/7)2

N1 N2 C1 3 4 C2 0 3 Gini= 0.342

\= 0.489

Gini(Children) = 3/10 \* 0 + 7/10 \* 0.489 = 0.342

Gini improves but error remains the same\!\!

59

Misclassification Error vs Gini Index A?

\-> classification

erron - not sensitive distribution

o

Parent

\=\>impurity improves error Yes doesn't

No

C1 7 C2 3

Node N1 Node N2

Gini = 0.42

8 Best N1 Split N2

But

still same error

G 30 %

emor N1 N2 C1 3 4 C2 0 3 Gini= 0.342

C1 3 4 C2 1 2 Gini= 0.416

쯤

\=→ 30%

G 30%

error =\>Gini affected Misclassification error for all three cases = 0.3 \!

by distribution across nodes

60

Decision Tree Based Classification

Advantages:

–Rela3vely inexpensive to construct –Extremely fast at classifying unknown records –Easy to interpret for small-sized trees –Robust to noise (especially when methods to avoid over2:ng are employed) –Can easily handle redundant aiributes –Can easily handle irrelevant aiributes (unless the aiributes are interac3ng) –Basis for other ensemble classi2ers –Insensi3ve to feature scales Disadvantages:

–Does not take into account interac3ons between aiributes. Due to the greedy nature of spli:ng criterion, interac3ng aiributes (that can dis3nguish between classes together but not individually) may be passed over in favor of other aiributed that are less discrimina3ng. –Each decision boundary involves only a single airibute –Prone to over2:ng specially when there is a large number of feature (need to stop the growth of the tree at the right 3me) –Space of possible decision trees is exponen3ally large. Greedy approaches are oven unable to 2nd the best tree.

\=\> non engineers

Prefer Mc \> Deep learning since clear

\=\>Data Split

per attribute at

a time

γ

\=\> So assume scaling a dataset

even diseases

GPA doesn't when

in matter

\=\> for continuous values· ↳ Since affected all in features knw when we had Gok-2201 =mid β

income=\> even if GItinwonttree cause

bein the

on ean.

. =\> Ff we scale \[o Ψ ー

ao tyuScSplit ae l

Robus

we baneselection

seame

was 1) 97 MmiddleincomeoS KNNnot GPA would robut be -

within usedcau edist- metric

)I 8onyrelaked work.

\=\> need to limit dept . hyper paramete toking

61

Handling interactions

\- Aiributes are considered interacHng if they are able to dis3nguish between classes when used together, but individually they provide liile or no informa3on. - Due to the greedy nature of the spli:ng criteria in decision trees, such aiributes could be passed over in favor of other aiributes that are not as useful. This could result in more complex decision trees than necessary. - Decision trees can perform poorly when there are interac3ons among aiributes.

Neither X1 nor X2 provide any reduc3on in the X1 and X2 are interac3ng aiributes

impurity measure when used individually impurity4, similar n SolSO =\> cant do cause diagonal

only one attribute= So aly study has alld

to

stuly best

X2

X1

\+ : 1000 instances

o : 1000 instances

Considering X1\>= 10 as test condition: Entropy (X1) : 0.99

Considering X2\>= 10 as test condition: Entropy (X2) : 0.99

62

Handling interactions

\=Divided based on X2 ㅣ λ

ー ー / \_X2

·

ㆁ

ㆁ ㆀ

\*

63

Handling interactions given irrelevant attributes

Y

Never6for addcanreadest

\+ : 1000 instances

o : 1000 instances

Adding Z as a noisy attribute generated from a uniform distribution

Entropy (X) : 0.99 Entropy (Y) : 0.99 Entropy (Z) : 0.98

Attribute Z will be chosen for splitting\!

Not useful too ..

X

64

Limitations of single attribute-based decision boundaries

Both positive (+) and negative (o) classes generated from skewed Gaussians with centers at (8,8) and (12,12) respectively.

X2

\=\>DT Les big =\> If this was SVM , would

just be diagonal

\=\>Desicion bondy so complicated

X1

65

Decision Trees in SKLearn

66

Decision Trees in SKLearn

Three classes: \[Setosa, Versicolor, Virginica\]

Number of samples in each class

67

\= we

Decision Trees in SKLearn

Beware of overXOng\!\! Main parameters to tune (available in sklearn):

• max\_depth

• min\_samples\_split

• min\_samples\_leaf

• max\_leaf\_nodes

I-prevent

• min\_impurity\_decrease

• ccp\_alpha

68

\* knN for

regression Decision Trees for Regression

3nearest you found

neighbor yaud price ? estimate from Sapphe

Car Type

& tryng redictmone FamilyLuxury

Sports Predicted 113.125 Y

K C0: Income:

67.5 1 K C0: 8 71.875 C0: K 1

C0 . Average of customers’ incomes who have family =\>Split car

by variance (Standard deviation) ↳ If & not

homogenous

69

Income

608070906555607580 110 607080 120 160 130 100 90 100 95

How to select best split

Gender

Car Type

Variance of the target

Yes M F No FamilyLuxury variable (income): Sports

Variance for Males of (IncomeVariance\_incomes

Car\_V1 C0: 6 Male) C0: Car\_V2 Variance for 4

Females of incomes

(IncomeVariance\_Car\_V3

Female)

C0: 1 C0: 8 C0: 1

Weighted variance:

IncomeVarience\_Male +

70 10 ㄻ Lincome) + .Lincome mance ) vericmmake Senate

Car\_V1 + InformaHon Variance (parent) (Carvi) Gain:

\=\> - Weighted variance (Gender) + (carvi + Ʃ

8 (CarY) choose Variance wi 0 (parent) weighted - Smallest Weighted variance Vanange(Car)

anr

Less weighted variance (higher informa3on gain) in regression trees is equivalent to less

↑ Gain

impurity (more homogeneity among the samples within the nodes).

Will choose the split with the smallest weighted variance / higher Informa3on Gain

How to select best split- calculate

Gender

Car Type

Variance of the target

Yes M F No FamilyLuxury variable (income): Sports

Variance for Males of (IncomeVariance\_incomes

Car\_V1 C0: 6 Male) C0: Car\_V2 Variance for 4

Females of incomes

(IncomeVariance\_Car\_V3

Weighted variance:

IncomeVarience\_Male +

71 Female) for Variance incomes 여 C0: with people 1 family

Incondana C0: 8 Sporis C0: Inconvariance 1

Luxey

cars IncomeVariance famly

Car\_V1 +

\=\> minimizes is the one he variance

we chouse InformaHon Gain: Variance (parent) - Weighted variance (Gender) Variance (parent) - Weighted variance (Car)

Less weighted variance (higher informa3on gain) in regression trees is equivalent to less impurity (more homogeneity among the samples within the nodes).

Will choose the split with the smallest weighted variance / higher Informa3on Gain

Decision Trees for Regression in SKLearn

72

Didn'tDoEnsemble This(Stoppedpeso

Learning

Ensemble methods combine the predic3ons of several base es3mators built with a given learning algorithm in order to improve generalizability / robustness over a single es3mator.

Literature widely categorizes ensemble learning methods into two groups:

o Parallel methods train each base learner apart from the others of the others. o Sequential methods train a new base learner so that it

minimizes errors made by the previous model trained in the preceding step.

73

Ensemble Learning

74

Ensemble Learning- Parallel Methods

Parallel methods are further divided into:

o Homogenous methods  use the same base learning

algorithm to produce all of the component base learners.

o Heterogenous methods  use different algorithms to

produce base learners

75

Ensemble Learning- Parallel Methods

How do ensemble methods combine base learners into a final learner?

Majority voting is a common method for consolidating base learner predictions.

For instance, in a binary classification problem, majority voting takes predictions from each base classifier for a given data instance and uses the majority prediction as the end prediction (See next slide).

Weighted majority voting is an extension of this technique that gives greater weight to certain learner’s predictions over others.

76

Ensemble Learning- Parallel Methods

How the input to the base learners is formulated?

Majority vote

77

Ensemble Learning- Bagging

The idea behind bagging is combining the results of multiple models (for instance, all decision trees) to get a generalized result.

It is a parallel ensemble method.

Here’s a question: If you create all the models on the same set of data and combine it, will it be useful? There is a high chance that these models will give the same result since they are getting the same input.

So how can we solve this problem? One of the techniques is bootstrapping (or Bootstrap Aggregating).

78

Ensemble Learning- BaggingBootstrapping: is a sampling technique in which we create subsets of observations (bags) from the original dataset, with replacement. The size of the subsets is the less or the same as the size of the original set.

79

Ensemble Learning- Bagging

Given training set of size

For to : //where is the number of base learners

Use sampling with replacement to create a new training set of size

Train a decision tree on the new dataset

80

Ensemble Learning- Bagging in Scikit-Learnhips://scikit-learn.org/stable/modules/generated/sklearn.ensemble.BaggingClassi2er.html

hips://scikit-learn.org/stable/modules/generated/sklearn.ensemble.BaggingRegressor.html

81

Ensemble Learning- Random Forest

Random forest is an extension of bagging. It iteratively samples random subsets of features to create a decision node.

At each node, when choosing a feature to use to split, if features are availabe, pick a random subset of features and allow the algorithm to only choose from that subset of features. For large

82

Ensemble Learning- Random Forest

Bootstrapped features

83

Ensemble Learning- Random Forest in Scikit-Learn

84

hips://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassi2er.html

hips://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassi2er.html

Ensemble Learning- Boosting

Boos3ng is a sequential ensemble method.

Given training set of size For to : //where is the number of base learners  Use sampling to create a new training set of size  But instead of picking from all examples with equal

probability, make it more likely to pick misclassi2ed examples from previously trained trees //causing the learner

to priori3ze the misclassi2ed samples from the previous learner  Train a decision tree on the new dataset

 Example: Adaptive boosting (AdaBoost)

85
