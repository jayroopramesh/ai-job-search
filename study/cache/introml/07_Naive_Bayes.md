# IntroML (CMP 466) — 07 Naive Bayes
> Source: Google Drive file 1Zqc6sYeUvdEqgkx7X-2KkeqwW6QylLPD · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466- Machine Learning and Data Mining Chapter 4- Classification: Alternative Techniques

\=\> probabiliy Naïve Bayes

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

• Bayes Theorem

• Using Bayes Theorem for Classification

• Naïve Bayes Classifiers

• Naïve Bayes in SKLearn\!

2

Example 1

Text Learning

Using three words for simplicity

Adam Lena

10% 80% 10% 50% 20% 30%

Love Deal Life Love Deal Life

Email with contents:

Assuming equal probability: P(Adam) = 0.5 P(Lena) = 0.5 Love\!

Whom do you think would be the sender of the email?

Lena\! → because Lena has higher probability of using the word Love than Adam.

3

↳ like

email

iS eitner from adam or

lena =\> Both can send email

Example 2

Text Learning

Using three words for simplicity

Adam Lena

10% 80% 10% 50% 20% 30%

Love Deal Life Love Deal Life

Email with contents:

Assuming equal probability: P(Adam) = 0.5 P(Lena) = 0.5 Love Life\!

Whom do you think would be the sender of the email?

Lena\! → because Lena has higher probability of using the word Love and the word Life than Adam.

4

Example 3

Text Learning

Using three words for simplicity Adam Lena

10% 80% 10% 50% 20% 30%

Email with contents:

Love Deal Life Love Deal Life Life Deal\!

Whom do you think would be the sender of the email? Adam\!

P(Adam is sender of “Life Deal”) = 0.5 × 0.1 × 0.8 = 0.04 P(Lena is sender of “Life Deal”) = 0.5 × 0.3 × 0.2 = 0.03

Posterior with normalization P(Adam is sender | “Life Deal”) = 0.04/(0.04 + 0.03) = 0.57 P(Lena is sender | “Life Deal”) = 0.03/(0.04 + 0.03) = 0.43

\+ = 1

5 Assuming equal probability:

^ since (life and deal)

&

P(Adam) = 0.5 P(Lena) = 0.5

↳ Probability P(“Life they Deal”)

are -\> sender

can be sent by Bom so prob 어 saying it

Example 4

Text Learning

Using three words for simplicity Adam Lena

10% 80% 10% 50% 20% 30%

Email with contents: Love Deal\!

Love Deal Life Love Deal Life

Whom do you think would be the sender of the email?

Assuming equal probability: Let’s find out\!

P(Adam) = 0.5 P(Lena) = 0.5 P(Adam is sender of “Love Deal”) = 0.5 × 0.1 × 0.8 = 0.04 P(Lena is sender of “Love Deal”) = 0.5 × 0.5 × 0.2 = 0.05

The result is affected by: - Contents of email?

Posterior with normalization P(Adam is sender| “Love Deal”) = 0.04/(0.04 + 0.05) = 0.444 P(Lena is sender| “Love Deal”) = 0.05/(0.04 + 0.05) = 0.555

\+ = 1

YES - Length of email? YES - Order of words? So it is Lena\!

NO (commutative property\!)

6

\_=\>help \_ with Prediction

2 words=\&content

& = Doesn't

matter

Bayes Theorem

• Conditional Probability:

\_ P(Y | X) = y given X P (X ∩ Y) -\> / P(X)

intersection between tem

P(X | Y) = P (X ∩ Y) / P(Y)

\->given X

↳ X given y

\->given Y

• Bayes theorem:

p

\= P(xny) 1

XYP α )|( =

YPYXP )()|( )( y givery \~ XP

\- given ×P(. ( Y )

X P(Y)

7

X Y

P (X ∩ Y)

P (X ∩ Y) = P(X | Y) . P(Y) P (X ∩ Y) = P(Y | X) . P(X)

Example of Bayes Theorem

→ PCsl µ) =0

. s

Given:

◦A doctor knows that meningitis causes stiff neck 50% of the time

◦Prior probability of any patient having meningitis is 1/50,000

◦Prior probability of any patient having stiff neck is 1/20

\->n o somptarsp(M)S) = =↳ wit Symptoms P(SIM) S) =0-S \_ ( If a patient has stiff neck, what is the probability he/she has meningitis? Trying to find P(M | S)

P(M) = 1 / 50,000

P(S) = 1 / 20

P(S |M) = 50%

P(M)

SMP

)|( = MPMSP )()|( SP

)(

\= 50000/15.0 × 20/1

\= 0002.0 1//50,000) Y 20

\=0.0002

8

Using Bayes Theorem for Classification

eX

O nclassy given Can we estimate P(Y| X1, X2,…, Xd ) directly from data?

those features

9

Given a record with attributes (X1, X2,…, Xd)

◦ Goal is to predict class Y

◦ Specifically, we want to find the value of Y that maximizes P(Y| X1, X2,…, Xd )

Bayes Classifier is a probabilistic framework for solving classification problems

Consider each attribute and class label as random variables

Using Bayes Theorem for Classification

Approach:

◦ Compute theorem

posterior probability P(Y | X1, X2, …, Xd) using the Bayes

P (Y | X) =

◦ Maximum a-posteriori: Choose Y that maximizes

P(Y | X1, X2, …, Xd)

◦ Equivalent to choosing value of Y that maximizes

P(X1, X2, …, Xd|Y) P(Y)

σ

class-stays same the

intersection

XXXYP |( \_21

 n ) =

YPYXXXP ( 21 XXXP

( ↳ records  d )()| 21



d ) Proboj -given

X

How to estimate P(X1, X2, …, Xd | Y )?

10

Using Bayes Theorem for Classification

Train your classifier with this a

dataset: class ID Home

Owner

\->3 features

Marital Status

Income Annual

Evade

Given a Test Record:

1 Yes Single 125K No

ð = (Home \_ Owner = No, Divorced, ー

Income = 120K)

2 No Married 100K No

3 No Single 70K No

What is the probability that this X will evade?

4 Yes Married 120K No

5 No Divorced 95K Yes

6 No Married 60K No

7 Yes Divorced 220K No

8 No Single 85K Yes

9 No Married 75K No

10 No Single 90K Yes

10

11

We need to estimate

P(Evade = Yes | X) and P(Evade = No | X)

For easiness, from now on, we will replace

“Evade = Yes” by Yes “Evade= No” by No

p(yes(x) Example Data

\= P(y(yes)p(yes)\_PCX)

Given a Test Record:

PCNOL )= PCX

P (X) ð = (Home Owner = No, Divorced, Income = 120K)

ID Home Owner

Marital

Annual Status

Income Evade

1 Yes Single 125K No

2 No Married 100K No

3 No Single 70K No 4 Yes 5 No Married Divorced 00 120K 95K No

Yes

6 No Married 60K No

p(yes(X) = Pestimate -31109

compare -easy Eo

7 Yes Divorced 220K No 8 No Single 85K ㆁYes

can ignore 9 No Married 75K No 10 No Single 90K ㆁ Yes

10

P(Yes) P(NOS

\=3110

\= 7/10

12

P(x(yes) & P(XINOS

\->if dependent

can't multiply Assume ◦ P(X |Y∞

j) independence = among P(X1, X2, …, Xd |Yj) attributes Xi when class = P(X1| Yjㆁ ) . P(X2| Yj) ㆀ

. … is given: . P(Xd| Yj)

sia & =\> result Dependent

y

\-> multiplication

Conditional Independence

\=\> Bus ◦ can't multiply Now the Entraining we mealssameaecan data

estimate ependent P(X-s i| Xd Yj) multiply for all Xi and X1 X2 X3 X4

... \* dependenly If have

Yj combinations drop featurefrom

one

of

use omer aly.

◦ New point is classified to Yj if P(Yj) Π P(Xi| Yj) is maximal.

13

Naïve Bayes Classifier

Classifier based on the Bayes Theorem

Conditional Independence

• X and Y are conditionally independent given Z if P(X|YZ) = P(X|Z)

\-> independent

• Example: Reading skills and arm length –Young child has shorter arm length and limited reading skills,

compared to adults –If age is fixed, no apparent relationship between arm length and

reading skills –Reading skills (X) and arm length (Y) and are conditionally

independent given age (Z)

14

Naïve Bayes on Example Data

P(

Note : Nyes P\* ) p(yes) +

Given a Test Record:

P(XINO) P(NO

ð = (Home Owner = No, Divorced, Income = 120K)

ID Home Owner

Marital Status

Income Annual

Evade

1 Yes Single 125K No 2 ㆁ No Married 100K ㆁ

No 3 ㆁ No Single 70K ㆁNo 4 5 Yes No σ Married Divorced o 120K 95K · No

ㆁ

Yes

6 No Married 60K No 7 Yes 8 ㆁ No σ Divorced Single 220K ㆁ No

85K ㆁ

Yes

(승) classes 9 ㆁ No Married 75K ㆁ

No

10 No Single 90K Yes

10

categorical attributes

continuous attribute

P(X | Yes) = P(Home Owner = No | Yes) . P(Divorced | Yes) . P(Income = 120K | Yes)

P(X | No) = P(Home Owner = No | No) . P(Divorced | No) . P(Income = 120K | No)

P(Yes)

P(No)

15

Estimate Probabilities from Data

• For Classes:

ID Home Owner

e.g., P(No) = 7/10, P(Yes) = 3/10

• For categorical attributes:

P(Xi =c| y) = nc/n

– having where attribute |Xi=c| is number value belonging to class y

of instances Xi = c and

– Examples:

P(Status = Married|No) = 4/7 P(Home Owner = Yes|Yes)=0/3 = 0

16 Marital Status

Income Annual

Evade

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

ㆁ ㆁ ㆁ& ㆁ ㆁ &

↳ \# of attbelonging Xi =C to

σ ㆁ ㆁ ←cluss ∞ ㆁ& 시키 & ·

Estimate Probabilities from Data

ð = (Home Owner = No, Divorced, Income = 120K)

ID Home Owner eitrediscretize Given a Test Record:

orProbability densits

estimation

41 ㅋ ㆁ ㆁ ㆁ ㆁ 8 σ σ ㆁ ㆁ · ㆁ o P(Home P(Home owner =No/NO) owener =Nolyes) G 313 그 P(Divorced /NO) = ㄻ ㆁ ㆁ PLDivorced(yes) = 1/3 ㆁ σ

Marital Status

Income Annual

Evade

Estimate probabilities for classes

1 Yes Single 125K No

P(Yes) = 3/10 2 No Married 100K No

P(No) = 7/10 3 No Single 70K No

4 Yes Married 120K No

5 No Divorced 95K Yes

6 No Married 60K No

7 Yes Divorced 220K No

8 No Single 85K Yes

9 No Married 75K No

10 No Single 90K Yes

10

17

Estimate Probabilities from Data

Given a Test Record:

ð = (Home Owner = No, Divorced, Income = 120K)

ID Home Owner

Marital Status

Income Annual

Evade

Estimate probabilities for categorical attributes 1 Yes Single 125K No

P(Home Owner = No | No) = 4/7

2 No Married 100K No

P(Home Owner = No | Yes) = 1

3 No Single 70K No

P(Marital Status = Divorced | No) = 1/7 4 Yes Married 120K No

P(Marital Status = Divorced | Yes) = 1/3

5 No Divorced 95K Yes

Other calculations: 6 No Married 60K No

P(Home Owner = Yes | No) = 3/7

7 Yes Divorced 220K No

P(Home Owner = Yes | Yes) = 0/3

8 No Single 85K Yes

P(Marital Status = Single | No) = 2/7

9 No Married 75K No

P(Marital Status = Married | No) = 4/7

10 No Single 90K Yes

10

P(Marital Status = Single | Yes) = 2/3 P(Marital Status = Married | Yes) = 0

18

Estimate Probabilities from DataFor continuous attributes: – Discretization: ◆ Replace ◦ – Probability Attribute continuous density changed Partition value from estimation: with continuous the bin value

range to ordinal

into \*bins: ◆ Assume attribute follows a normal distribution ◆ Use data to estimate parameters of distribution value close

(e.g., ー

mean and standard deviation) to mean ◆ Once probability distribution is known, use it to estimate the \> farafon mean Height Lfala namal usualy as conditional distribution one income close probability must to distribution

mean P(Xi|Y)

follow normal

\=\> usually does

19

Estimate ID Home

Owner

Marital Status

continuous Gaussian/Normal YXP )|( i for each For (Income, –If Class=No

j (Xprobabilities = i , attributes Yi) Class=No): 2pair. πσ 1 distribution:

ㆁ ij 2 -\> e - - (

for variance X I using - i2 - Obbaheσμ

ij2 Variance ij ) 2

population far each class

value 9

◆ sample mean (µ) = 110 ◆ sample variance (σ2) = = 2975

an

population

for that class vahe-\> -\> mean12S + 100 +220 +70 セ +120 AS +66 ⇌

\= )54.54(2

l 0

σ → raas Income Annual

Evade

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

P (

Income =

)|120 No = 1 π

e -120( )2975(2

\- )110 2

\= 0072.0 20

Estimate Probabilities from Data

Estimate Probabilities from Data

Given a Test Record:

ð = (Home Owner = No, Divorced, Income = 120K)

ID Home Owner

Marital Status

Income Annual

Evade

Estimate probabilities for continuous attributes 1 Yes Single 125K No

2 No Married 100K No

For Taxable Income:

3 No Single 70K No

4 Yes Married 120K No

If class = No

sample mean = 110 5 No Divorced 95K Yes

sample variance = 2975 6 No Married 60K No

7 Yes Divorced 220K No

8 No Single 85K Yes

If class = Yes

sample mean = ㆁ90

9 No Married 75K No

sample variance = ·

25

10 No Single 90K Yes

10

21

Estimate Probabilities from Data

Given a Test Record:

ð = (Home Owner = No, Divorced, Income = 120K) Putting it all together

ID Home Owner

Marital Status

Income Annual

Evade

1 Yes Single 125K No

2 No Married 100K No

3 No Single 70K No

4 Yes Married 120K No

5 No Divorced 95K Yes

6 No Married 60K No

7 Yes Divorced 220K No

8 No Single 85K Yes

9 No Married 75K No

10 No Single 90K Yes 10 σ P(NO(X) 2 Plyes/

x)

P(X | Yes) = P(Home Owner=No | Yes) × P(Divorced | Yes) × P(Income=120K | Yes) = 1 × 1/3 × 1.2 × 10-9 = 4 × 10-10

❑ P(X|No). P(No) = 0.0006 × 7/10 = 4.1× 10-4 ❑ P(X|Yes). P(Yes) = 4 × 10-10 × 3/10 = 1.2 × 10-10 Since P(X|No). P(No) \> P(X|Yes). P(Yes) Therefore P(No|X) \> P(Yes|X)

→ Class = No

P(X | No) = P(Home Owner=No | No)

× P(Divorced | No) × P(Income=120K | No) = 4/7 × 1/7 × 0.0072 = 0.0006

22

Estimate Probabilities from Data

All calculations:

misses incomeP(Yes) = 3/10

X = (Home Owner = No, Divorced) or X = (Divorced) Given the following Test Records: smisstertwo

P(No) = 7/10

P(Home Owner = Yes | No) = 3/7

P(Yes | Home Owner = No, Divorced) P(Home Owner = No | No) = 4/7 P(Home Owner = Yes | Yes) = 0

\= P(Home Owner=No | Yes) P(X)

P(Divorced | Yes) P(Yes)

P(Home Owner = No | Yes) = 1

P(Marital Status = Single | No) = 2/7 P(Marital Status = Divorced | No) = 1/7

\= 1 1/3 P(X) 3/10

\= P(X) 1/10

\= P(X)

0.1

P(No | Home Owner = No, Divorced)

P(Marital Status = Married | No) = 4/7 P(Marital Status = Single | Yes) = 2/3

\= P(Home Owner=No | No) P(Divorced | No) P(X)

based

calcs on available - → data

P(No)

P(Marital Status = Divorced | Yes) = 1/3 P(Marital Status = Married | Yes) = 0

\= 4/7 P(X) 1/7 7/10

\= P(X) 4/70

\= 0.057 P(X) → Predicted class: Yes For Taxable Income: If class = No: sample mean = 110

P(Yes | Divorced) = P(Divorced | Yes) P(X) P(Yes)

\= 1/3 P(X) 3/10

\= P(X)

0.1

sample variance = 2975 If class = Yes: sample mean = 90

sample variance = 25

P(No | Divorced) = P(Divorced | No) P(X) P(No)

\= 1/7 P(X) 7/10

\= P(X) 0.1

→ Same value, can’t

tell ☹ This classifier ignores missing data\!

23

Issues with Naïve Bayes Classifier

All calculations: P(Yes) = 3/10 P(No) = 7/10

P(Home Owner = Yes | No) = 3/7 P(Home Owner = No | No) = 4/7 P(Home Owner = Yes | Yes) = 0 P(Home Owner = No | Yes) = 1

P(Marital Status = Single | No) = 2/7 P(Marital Status = Divorced | No) = 1/7 P(Marital Status = Married | No) = 4/7

If one of the conditional probabilities is zero, P(Marital Status = Single | Yes) = 2/3

then the entire expression becomes zero P(Marital Status = Divorced | Yes) = 1/3 P(Marital Status = Married | Yes) = 0

For Taxable Income: If class = No: sample mean = 110

sample variance = 2975 If class = Yes: sample mean = 90

sample variance = 25

Given a Test Record:

X = (Home Owner = No, Married, Income=120K)

P(Yes | X) = 1 x 0 x 1.2 × 10-9 × 3/10 /P(X) = 0 P(No | X) = 4/7 x 4/7 x 0.0072 x 7/10 /P(X) = ??

mting will always class

be no in this case

Since \> o

24

Issues with Naïve Bayes Classifier

Naïve Consider the table with Tid = 7 deleted

Bayes Classifier:

ID Home Owner

Marital

Annual Status

Income Evade

P(Home Owner = Yes | No) = 2/6 P(Home Owner = No | No) = 4/6 1 Yes Single 125K No

P(Home Owner = Yes | Yes) = 0

2 No Married 100K No

P(Home Owner = No | Yes) = 1 P(Marital Status = Single | No) = 2/6 3 No Single 70K No

P(Marital Status = Divorced | No) = 0

4 Yes Married 120K No

P(Marital Status = Married | No) = 4/6 P(Marital Status = Single | Yes) = 2/3 5 No Divorced 95K Yes

P(Marital Status = Divorced | Yes) = 1/3

6 No Married 60K No

P(Marital Status = Married | Yes) = 0/3 For Taxable Income: 7 Yes Divorced 220K No

8 No Single 85K Yes

If class = No: sample mean = 91

sample variance = 685 If class = Yes: sample mean = 90 9 No Married 75K No

sample variance = 25

10 No Single 90K Yes

10

Given X = (Refund = Yes, Divorced, 120K) P(X | No) = 2/6 X 0 X 0.0083 = 0 P(X | Yes) = 0 X 1/3 X 1.2 X 10-9 = 0

In this case, Naïve Bayes will not be able to classify X as Yes or No because both probabilities are 0.

This also applies when the resulting probabilities are the same.

25

Issues with Naïve Bayes ClassifierIf one of the conditional probabilities is zero, then the

entire expression becomes zero

Need to use other estimates of conditional probabilities than simple fractions

p(married(yess Probability estimation:

을 강

n: number of training instances belonging to class y a

nc cand : number Y = y

of instances with Xi =

v: total number of attribute values that Xi can take

·O Total \# I original: ð ð = ð ð¦) = ð ð Laplace Estimate: ð ð = ð ð¦) = ð ð + + ð£ 1

p: initial estimate of m − estimate: ð ð = ð ð¦) = ð ð + + ðð

ð

attr

(P(Xi = c|y) known apriori m: hyper-parameter for our confidence in p values that X can

take , ex . married , single , divorced V=3 26

Example of Naïve Bayes Classifier

Name Give Birth Can Fly Live in Water Have Legs Class human yes no no yes mammals python no no no no non-mammals salmon no no yes no non-mammals whale yes no yes no mammals frog no no sometimes yes non-mammals komodo no no no yes non-mammals bat yes yes no yes mammals pigeon no yes no yes non-mammals cat yes no no yes mammals leopard shark yes no yes no non-mammals turtle no no sometimes yes non-mammals penguin no no sometimes yes non-mammals porcupine yes no no yes mammals eel no no yes no non-mammals salamander no no sometimes yes non-mammals gila monster no no no yes non-mammals platypus no no no yes mammals owl no yes no yes non-mammals dolphin yes no yes no mammals eagle no yes no yes non-mammals

Give Birth Can Fly Live in Water Have Legs Class yes no yes no ?

A: attributes

M: mammals

N: non-mammals

MAP

)|(

\=76 × 76

× 72

× 72 = 06.0 NAP

)|(

\=

131 × 10

13× 133

× 134 = 0042.0 MPMAP

06.0)()|(

\= × 207 = 021.0 NPNAP

004.0)()|(

\= × 13 20= 0027.0 P(A|M)P(M) \> P(A|N)P(N)

→ Class = Mammals

27

Naïve Bayes Classifier

Naïve Bayes Classifier in SciKit-learn:

https://scikit-learn.org/stable/modules/naive\_bayes.html

28

Naïve Bayes classification Example in Python\!

Naïve Bayes Classifier

Red points are of class 1, while blue points are of class 2

29

Naïve Bayes (Summary)

Strengths:

• Easy to implement

• Simple to run and efficient

• Great for text (better than SVM in this particular problem)

• Deals with big feature spaces 20 to 200 K language text

• Handle missing values by ignoring the instance during probability estimate calculations

• Robust to isolated noise points and irrelevant attributes (these will have low probability)\!

30

Naïve Bayes (Summary)

Weaknesses:

• Assumes conditional independence which may not hold for some attributes.

• Redundant and correlated attributes will violate class conditional assumption

• Can break, not good for phrases. “AUS student” is being treated similarly as “AUS” and “Student” separately.

• Other Bayesian techniques can handle this such as Bayesian Belief Networks (BBN)

31

Naïve Bayes (Summary)

How does Naïve Bayes perform on the following dataset?

Conditional independence of attributes is violated

32

Learning Outcomes

1\. Perform machine learning steps including data preparation, task identification, model selection, and evaluation. 2. Employ mathematical methods to explain the theoretical aspect of machine learning and data mining techniques.

3\. Select appropriate supervised learning methods including classification and regression for given problems and datasets.

4\. Use unsupervised learning methods such as clustering and association rule mining to discover patterns and relationships in datasets. 5. Apply feature selection and dimensionality reduction methods. 6. Use 
