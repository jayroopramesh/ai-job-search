# IntroML (CMP 466) — 08 Regression I
> Source: Google Drive file 1CS6iuzKgr_YtdKyC_xtox41RxUhUTT-l · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466 Machine Learning and Data Mining

↑ supervised

1

Predict Continuous

output Supervised Learning- Regression I

↳Basicunode

Salam Dhou, PhD Computer Science and Engineering American University of Sharjah

1

Outline

• Regression concept

• Regression vs. Classification

• Linear Regression

• Non-Linear Regression

• Multiple and Multi-variate Regression

• Regression in SKLearn\!

2

Regression vs. Classification

Common things: Regression and classification are both supervised learning methods

Difference In regression, output is continuous (number) In classification, output is discrete (class labels)

3

Regression is Supervised

(same

dassification) as Training Set

Learning Algorithm

result-trained model Age (ð¥) O

ℎ or Estimated

hypotresis net worth ℎ: hypothesis

4 ℎ maps from ð¥’s to ð¦’s.

(ð¦)

Univariate Linear Regression

Example Estimating the net worth of people based on their age. One feature x = Age, output y = Net worth

↳ input 4 output

Net worth

ofold, mich

요Age young, poo

5

Univariate Linear Regression

Example

linequation

\= Estimating the net worth of people based on their age.

Y = mx + b

One feature x = Age, output y = Net worth Hypothesis: Net worth

Univariate linear regression is linear regression with one variable.

6 ℎ ð¥ = 0Oð¤ ^+ ð¤ -\>↳ ð¥ wantfind line Parameters: fits data,

ð¤ ,ð¤

ð¤ + ð¤ ð¥

capture trend어 data -\>slope ω wo t -b -\>m ㆁ ↳ y-intercept Age

←α×

\_

on Univariate Linear Regression

findL \#Here

we line

know

line to

parameters

뷰

fusingI need\!order to the

O↳ x = =0, 4.0 ( in Bot ¤

hypotnesis d ↳eslope

Y-intercept

7

→

equation getting In ML

Example

\#need point

one ↳wewanteen

How do we estimate ð¤ and ð¤ ?

500

0

0 80

Line Equation: ℎ ð¥ = ð¤ + ð¤ ð¥,

where ð¤ is slope, and ð¤ is the y-

Net worth

intercept (value of y when x = 0) From one point on the line

ð¦ = 0 + age

Age

Or it can be represented by ℎ ð¥ = ð¤ + ð¤ ð¥ so ℎ ð¥ = 0 + ð¥

Univariate Linear Regression

Example Using this model, predict the net worth of a person of age of'\*

36 in put na(b6) = (36)

\= 22S

500

0

0 36 80

8 By substituting in the equation: Net worth

ℎ ð¥ = 0 + 36 = 225

Age

Univariate Linear Regression

Find ð¤ and ð¤ for each of the following lines, given the hypothesis ℎ ð¥ = ð¤ + ð¤ ð¥

wo = 1

slope = o

Y-intercept

\= I. S wo = 0 W , = Y 2 = 0

. s9 w , = 0

. S cnot dear hesb) 3

3

3

ℎ ð¥ = 1 + 0.5ð¥

21ℎ ð¥ = 1.5 + 0ð¥

21F

ℎ ð¥ = 0.5ð¥

2- 10 1 2 3 0 1 2 3 0

1 2 3 ð¤ = 1.5

ð¤ = 0

ð¤ = 0 ð¤ = 0.5

ð¤ = 1 ð¤ = 0.5

Estimating ð¤ and ð¤

Example If you want to draw a line representing the data, which line of the following is the best?

Answer is Line B

Idea: Choose ð¤ , ð¤ so that ℎ ð¥ is the closest to ð¦ for your training examples (ð¥, ð¦)

Net worth

· A

near andend

ning diver ges B C Es Choose me line

closes ∞ wraining

minimizes

Age

10 example

the overall distance to all

the points

Regression Regression Example

Error

5tryinbest

tofodoption ↳ Given with all a find and X\&y dataset

need best values

to

line

↳ inimites

error

Finding a regression line is an optimization problem. The best line is the one that minimizes the distance (error) between the predicted output (regression line) and actual output of the training data points.

Best lie

↳ line that minimizes Net worth

difference and error Predicted real or rahe between value

minimizes the errors errorps

thselgo-- ℃ ←ㅣ

Age

Distance Between point

line

Smnaller the dils =\> Bette

11 Net worth

Age

Regression Error

The error/residual is the difference between actual net worth and the predicted net worth by the model (regression line).

Net worth

For age = 35, predicted net worth is 218.75. Assume actual net worth = 200.

error

predicted actual value value

Age

Error for this sample = 200- 218.75 = -18.75.

12

Minimizing Regression Error

↳ for all points

The best line is the one that minimizes ∑(ððððð)ðon all samples

∑ ððððððððð − ðððððð %ð ↳ for find all samples squared (training errar

data points).

Net worth

why and squared

not sum and of squared error absoluerawe ?? =\> sse o

551\]

error

predicted actual value value

Age

13

\#Square magnifies era Why Sum of Squared Error (SSE)?

euror larger

so

penelizes

There can be multiple minimize ∑(ððððð)ð \!

lines that minimize ∑|ððððð|, but only one -enosuesectilline eeewill all tdata

Using ∑|ððððð| and considering two points:

For For the the blue orange regression regression line: line: ∑|ððððð| ∑|ððððð| = = |1| |2| + + |-3| |-2| = = 4. 4.

Ye

Same

Net worth

Using ∑(ððððð)ð:

blue regression line: ∑(ððððð)ð= 1 + 9 = 10. error = 1

ㆁorange regression line:∑(ððððð)ð= 4 + 4 = 8.

error = 3 ㅇ

error = 2

The orange line minimized the ∑(ððððð)ð \!

Age

14

Sum of Squared Error (SSE)

Sum of Squared Error (SSE) :∑(ððððð)ð is not perfect:

Net worth

Net worth

\# More samples penelizes

the even

line mough more

same line ↳ so normalize

Age

Age

The more data samples you have, the larger the SSE\! Which means a worse fit. What do we need to solve this?

Normalize to get the Mean Squared Error (MSE) MSE = ㆁðð∑(ððððð)ð d\# & samples

15

Learning Choose ð¤ , ð¤ that Algorithm

minimizes the error

→ finding that me minimizes

line MSE

∑(ððððð)

∑ ððððððð¡ðð − ððð¡ð¢ðð ∑ (ℎ ð¥( ) − ð¦ O)

multipleefor all the predicted output

actual output

ponse from - pant

Thus, a cost/ loss function is the Sum of Squared Error Function: ð½ ð¤ ,ð¤ = ㆁ∑ (ℎ ð¥( ) − ð¦ )

dwillb derived so 2 goes awaylase Best line one - that cost/loss

the

minimizes

16

Learning Algorithm

Hypothesis: ℎ ð¥ = · ð¤ + ㆁð¤ ð¥ -\> line equation Parameters:

U-\> parameters ð¤ ,ð¤ Cost Function (Squared Mean

Error Function):

\->Drawn like the U

ð½ ð¤ ,ð¤ = ∑ (ℎ ð¥( ) − ð¦ )

Shape

Goal:

\-> in regression , to find min ð½ ð¤ ,ð¤

line that minimizes

cost

or parameters that minimizers

he line

17

Gradient Descent

\->Optim algorithm

ization

\-> we want to get wo

, we for o Gradient Descent is an optimization algorithm the used best in line training that minimizes

a

cost

machine learning model to find the values of a function's parameters (coefficients) that minimize a cost function as far as possible.

o It is used to find a local minimum of a differentiable function.

o The algorithm start with initial parameter’s values and it

iteratively adjusts the values so they minimize the given cost function.

\* The alg is used to find

the values of the parameters, wo 5W1 for the

mmmm best line

18

Gradient Descent -\> square functionHave some function ð½ ð¤ ,ð¤

Want to min ð½ ð¤ ,ð¤ \~Outline: to how know α ∞ &

0

• • Start Keep with changing some ð¤ ð¤ ,ð¤ ,ð¤

to reduce ð½ the we ð¤ derivitive ,ð¤

are tangent, here of want ? J until we hopefully end up at a minimum

wo makes Minimum

\= 0.

to know or

ot that minimum

Irat 19

\* Gradient Descent

more attributes

\-> more coef. ↳ Butbe Ken able to wantVisualize Lets plot the cost function ð½ ð¤ ,ð¤ → it is a quadratic function so it will look somehow similar to the one below.

ein 3D·ð½ ð¤ ,ð¤

\->lookS

like convex ð½(ð¤ )

Here is the minimum

3D

· ð¤

ㆁ ð¤

α simplicity for

ㆁ Here is the minimum ð¤ this for

onlyoneattribute 20

Gradient Descent

Lets plot the cost function ð½ ð¤ ,ð¤ → it is a quadratic function so it will look somehow similar to the one below.

For simplicity, let’s consider one variable, e.g., ð¤

Where is the minimum of this function?

How can we find the value of ð¤ this point?

It is the point is at slope 0.

How to find the slope at

ð½(ð¤ ) any point of the curve? By taking the derivative at any ð¤

Here is the minimum

ð¤ 21

Gradient Descent

ð½(ð¤ )

4 6

22

How to find min w1? 1) start with random

W

\-> Takederivitive어 function - \> \> -Mir tve

then Point

our

to

left to So Subtract move to left

• The gradient is the slope of a function. ㆁ

positive slope

• The higher the gradient, the steeper the slope and the faster a model can learn.

• But if the gradient is zero, the model stops learning.

• In mathematical terms, a gradient is a partial derivative

·

with respect to its inputs.

ð¤

Gradient Descent

\-> Take 여 denivite

Skope

negative

\=

\-ve

slope

means

ð½(ð¤ )

min Point to

right So

a wt and so

O 2

4

23 ð¤

on

Ex Gradient Descent

\-> error = o Repeat until convergence {

ð¤ ≔ ð¤ − ð¼ Ej ð½(ð¤ Derivative ,ð¤ ) OfCost function (for ð whatever } u are trying oLearning rate derivative

w = = wa-slope incase Optimize slope-veadd Slope - the minus

ㅣ ωI = 2

: Slope = -2 , α=マ

w1 = W1 - X Slope

wk = w1

\- (

\- 2)

wa = 2 - (-2)

\= 4 → \_

Slope = -3 ー E Slope

wI w = = = 5

S - (+2)

ω I = 3ω 1 = 3 - (- J) … = 0 and ð = 1) stepstsLnot sowe sesmaller \*to more overshoot slope ba multiply

Mis .

by that \< clearning rase

more right

\-more left

24

Gradient Descent – learning rate

ð¤ ≔ ð¤ − ð¼ ð½(ð¤ )

If ð¼ is too small, gradient descent can be slow

↳gaurantee

ð½(ð¤ ) reaching

min,mum e ð¤

25

Gradient Descent – learning rate

ð¤ ≔ ð¤ − ð¼ ð½(ð¤ )

If ð¼ is too large, gradient descent can overshoot the minimum. It may fail to converge, or even diverge.ð½(ð¤ )

26

ð¤

Gradient Descent – learning rate

What if the learning rate (ð¼) is 0? → ð¤ ≔ ð¤ − 0 . ð½(ð¤ ,ð¤ )

→ ð¤ ≔ ð¤ → ð¤ will not change → model will not learn

What if it is 1? → ð¤ ≔ ð¤ − 1 . ð½(ð¤ ,ð¤ )

→ You will each time subtract a large value (positive/negative), can overshoot the minimum. It may fail to converge, or even diverge.

27 ð½(ð¤ )

ð¤

Gradient Descent – learning rate

Repeat until convergence {

Given the loss function:

}

ð¤ for ㅇ≔ each ð¤ − ð¼ coef

ðð¤ ðð½(ð¤ ,ð¤ )

ð½ ð¤ ,ð¤ = 2ð 1(ℎ ð¥( ) − ð¦ )

For each once of ð¤ for and wo ð¤ , oncefo,

ut

Repeat until convergence {

The derivatives with respect to each of ð¤ and ð¤ are:

ð¤ ≔ ð¤ − ð¼ ðð¤ ðð½(ð¤ ,ð¤ )

ððð¤ 28 -\>ð½ multiplied ð¤ ,ð¤ by nothing

\= ð 1(ℎ ð¥( ) − ð¦ )

}

ð¤ ≔ ð¤ − ð¼ ðð¤ ðð½(ð¤ ,ð¤ )

ððð¤ ð½ ð¤ ,ð¤ = ð 1(ℎ ð¥( ) − ð¦ ) ð¥( )

\->multiplied by X

anGradient Descent

wr

Example Estimating the net worth of people One feature x = Age, output y = Net based worth

on their age.

eslope

\= c

\* at ileration Iteration 1 serror 2 error ien t lowe iter

z

wo, wa - where Valuejost min

\=

Net worth

Best fit line

→ almostminimizing

mere 9JesubrachtIteration ,

2 -\> tries Iteration 1 ⑪ Iteration 3

to move

right value

Age

↳ random, doesnt Captire

rend 29

Ordinary Least Squares (OLS)

Ordinary Least Squares (OLS) provides a closed form solution to a simple linear regression problem, i.e., a problem with only one feature.

With OLS, the aim is to calculate the values ð¤ and ð¤ in the equation of a line to find the line of best fit for n points: ℎ ð¥ = ð¤ + ð¤ ð¥

Calculate =\> slope

w\] \# oJ samples woð¤ θ

\= ð ㄱ ð∑ ∑(ð¥ð¦) -ð¥ traning -\> data Sum → than no square -\>

− ∑(ð¥)∑(ð¦)

− (∑ð¥) o Calculate y-intercept

↳ squarex, tren Optimization ð¤ = ∑(ð¦) O − ð ð¤ ∑(ð¥)

o Assemble the equation of a line

Sum

of samples

ℎ ð¥ = ð¤ + ð¤ ð¥

30

Ordinary Least Squares (OLS)

h(w) = 1

. 518 X + 0

. 30s

ω I = 5(233)

\- (25)(41)

Example: Ordinary Least Squares

ー3(68)

\- 676

Dataset showing the number of hours of sunshine vs the number of ice creams sold at the shop from Monday to Friday:

\=1

. s 183

ㅣ

"x"

@ ×)P= 676

Hours of Sunshine

wo' G)

\_ - = 3 1 .s2 (26) 5 ousy 慈 sum

"y" Ice Creams Sold 2 4 3 5 ”…5 7 9 7

3 S 10 킹 15

23 、 …

31

Ordinary Least Squares (OLS)

Example: Ordinary Least Squares

Step 1: For each (x,y) calculate x2 and xy:

x y x2 xy 2 4 4 8 3 5 9 15 5 7 25 35 7 10 49 70 9 15 81 135

Also n (number of data values) = 5

32

Ordinary Least Squares (OLS)

Example: Ordinary Least Squares

Step 2: Sum x, y, x2 and xy (gives us Σx, Σy, Σx2 and Σxy):

x y x2 xy 2 4 4 8 3 5 9 15 5 7 25 35 7 10 49 70 9 15 81 135 Σx: 26 Σy: 41 Σx2: 168 Σxy: 263

33

Ordinary Least Squares (OLS)

Example: Ordinary Least Squares

Step 3: Calculate Slope ð¤ :

ð¤ = ∑( ) ∑( ) ∑( ∑ (∑ ) )

\= ( )

ð¥ ð¦ ð¥2 ð¥ð¦ 2 4 4 8

\= = 1.5183

3 5 9 15 5 7 25 35 7 10 49 70 Step 4: Calculate Intercept ð¤ :

9 15 81 135 ð¤ = ∑( ) ∑( ) = . = 0.3049

Σð¥ = 26 Σð¦ = 41 Σx2 = 168 Σð¥ð¦= 263

34

Ordinary Least Squares (OLS)

Example: Ordinary Least Squares

Step 5: Assemble the equation of a line:

ℎ ð¥ = ð¤ + ð¤ ð¥

ð¥ ð¦ ð¦ = 0.305+ 1.518 ð¥ error

2 4 3.34 −0.66

ℎ ð¥ = 0.305 + 1.518 ð¥

3 5 4.86 −0.14 5 7 7.89 0.89 7 10 10.93 0.93

Done\!

9 15 13.97 −1.03

35

Ordinary Least Squares (OLS)

Example: Ordinary Least Squares

If the weather forecast says "we expect 8 hours of sun tomorrow", How many ice creams are predicted to be sold?

Using the line equation:

ð¥ ð¦ ð¦ = 0.305+ 1.518 ð¥ error ℎ ð¥ = 0.305+ 1.518 ð¥

2 4 3.34 −0.66 3 5 4.86 −0.14 -\> substitute 5 7 7.89 0.89 ⼊ o 7 10 10.93 0.93

9 15 13.97 −1.03 ↑ PredictSubstitute ð¥ with 8 ℎ ð¥ = 0.305+ 1.518 8 = ←12.45 Ice Creams Ice cream man should have at least 13 in his truck then\! Yum.

ー

36

Gradient Descent vs. OLS

Gradient Descent Ordinary Least Squares

• Need to choose ð¼.

• Needs many iterations.

• Works well even with very large number of features ≥ 1000

• No need to choose ð¼.

• Don’t need to iterate.

• Slow if the number of features is very large.

37

How 줍 BonR R-Squared ↳ Squared if to evaluate (R2) - regression Coefficient ↑

MAE of MSE determination

(mean Better

Absolute error

there is a correlation between two variables, R describes that

is an accuracy measure. It measures how much of any ^change -\> -ve correlation + 1 ð → Perfect = 1 in correlation −

the output is explained by the ððð¸ change in = input.

∑(ð s − actualð)↳ð 0-

no correlation

ððð¸ = ∑(ð − ð)ð

predicted actual -average Value of ð : 0.0 \< ð \< 1.0

where y is the actual value, ð is the predicted value,

\->

no correlation

ð is the mean y value.

0.0 means line is not doing a good job of capturing the trend in data.

{ on 1.0 input bemeans and theeve the line output.

does a good job \# of describing area of te house and correlation the have price relationship \* age between Price -ve the and of house

correlation

38

\# Linear ↳ trathis one createline-- Regression dats / -\>

wont no

perfectly

fitt 2 Sometimes data

acc doesnt

have trend

Which dataset

Net worth

Net worth makes a good linear Regression?

\_

α Age

Age

\_

\-perfect \_ √ Net worth

Net worth

Net worth

\->slope∝

ㆀ

not α

\-Good no wrend Age

Age

Age for same diff netwartn age

?

\-> cant relationship

find

39

Classification vs. Regression

Property Supervised Classification 
