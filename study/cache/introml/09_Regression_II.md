# IntroML (CMP 466) — 09 Regression II
> Source: Google Drive file 1jtVOLv3mp9bglsXTvQFyWw5PBvLUTwNw · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

CMP 466 Machine Learning and Data Mining

Supervised Learning- Regression II

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

Regression is Supervised

Training Set

Learning Algorithm

Age (ð¥) ℎ Estimated net worth ℎ: hypothesis

3 ℎ maps from ð¥’s to ð¦’s.

(ð¦)

Univariate Linear Regression

Recall: Hypothesis for ㆁunivariate (one variable) linear regression: ℎ ð¥ = ð¤ + ð¤ ð¥

Hypothesis for →multivariate (multiple variables) linear regression: ℎ ð¥ = ð¤ + 0 ð¤ ð¥ + ° ð¤ ð¥ + ㆀ

ð¤ ð¥ + ð¤ ð¥

Net worth

Age Highest level

Income … of education

Age

4

Univariate Linear Regression

Hypothesis for linear regression (one variable): ℎ ð¥ = ð¤ + ð¤ ð¥

Parameters: ð¤ ,ð¤

Cost Function (Squared Error Function):

ð½ ð¤ ,ð¤ = ∑ (ℎ ð¥( ) − ð¦ )

Goal:

min ð½ ð¤ ,ð¤

\-> Find min cost, so wod ω원 Gradient Descent:

tmar minimizes Repeat {

the error

ð¤ ≔ ð¤ − ð¼ ð½(ð¤ ,ð¤ )

}

5

Multivariate Linear Regression

Hypothesis for multivariate regression (multiple variables): ℎ ð¥ = ð¤ + ð¤ ð¥ + ð¤ ð¥ + ð¤ ð¥ + …+ ð¤ ð¥

Parameters: ð¤ ,ð¤ ,ð¤ ,⋯,ð¤

Cost function:

\-> find the

Parameters

that ð½ ð¤ ,ð¤ ,⋯,ð¤ = ∑ (ℎ ð¥( ) − ð¦ )

minimites Goal:

℃ error min … ð½ ð¤ ,ð¤ ,…,ð¤ Gradient Descent: Repeat { ð¤ ≔ ð¤ − ð¼ ð½(ð¤ ,ð¤ ,⋯,ð¤ )

}

6

Gradient Descent Multiple Variables

New algorithm (ð ≥ ð): Previously (ð = ð):

Repeat {

Repeat {

}

}

7 ð¤ ð¤ ≔ ð¤ − ð¼ ð 1(ℎ ð¥( ) − ð¦ )

≔ ð¤ − ð¼ ð 1(ℎ ð¥( ) − ð¦ )

ð¤ ≔ ð¤ − ð¼ ð 1(ℎ ð¥( ) − ð¦ ) ð¥( )

ð¤ ≔ ð¤ − ð¼ ð 1(ℎ ð¥( ) − ð¦ ) ð¥ ( )

….

\-> until slope of

botn =

ð¤ ≔ ð¤ − ð¼ ð 1(ℎ ð¥( ) − ð¦ ) ð¥ ( )

Gradient Descent – Feature Scaling ↳ need to do

fecture sceeling Get every feature into approximately a −3 ≤ ð¥ ≤ 3 range.

we cause

don't

to want dominate

one

0 ≤ ð¥ ≤ 3

Transforms data to have a mean of 0 and a standard deviation of 1.

−2 ≤ ð¥ ≤ 0.5

Shuge

Z = ð − ð

\-> Dominates

↳every ^neglected

small

8 μ

−100 ≤ ð¥ ≤ 100

−0.0001 ≤ ð¥ ≤ 0.0001

Gradient Descent – Debugging & Learning Rate

Gradient Descent:

ð¤ ≔ ð¤ − ð¼ ðð¤ ðð½(ð¤ ,ð¤ ,⋯,ð¤ )

• “Debugging”: How to make sure that gradient descent is working correctly.

• How to choose learning rate ð¼

9

Gradient Descent – Debugging & Learning Rate

\* purpose of -\> Decrease ang

cost

so cost when is conversee

minimized The cost function ð½ shoud decrease after every iteration.

Some applications can take 30 iterations. Others 3,000 iterations, and others 3,000,000 iterations.

Automatic convergence test:

Declare convergence if the cost function ð½ decreases by less than

10 ร ð½

cost =\> stop when pointsislesdiff in eold · convergesC-\>high when decrease and random

should until

d · 10 in one iteration. 0 Diff 100 200 300 400

should

No. of iterations be high

Gradient Descent – Debugging & Learning Rate

\-> Done wrong ,

⼩ α

Gradient Descent not working

ð½ Use smaller ð¼

0 100 200 300 400

No. of iterations

11

Gradient Descent – Debugging & Learning Rate

\-> wrong

Gradient Descent not working

ð½ Use smaller ð¼

For sufficiently small ð¼, the cost function ð½, should decrease on every iteration.

0 100 200 300 400

No. of iterations

12

Gradient Descent – Debugging & Learning Rate

Gradient Descent not working Use smaller ð¼

ð½

0 100 200 300 400 …..

No. of iterations

13

\-> keeps

going up & down

so wrong

Gradient Descent – Debugging & Learning Rate

Gradient Descent not working

ð½ Use smaller ð¼

For sufficiently small ð¼, the cost function ð½, should decrease on every iteration.

0 100 200 300 400

No. of iterations

14

Gradient Descent – Debugging & Learning Rate

Summary:

gaurantee reach you 15 will minimum

\- If ð¼ is too small: slow convergence. - If ð¼ is too large: the cost function ð½ may not decrease on every

iteration; may not converge. ↳ no To choose ð¼, try:

gaurantee reach you will

min

…, 0.001, 0.003, 0.01, 0.03, 0.1, 0.3, ㆁ1, …

αgreatest, dont exceed

Multivariate Polynomial Regression

A form of regression in which observational data are modeled by a function which is a nonlinear combination of the model parameters.

The model estimates

when in fact the original function was

16

non-linear regression

\=\> can have line,bu

data very well ↳ will be bad

fits data -\> come that best

data add noise evandom someso data has preferred \#a 0 อ -variability

Multivariate Polynomial Regression

\-area House prices prediction っℎ ð¥ = ð¤ + ð¤ × frontage +ð¤ × depthArea17

\_d Side in length

front 어 house ð¥ = frontage ∗ depth frontage depth ℎ ð¥ = ð¤ + ð¤ × ð¥

Land area

Multivariate Polynomial Regression

18

ð¤ + ð¤ ð¥ + ð¤ ð¥ ㆁ

Multivariate Polynomial Regression

19

\=\>Better

representation

ð¤ + ð¤ ð¥ + ð¤ ð¥ α area + ð¤ 읊 ð¥ tareg

esse

Multivariate Polynomial Regression

ð¤ + ð¤ ð¥ + ð¤ ð¥ + ð¤ ð¥

ℎ ð¥ = ð¤ + ð¤ ð¥ + ð¤ ð¥ + ð¤ ð¥

\= ð¤ + ð¤ (ð ðð§ð) + ð¤ (ð ðð§ð) + ð¤ (ð ðð§ð)

Feature train a good scaling model. becomes necessary in order to

asameatribure

ð¥ ð¥ ð¥ = = = ð ðð§ð ð ðð§ð ð ðð§ð 20

Regression in SKLearn

Kernel = ‘poly’ will do the polynomial regression, need to set degree to a number21

ubf- \>non-linear regression

↳ vey flexible curve Kemel- \> linear\_ Poy , 2 - WM Poly,, 1s e e

rop uei

↳ was flexible

Learning Outcomes

1\. Perform machine learni
