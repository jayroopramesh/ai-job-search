# DL4H — L14-15: Sequence Models (RNNs, LSTMs, GRUs)
> Source: Google Drive file 163bfyyq51WXHD6I_Memw2gS3-YSr4MjL · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L14-15\_sequence\_models 

Deep Learning in Healthcare

Sequence Learning

Ana Namburete Department of Computer Science University of Oxford

Convolutional Fully-connected neural networks

neural networks (linear layers;

(convolutional layers; suitable for image inputs) suitable for vectorised inputs)

ð¥\!ð¥"ð¥\#

Recurrent neural networks (linear layers that model sequential relations; suitable for temporal inputs)

\!ð¦\!

…

Input sequence

Output sequence

Why sequence models?

Fixed-size vector

E.g. Image captioning

Examples of sequence learning

1 One-to-many

One-hot encoding

2 Many-to-one

Fixed-size vector

E.g. Hydrophilicity prediction (Drug discovery)

H= 1 0 0 0 ⋯ 0 C= 0 1 0 0 ⋯ 0 O= 0 0 1 0 ⋯ 0 Acetaminophen … (Paracetamol)

1 Many-to-many

E.g. Language translation

“Good morning.”

“Bom dia.”

Image credit

Sequence modelling desiderata

To model sequences, we need to:

1 Account for relationship between inputs

2 Handle sequences of variable length

3 Compute the same function at each time step

4 Track long-term dependencies

We will focus on each of these in turn until we arrive at a model to handle sequential data.

Recurrent Neural Networks (RNNs)

Based on a temporal chain:

ℎ\! =ð ð¥\! ℎ\!"\#

Simplified Feedforward neural network representation Output vector

%ð¦∈ℝ"

%ð¦\# ∈ ℝ" ð¦\! ð¦$

Time step, ð¡

ð¥\! ð¥" ð¥\#

Input vector

ð¥∈ℝ\!

ð¥\# ∈ ℝ\!

Function at each timestep

• Let’s first consider the function that is computed at each timestep %ð¦$%ð¦'ℎ$

ð%&

ð%& ð¥$ð¥'ð¡ = timestep ð&(

ð&( ℎ' =ð ð()ð¥' + ð

ℎ'

ð¦' = ð\* ð)+ℎ' + ð

where: ð is the non-linearity in the hidden layers ð\* is the output mapping function

Function at each timestep

• Goal: Execute the same function at each timestep

• Solution: use the same network

• i.e. use the same parameters are each timestep

• Advantages:

• Parameter-sharing ensures that the network is agnostic to the length (size) of the input sequence

• Easy to create multiple copies of the same network and execute them at each timestep

"ð¦\! ðℎ\!

…

ð¥\!ð$%

"ð¦"

%&

ðℎ"

ð¥"ð$%

"ð¦\#

%&

ðℎ\#

ð¥\#ð$%

"ð¦$

%&

ðℎ$

ð¥$ð$%

"ð¦%

%&

ð%&

ℎ%

ð¥%ð$%

Accounting for input relationships

Naïve approach:

• Suppose previous input that at to a the given network timestep, we were to feed every Timestep ð¡=1

"ð¦\!

ℎ\!

ð¥\!ð$%

Timestep ð¡=2

"ð¦"

ℎ\!

ð¥"ð$%

Timestep ð¡=4

"ð¦$ ð%&

ð%&

ð%&

ℎ\!

ð¥\!

ð¥\!

ð¥" ð¥\# ð¥$ð$%

Although this accounts for the relationships between inputs (and maintains order), it violates two other items on our “wishlist”

Credit: Mitesh Khapra

Timestep ð¡=3

"ð¦\#

ð%&

ℎ\!

ð¥\!

ð¥" ð¥\#ð$%

…

Credit: Mitesh Khapra Accounting for input relationships

Timestep ð¡=1

"ð¦\!ℎ\! ℎ" ℎ\# ℎ$

ð¥\!ð$%

Timestep ð¡=2

Timestep ð¡=3

Timestep ð¡=4

"ð¦""ð¦\#"ð¦$ð%&

ð%&

ð%&

ð%&

ð¥\!

ð¥"ð$%

ð¥\!

ð¥" ð¥\#ð$%

ð¥\!

ð¥" ð¥\# ð¥$ð$%

• The function executed at each timestep is now different

• The sequence

network is now sensitive to the length of the input …

"ð¦\! = ð\! ð¥\! "ð¦"ð¦" \# = = ðð" \# ð¥ð¥\!\!,ð¥,ð¥" ",ð¥\# "ð¦$ = ð$(ð¥\!,ð¥",ð¥\#,ð¥$)

Recurrence connections

• Solution: add recurrence connections

ð¦\!ð¦"ð¦\#ð¦$ð¦%ð%&

ð%&

ð%&

ð%&

ð%&

ℎ\!ð%%

ℎ"ð%% ℎ\#ð%% ℎ$ð%% … ℎ%ð$%ð$%ð$%ð$%ð$%ð¥\!ð¥"ð¥\#ð¥$ð¥%Introduce new parameter ð)) to connect across the timesteps

Credit: Mitesh Khapra

RNN Forward Pass

• “Rolled” representation

ð¦\!ð¦"ð¦\#ð¦$ð¦%ð%&

ð%&

ð%&

ð%&

ð%& ℎ\!ð%%

ℎ"ð%% ℎ\#ð%% ℎ$ð%% … ℎ%ð$%ð$%ð$%ð$%ð$%ð¥\!ð¥"ð¥\#ð¥$ð¥%Forward Pass equations:

ℎ' =ð ð()ð¥' + ð))ℎ'12 + ð

ð¦' = ð\* ð)+ℎ' + ð

All parameters (ð= ð$%,ð%%,ð%&, ð, ð ) are shared across the timesteps

Credit: Mitesh Khapra

RNN Forward Pass

• “Rolled” representation

ð¦\!ð¦"ð¦\#ð¦$ð¦%ð%&

ð%&

ð%&

ð%&

ð%& ℎ\!ð%%

ℎ"ð%% ℎ\#ð%% ℎ$ð%% … ℎ%ð$%ð$%ð$%ð$%ð$%ð¥\!ð¥"ð¥\#ð¥$ð¥%Forward Pass equations:

ℎ' =ð ð()ð¥' + ð))ℎ'12 + ð

ð¦' = ð\* ð)+ℎ' + ð

All parameters (ð= ð$%,ð%%,ð%&, ð, ð ) are shared across the timesteps

Credit: Mitesh Khapra

ð¦\!ð¦"ð¦\#ð¦$ð¦%ð%&

ð%&

ð%&

ð%&

ð%& ℎ\!ð%%

ℎ"ð%% ℎ\#RNN Forward Pass

• “Rolled” representation

More compact representation

ð¦'ð&'

ð%% ℎ$ð%% … ℎ%ℎ'ð$%ð$%ð$%ð$%ð$%ð¥\!ð¥"ð¥\#ð¥$ð¥%ð%&

ð&&

ð¥'Forward Pass equations:

ℎ' =ð ð()ð¥' + ð))ℎ'12 + ð

Or, ð¦' =ð ð¥',ℎ',ð(),ð)),ð)+, ð, ð ð¦' = ð\* ð)+ℎ' + ðAll parameters (ð= ð$%,ð%%,ð%&, ð, ð ) are shared across the timesteps Same network (and parameters) can be used to compute ð¦\#,ð¦',…,ð¦\#(,…,ð¦\#(((

Backpropagation Through Time (BPTT)

How do we train RNNs?

• We will first consider the dimensions ð¦\!of each of the components

ð%&ℎ\!ð%%

ð$% ð¥\! ð¥" ð¥( ð¥)

ð¦"ð%&ℎ"ð%%

ð$%

ð¦(ð%&ℎ\#ð%%

ð$%

ð¦)ð%&ℎ$ð%%

ð$%

ð¥' ∈ ℝ9 ð-dimensional input ℎ' ∈ ℝ: ð-dimensional hidden state ð¦' ∈ ℝ; ð classes

• The parameters have dimensions:

ð)( ∈ ℝ9×: ð)) ∈ ℝ:×: ð)+ ∈ ℝ:×;

Forward pass

Backward pass

? ℒ ð = \<ℒ'(ð)

'\>2Forward pass The total loss is the sum of the loss over all timesteps (ð)

ℒ

ℒ\! ℒ" ℒ( ℒ) ℒ\* …ð¦'ð¦)ð¾ððℎ'ℎ$ℎ%

…

ð¥\! ð¥" ð¥( ð¥)

ð¾ðð

ð%& ð¾ðð ð¥'ð¦\!ð¾ððℎ\!ð¾ðð ð¾ðð

ð¦"ð¾ððℎ"ð¾ðð

ð¾ðð ð¦(ð¦\*unroll ð&'

ð¾ððð¾ðð

ð&&

ℎ\#ð¾ðð

ð¾ðð

ð¥\*

Forward pass

Backward pass

? ℒ ð = \<ℒ'(ð)

'\>2Backward pass The total loss is the sum of the loss over all timesteps

ℒ

…Goal:

Compute:

ðℒ ðð$% , ðððℒ

%% ℒ\! ℒ" ℒ( ℒ) ℒ\* ð¦\!ð¾ðð, ðððℒ

%&

ℎ\!…

ð¥\! ð¥" ð¥( ð¥)

ð¾ðð

ð¾ðð

ð¦"ð¾ððℎ"ð¾ðð

ð¾ðð

ð¦(ð¾ððℎ\#ð¾ðð

ð¾ðð

ð¦)ð¦\*ð¾ððð¾ðð

ℎ$ð¾ðð

ð¾ðð

ð¥\*

Gradient Flow through Time

• Goal: Calculate the gradients of ℒ wrt. weights ð\!",ð\!\!,ð\!\#

• We can then use e.g. SDG to update the weights

• How do we compute %'%ℒ?

ðℒ ðð ðℒ ðð - = D\!,\#- = D\!,\#First, note that we have an error for every timestep

ðℒ\! ðð

ðℒ ðð = ðℒðð \!

ðℒ\! ðð

Many-to-many Many-to-one One-to-many

Gradient wrt. ð&(

ðℒ ðð&'

• • Consider We can start the by loss calculating at one timestep, the gradient e.g. ℒ$

%'%ℒ'(

&

ℒ\! ℒ" ℒ( ℒ) ð¦\!ð¦"

ð¦(

ð¦)ð%&

ℎ\!

ℎ"

ð¥\! ð¥" ð¥( ð¥) ð%%

ℎ\#ℎ$

Gradient wrt. ð&(

ðℒ ðð&'

• • Consider We can start the by loss calculating at one timestep, the gradient e.g. ℒ\* %'= %ℒ/0 .

ð¦\* − %ð¦\* + \[MSE loss\]

• Let all activation functions be linear

Let ð\# = ð)\*ℎ\#, where "ð¦\# = ð+ ð\# . ℒ\!

ℒ" ℒ( ℒ) The loss gradient can be calculated as

ðℒ\# ð¦)ðð)\* = ðℒðð¦\# \#

ℎ$This becomes the gradient ð¥\! ð¥" ð¥( ð¥)

for ð¡=3, so the total loss is the sum:

ðð¦\# ð¦\!ðð)\*

\= ðℒðð¦\# \#

ℎ\!

ð¦"

ℎ"

ð¦(

ð%& ℎ\#ðð¦\# ðð\#

ðð\# ðð)\*

ð%%

\= ðℒðð¦\# \#

ðððð¦\#

\# ℎ\# =2ð¦\# − "ð¦\# ℎ\#

ðℒ ðð)\* \# = 3,-\!ðℒ, ðð)\*

• What about +-+ℒ--,

?

ℒ\! ℒ" ℒ( ℒ) ð¦\!ð¦"

ð¦(

ð¦)ð¾ðð

ℎ\!

ℎ"

ð¾ðð ℎ\#ℎ$ð¥\! ð¥" ð¥( ð¥)

Gradient wrt. ð$$

We know that we can write this as

ðℒE ðð)) = ðℒðð¦E E

ðð¦E ðℎE

ðℎE ðð))

ðℒ ðð&&

• What about +ℒ,

\+---?

ð¦ℒ\! ℒ" ℒ( ℒ) ð¦\!ð¦" )ℎ\!

ℎ"

ℎ$ð¦( ð¾ðð

ð%%

ℎ\#

ð¥\! ð¥" ð¥( ð¥)

We know that we can write this as

ðℒE ðð)) = ðℒðð¦E E

ðð¦E ðℎE

ðℎE ðð))

This is not the full picture because ℎ\# also depends on ð)) and on ℎ"

ℎE =ð ð()ð¥E + ð))ℎF + ð

The chain rule needs to be applied again\!

Gradient wrt. ð$$

ðℒ ðð&&

Note: We can compute gradient 131ℒ"\# \!

in a similar way.

• Observe that indirectly via ℎℎ"( , depends ℎ\!, … on ð&& directly, and also ℒ\!

ℒ" ℒ( ℒ) ðℒ\#

ðð)) = ðℒ\# ðð¦\#

ð¥\! ð¥" ð¥( ð¥)

Hence, we can write this gradient as follows:

ðℒE ð¦)ðð)) ℎ$E = \<;\>\!ðℒE ðð¦E

ðð¦E ðℎE

ðℎE ð¦\!ðℎ;

ℎ\!

ð¦"

ℎ"

ð¦(

ð¾ðð ℎ\#ðℎ\#

\+ ðℒ\# ðð¦\#

ðð¦\#

ð%%

ðℎ\#

ðð))

ðℎ"

\+ ðℒ\# ðð¦\#

ðð¦\#

ðℎ\# ðℎ\#

ðℎ"

ðð))

ðℎ\!

\+ ðℒ\# ðð¦\#

ðð¦\#

ðℎ\#

ðℎ" ðℎðð¦\# \#

ðℎðℎ" \#

ðℎðℎ\! "

ðððℎ\!

))

ðℎ. ðℎ\#

ðℎ"

ðℎ\!

ðℎ.

ðð))

Gradient wrt. ð$$

ðℒ ðð&&

ðℎ; ðð))

Gradient Flow through Time

• The all intermediate gradient from one-step time ð¡ back Jacobians.

to time ð is the product of ðℎ. ðℎ/ = ðℎðℎ\! (

\= ðℎðℎ( "

ðℎ" ðℎ\!

As such, the gradient can be written as:

ðℒ( ðð&& ( = +/01ðℒ( ðð¦(

where /)/)()\* (

is a

one-step Jacobian.

ðð¦( ðℎ( ( ,20/3\!

ðℎ2 ðℎ24\!

ðℎ/ ðð&&

What is the problem with this?

Exploding/Vanishing Gradients

Gradient Flow Problems

Suppose we consider just one term in the product, e.g. +&+&./0

.

Let the activations be given by:

ðℎ/ / = = ð(ðð&&/ℎ)

/ + ð&& ð4 = ð4\#,ð4',ð45,…,ð46

ℎ4 = ð(ð4\#), ð(ð4'), ð(ð45), … , ð(ð46) Note: - If it is ð0 ℎ0

We are interested in the magnitude small (or large), then 1%17$ $ and hence ð)),ð))

of 131ℒ1%"" '

1%$%&

will $

vanish (or explode)

Gradient Flow Problems

Suppose we consider just one term in the product, e.g. %\!%\!123 1 Let the activations be given by: ðℎ( ( = = ð(ðð\!\!(ℎ) ( + ð\!\! The gradient will be computed as

ðℎ( ðℎ()\* = ðℎðð( (

ð4 = ð4\#,ð4',ð45,…,ð46

ð)),ð)) ð0 ℎ0

ℎ4 = ð(ð4\#), ð(ð4'), ð(ð45), … , ð(ð46)

ðℎ4\# ðð4\# ðℎðð4

4 =

ðℎ4' ðð4\# ⋯ ðℎ46 ðð4\# ðℎ4\# ðð4'

ðℎ4' ðð4' ⋯ ⋮ ⋮ ⋮ ⋱ ⋮ ⋮ ⋯ ⋯ ðℎ46 ðð46

Note: - If it is We are interested in the small (or large), then 1%17$

$ magnitude and hence of 1ℒ1%'

1%$%&

$ 13"" ðð( ðℎ()\*

will vanish (or explode)

Gradient Flow Problems

Suppose we consider just one term in the product, e.g. %\!%\!123 1 Let the activations be given by: ðℎ( ( = = ð(ðð\!\!(ℎ) ( + ð\!\! The gradient will be computed as

ðℎ( ðℎ()\* = ðℎðð( (

ð4 = ð4\#,ð4',ð45,…,ð46

ð)),ð)) ð0 ℎ0

ℎ4 = ð(ð4\#), ð(ð4'), ð(ð45), … , ð(ð46)

ðℎ4\#

ðℎ4' ðð4\# ðð4\# ðℎ4 ðð4 =

⋯ ðℎ46 ðð4\# ðℎ4\# ðð4'

ðℎ4' ðð( ðð4' = ðððð ðℎð()\* + ð( ð\!\!

⋯ ⋮

⋮ ⋮ ⋱ ⋮ ⋮ ⋯ ⋯ ðℎ46 ðð46

\=

ð′(ð4\#) 0 ⋯ 0

Note: - If it is We small are (or interested large), then in the 1%17$

$ magnitude of 1%1%$%& $

0 ð′(ð4') ⋯ 0 ⋮ ⋮ ⋱ ⋮ 0 ⋯ ⋯ ð′(ð46) = ðððð(ð′(ð4)) and hence 1ℒ'

13"" will vanish (or explode)

ð(ð\!) is a sigmoid, ð8 ð\! ≤ \#9 = ð¾

Gradient Flow Problems

• Looking closely at the magnitude of this term, we can express it as:

ðℎ; ðℎ;12 = ðððð ð′ ð; ⋅ ð))

≤ ðððð ðR(ð;) ⋅ ð))

Image credit

Hölder’s inequality: ðð ≤ ð ⋅ ð

ð) ð ≤ ð¾

Image credit

Gradient Flow Problems

• Looking closely at the magnitude of this term, we can express it as:

ðℎ; ðℎ;12 = ðððð ð′ ð; ⋅ ð))

≤ ðððð ðR(ð;) ⋅ ð))

Since ð(ð4) is a bounded function (i.e. sigmoid or be tanh), bounded.

then its derivative, ð′(ð4), must also

• By substituting ð¾, we get ðℎ;

ðℎ;12 ≤ ð¾ð

ð&& ≤ ð

Gradient Flow Problems

• Similarly, we can express the product in terms of ð¾:

ðℎ' ðℎ; ' = GV\>;W2

ðℎV ðℎV12

' ≤ Gð¾ð

V\>;W2 ≤ ð¾ð '1;

• If ð¾ð \<1, gradients vanish

• If ð¾ð \>1, gradients could explode

This is known as the vanishing / exploding gradient problem.

Is it possible to address the vanishing gradient problem without changing the architecture?

Truncated BPTT

• Truncated backpropagation restricts the product to consider just ð terms at a time ð \< (ð¡ − ð)

ℒ.

Another strategy: Gradient clipping

Standard BPTT Truncated BPTT

ℒ.

LSTMs

The Problem of Long-Term Dependencies

• As the gap grows, RNNs become unable to learn to connect the information

The Standard RNN

• Each step, ð¡, the RNN block outputs a hidden state, ℎ.

The repeating module of a standard RNN contains a single layer

Long-Short Term Memory (LSTM)

• “Long-short term memory” units

• Designed specifically to address long-range dependency problem

The repeating module of an LSTM contains four interacting NN layers

Cell state (ð¶.)

Can think of it as a “gradient highway” Very easy for information to flow along it unchanged

LSTM

• Key ideas behind the LSTM: the cell state and the gates

Cell state (ð¶.)

Gate

Can think of it as a “conveyor belt”

Selectively let information flow through Very easy for information to flow along it unchanged

Regulate the removal or addition of information to the cell state

An LSTM has 3 of these gates to protect and control the cell state.

LSTM

• Key ideas behind the LSTM: the cell state and the gates

LSTM: Explained

Forget Gate

1 Deciding which information to discard from the cell state

Learnable parameters

Sigmoid activation

Inputs

Input Gate

2 Deciding which information to store in the cell state

Values between 0 and 1

Values between -1 and 1

Inputs

1

Combining Forget + Input Gates

2 Deciding which information to remove/store in the cell state

From input gate

From forget gate

∗ = Element-wise product

Output Gate

3 Deciding what information to output

Learnable parameters

Inputs

ð¶\!

Hidden state passed on to the next cell

Credit: Vineeth Balasubramanian

LSTM Equations

Sigmoid gates with values between 0 and 1 Forget gate ð' =ð ðY ⋅ ℎ'12,ð¥' + ðY

Input gate ð' =ð ðZ ⋅ ℎ'12,ð¥' + ðZ

Output gate ð' =ð ð\* ⋅ ℎ'12,ð¥' + ð\*

Controls what is kept/forgotten from previous cell state

Controls what parts of the new content are written to the cell

Controls what parts of the cell transmitted to the hidden state

New cell content ð¶J' = tanh ð\[ ⋅ ℎ'12,ð¥' + ð\[

Current cell state ð¶' = ð' ⋅ ð¶'12 + ð' ⋅ ð¶J'

Hidden state ℎ' = ð' ⋅ tanh ð¶'

The new content to the written to the cell

Erase (i.e. “forget”) some content from the last cell state, and write (i.e. ”input”) some new cell content

Transmit (i.e. ”output”) some content from the cell

If ð' = 1 and ð' = 0,

ð¶' = ð¶'12

So the memory is copied forward unchanged.

Current cell state ð¶' = ð' ⋅ ð¶'12 + ð' ⋅ Jð¶'

Hidden state ℎ' = ð' ⋅ tanh ð¶'

If ð' = 1 and ð' = 0,

ð¶' = ð¶'12

So the memory is copied forward unchanged.

If ð' = 1, ð' = 0 and ð' = 1,

The memory becomes entirely the new candidate state. This almost reduces to a vanilla RNN, except for the extra tanh. So the LSTM generalises the RNN.Current cell state ð¶' = ð' ⋅ ð¶'12 + ð' ⋅ Jð¶'

Hidden state ℎ' = ð' ⋅ tanh ð¶'

Gradient “highway”

Cell state update:

ð¶' = ð' ⊙ ð¶'12 + ð' ⊙ Jð¶'

LSTMs address the vanishing gradient problem

Gradient along the highway: ðð¶'

ðð¶'12 = ð'

Gradient across multiple timesteps:

ðð¶' ðð¶; '

\= GðV V\>;W2

LSTMs address the vanishing gradient problem

Gradient “highway”

Learn more…

Vanilla RNN:

G diag ð′ ð))

LSTM:

GðV

Exploding gradients may still occur → use gradient clipping.

Vanishing gradients are significantly mitigated.

Vanilla RNN vs. LSTM

Variations on LSTMs

”Peephole” connections allow the gate layers to look at the cell state.

Gers & Schmidhuber (2000)

LSTM with Peephole Connections

Vanilla LSTM ð¶' = ð' ∗ ð¶'12 + ð' ∗ Jð¶'

Instead of separately deciding what to forget and what to add, make the decisions together

Coupled Forget and Input Gates

Combine forget and input gates into a single update gate Merges cell state and hidden state

Chung et al. (2014)

Gated Recurrent Units (GRU)

Credit: Vineeth Balasubramanian

Gated Recurrent Units (GRU)

Controls s etaGUpdate gate

Reset gate

which parts of the hidden state are updated vs. preserved

Controls which parts of the previous hidden state are used to compute new content

Combines forget and input gates into a single update gate Merges cell state and hidden state

Chung et al. (2014)

The Credit: Vineeth Balasubramanian Gated Recurrent Units (GRU)

reset gate (ð\!) selects useful parts of the and hidden previous current content input hidden (ℎ\](ð¥\!).\!state ) to compute (ℎ\!"\#). Use new

this

The update gate (ð§\!) simultaneously controls what is kept from the previous hidden state, and what is updated

Update gate

Reset gate

New hidden state content

Hidden state

Combines forget and input gates into a single update gate Merges cell state and hidden state

Chung et al. (2014)

Summary: LSTMs vs GRUs

LSTM GRU

Number of gates 3 gates 2 gates

Gate composition Separate input and forget gates Input and forget gates are coupled

into an update gate

Reset gate is applied directly to the previous hidden state (ℎ\!"\#)

Memory/History ð¶\! serves as the internal memory

of the network

No internal memory (ð¶\!) that is different from the exposed hidden state (ℎ\!). Only a hidden state

No output gate

Note: LSTM is a good default choice, especially if data has long-range dependencies. Switch to GRUs for speed, and if the training dataset is small.

Applications

Image source: \[1\]\[2\]

Application: Abnormal EEG Detection

• Manual analysis of EEG or CTG data

• Requires highly trained clinicians

• Time-consuming process

Example: CTG

Ogasawara et al. Nature Sci Reps 2021

Potential solution: RNNs can facilitate detection of fetal distress (ideally, in real-time) i.e. identifying whether heart rate acceleration/decelerations are normal or abnormal

Normal delivery

Abnormal delivery

Application: Abnormal EEG Detection

• Manual analysis of EEG or CTG data

• Requires highly trained clinicians

• Time-consuming process

Proposed solution: ChronoNet RNNs can facilitate detection of normal or abnormal brain activity 86% accuracy Roy et al. J Neural Eng 2018

Image source: \[1\]\[2\]

Example: EEG

Each 1D CONV layer uses multiple filters of exponentially varying lengths

Stacked GRU layers densely connected with skip connections

Application: Disease Progression Modelling

• Alzheimer’s is a progressive disease

• Existing Disease Progression Modelling (DPM) algorithms:

• Neglect temporal dependencies across measurements

• Fail to jointly model multiple biomarkers

Ghazi et al (2019) proposed an LSTM to model AD progression using 6 volumetric measures extracted from a brain MRI scan

ventricles, hippocampus, whole brain, fusiform, middle temporal gyrus, entorhinal cortex

Ghazi et al. MedIA 2019

Further Reading

Textbooks:

• Goodfellow et al. Deep Learning, Chapter 10

• Sections 10.1-10.7, 10.10-10.11

• Graves, Alex. Supervised Sequence Labelling with Recurrent Neural Networks (Section 4.6)

• Pascanu et al. “On the difficulty of training recurrent neural networks”, ICML, 2013

• Hochreiter and Schmidhuber. “Long short-term memory”, Neural Computing, 1997

Useful resources:

• Blog on “Understanding LSTMs” \[link\]

• Illustrated Guide to LSTMs and GRUs \[link\]

References

• Textbooks:

• Goodfellow et al. Deep Learning: Chapter 10

• Pascanu et al., “On the difficulty of training recurrent neural net
