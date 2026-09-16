# DL4H — L15-16: Self-Attention & Transformers
> Source: Google Drive file 1CQglVu-g3aFo1l7_4FDQrOHB1yNIWmcz · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

L15-16\_self-attention\_transformers 

Deep Learning in Healthcare

Self-Attention and Transformers

Ana Namburete Department of Computer Science University of Oxford

Why go beyond CNNs and RNNs?

“The restaurant refused to serve me a ham sandwich because it only cooks vegetarian food. In the end, they just gave me two slices of bread. Their ambiance was just as good as the food and service.”

1 Large encoded input

• 37 words x 1024-dimensional embeddings

• Fully connected networks are infeasible

2 Variable length

• Sentences differ in length

• Architecture must handle arbitrary ð

3 Long-range dependencies

• The word “it” must refer to “restaurant” (not “ham sandwich”)

How do transformers satisfy sequence modelling requirements?

1234

Requirement Transformer Mechanism

Account for relationship between inputs Self-attention weights

Handle sequences of variable length Shared projections (Ωq, Ωk, Ωv)

Compute the same function at each position Shared linear layers + MLP

Track long-range dependencies Direct token-to-token attention

Recap: Sequence Learning

• RNNs are feedforward neural networks rolled out over time

• Ideal for handling sequence data

"ð¦\!

"ð¦\! "ð¦" "ð¦\# "ð¦$

"ð¦%

unroll

… ð¥\!ð¥\! ð¥" ð¥\# ð¥$

ð¥%Unrolled RNN

Self-Attention

Attention

Q: Which part of the input should I focus on?

“The cat drank the milk because it was hungry.”

vs.

“The cat drank the milk because it was sweet.”

ð=1 ð=2

ð=3

ð=7

Attention vectors

ð",$ = softmax" ð"%ð$

The attention distribution depends on the entire input sequence.

Self-attention as routing

Each output uses different weights.

Initialise the weight matrices and compute key, query, and values

Self-attention block

ð& = ð'ℎ&

ð'

In practice, a bias vector may be added to the result of the matrix multiplication.

ð& ð£& ð\* ð£\* ð+ ð£+

ð( ð) ð( ð) ð( ð)

ℎ& ℎ\* ℎ+

Image credit

Dot-product attention

• There are several options of attention scores

• Dot product is commonly used in Transformers

ð",$ = softmax" ð' ð(

ð"%ð$

Dot-product

ð(

ð$ ð"

Single-head attention

Single-head attention

Self-attention is parallelisable Blocks are processed sequentially

Block

⋮ ⋮ ⋮ ⋮

Block

Block

Multi-Head (self-)Attention

Concatenate

Scaled Dot-Product Attention

ð\!\[\#\] ð%\[\#\] ð&\[\#\]

Linear

ð \!

Scaled Dot-Product Attention ð \# ð¾ \# ð \#

ð\!\[(\] ð%\[(\] ð&\[(\]

⋯Scaled Dot-Product

Attention

⋯ð\!\['\] ð%\['\] ð&\['\]

ð»= ℎ\!,ℎ",…,ℎ& ð»= ℎ\!,ℎ",…,ℎ& ⋯ ð»= ℎ\!,ℎ",…,ℎ&

ð»= ℎ\!,ℎ",…,ℎ&

Multi-Head (self-)Attention

Linear

Concatenate (512 ×ð)

Scaled Scaled Scaled Attention

Dot-Product Attention

Attention Dot-Product

Dot-Product

ð\!\[\#\] ð)\['\] ð)\# ð%\[\#\] ð\*\['\] ð\*\# ð&\[\#\]

ð+\['\]

ð+\#

Why multiple heads?

• A single similarity metric is too restrictive

• Multiple heads learn different attention subspaces:

• Synaptic relations

• Semantic relations

• Positional relations

• Increase expressive capacity

• Improves robustness in practice

Efficient Parameterisation

• Split embedding dimension ð across ð» heads

• Each head operates in dimension ,- • Concatenate outputs → linear projection back to ð

• Total parameter count remains controlled

What have we gained?

Self-attention

Strengths Limitation

Content-dependent interactions

❌ No inherent order information

Parallel computation

Shared parameters

Multi-head expressivity

But… no notion of order\!

Positional Encoding

In transformers, no such information is available to either encoder or decoder The output from the self-attention block is permutation-invariant

Order matters\!

• In contrast to RNNs, there is no order information in the inputs of the self- attention block

Positional Encoding

Positional encoding = function of token index ℎ' + ð'

“The food was good, not bad at all.” Position 5

“The food was bad, not good at all.” Position 3

Positional Encoding

• Embedding matrix:

Dimension, ð

ð = 0 …

ð = 511 the

ℎ\!" ∈ ℝ\#$%

food

ℎ$" ∈ ℝ\#$%

was ℎ%" ∈ ℝ\#$% ð=3 ℎ&" ∈ ℝ\#$%

ð=4

ℎ'" ∈ ℝ\#$%

ð=5

ð = 1 ð = 510 ð=0

ð=1

ð=2

good

not

bad

ℎ\#" ∈ ℝ\#$%

ð+ð

Credit: Mitesh Khapra Positional Encoding

• Vector (ð.) to provide additional context to the embeddings, ℎ.

• How • Constant do we fill vector the for elements each position of the ð?

positional vector ð.?

• One-hot encoding for the position?

• Learnable embeddings for all possible positions?

…

ℎ\! ∈ ℝ\#$%

ð\! ∈ ℝ\#$%

ℎ\!" ∈ ℝ\#$%

the

…

Absolute position vs Relative Geometry

• Distance between words in the sentence

• Distance is symmetric around the centre position of the sentence

the food was good not bad at all

the 0 1 2 3 4 5 6 7

food 1 0 1 2 3 4 5 6

was 2 1 0 1 2 3 4 5 good 3 not 4 2 3 ð 1 2 ð,ð 0 1 = 1 0 ð − ð

2 1 3 4 2 3

bad 5 4 3 2 1 0 1 2

at 6 5 4 3 2 1 0 1

all 7 6 5 4 3 2 1 0

Monotonicity:

ð−ð increases as tokens move apart

Translation invariance:

ð ð+ð,ð+ð =ð ð,ð

Symmetry:

ð ð,ð =ð ð,ð

Positional Encoding

the food was good not bad

Method 1

Broadcasting (absolute position) 0 0 0 0 0 0 1 1 1 1 1 1 Index, ð

2 2 2 2 2 2 3 3 3 3 3 3 4 4 4 4 4 4 5 5 5 5 5 5

Method 2

One-hot encoding Questions: 01• Do these positional encoding

methods preserve the notion of 2distance?

3• Are the resultant contextual 4vectors orthonormal? 5

1 0 0 0 0 0 0 1 0 0 0 0 0 0 1 0 0 0 0 0 0 1 0 0 0 0 0 0 1 0 0 0 0 0 0 1

Preserving Orthogonality

• Goal: the dot-product between the two vectors should remain unchanged by adding the positional encoding

One-hot Broadcasting

ð¤( + ð(,ð¤' + ð' = ð¤( , ð¤' + ð( , ð' + cross terms

Credit: Arun Prakash

Positional distortion

Sinusoidal Method 3

Encoding Function

• Embed a unique pattern of features for each position, ð, and the model will learn to attend by the relative position

ð´sin ðð¥ = ð´sin(2ððð¥)

\= ð´ sin(2ðð ð¥)

Distance is associated with wavelengths\!

sin cos ð

1000 ⁄(4 ,ð \!"\#$% , 1000 ⁄(46\# ,\!"\#$% , where ð/0,12 = 512

ð = 0,1, … , 255

ð = 0,1, … , 255

For the fixed position, ð: ðð¸ .,4 =

Use the sin(⋅) function if ð is even Use the cos(⋅) function if ð is odd

Credit: Mitesh Khapra

Sinusoidal Encoding Function

• Example:

• Evaluate ðð¸(A,B) for ð = 0,1, … , 7 and ð = 0,1, … , 63 (ð"CDEF = 64)

• Visualise the resultant matrix as a heat map

For position ð=0:

ð\! = 0,1,0,1,0,…,0,1,0

This vector of alternating 0’s and 1’s will be added to the first word (embedding) of all sequences.

Sinusoidal Encoding Function

• Example:

• Evaluate ðð¸(A,B) for ð = 0,1, … , 7 and ð = 0,1, … , 63

• Visualise the resultant matrix as a heat map

For position ð=0:

ð\! = 0,1,0,1,0,…,0,1,0

These elements will have values close to lim (→\* sin +( = 0 and lim (→\* cos +( = 1

Sine and cosine are orthogonal as they differ by ,% Sine waves of different frequencies are, too

Credit: Mitesh Khapra

The Encoder and Decoder Blocks

Encoder: Bidirectional Self-Attention

• This embedding vector is then passed into the encoder block

• Stack of N=6 identical layers

• Each layer has:

• A multi-head self-attention layer

• A position-wise fully connected feedforward network layer

• Each sub-layer has a residual connection and layer normalisation

The Encoder Block

\=6

Credit: Hung-yi Lee The Encoder Block

Self-attention

Block

Output sequence

Block ⋮

⋮ ⋮ ⋮ Input

ℎ&

ℎ\* ℎ+ ℎJ sequence FC FC FC FC Block

Credit: Hung-yi Lee

ℎ

Residual = ℎ+ð§

ð§

Self-attention

ℎ

Credit: Hung-yi Lee

ð¥ð¥⋮\#(77ð¥-" = ð¥- − ð

ð ð¥%7

norm

norm

ℎ

ð¥ð¥⋮\#(ð¥%Mean, Standard deviation, ð Residual = ℎ+ð§

ð ð§

Self-attention

ℎ

Credit: Hung-yi Lee

norm ð¥\#ð¥(⋮ð¥%ð¥\#7ð¥(7⋮ð¥%7

Mean, ð Standard deviation, ð

norm

ð¥-" = ð¥- − ð

ð

FC

norm

ℎ

Residual = ð+ð

ð

Self-attention

ℎ

The Encoder Block

\=6

Residual + LayerNorm

ℎ

Self-attention

norm

FC

norm

ℎResidual = ℎ+ð§ ð§

• Each layer has:

• Two multi-head self-attention layers

• One position-wise fully connected feedforward network layer

• Similar to the encoder, each sub-layer has a residual connection and layer normalisation

Output sequence

Encoder Decoder

Input sequence

The Decoder Block

The Autoregressive Decoder Block

• Autoregressive decoder

• \<BOS\> token symbolises the “beginning of the sentence”

• \<EOS\> is the “end of the sentence”

Encoder Decoder

\<BOS\>

Note: Scheduled sampling

\<EOS\>

(special token)

“I”

“am”

“here”

softmax

“I”

“am”

“here”

Masked Self-Attention

ð¥1 ð¥2 ð¥3 ð¥4

ð¥1 ð¥2 ð¥3 ð¥4

ð¥1 ð¥2 ð¥3 ð¥4

ð¥1 ð¥2 ð¥3 ð¥4

0 −∞ −∞ −∞

0 0 −∞ −∞

0 0 0 −∞

0 0 0 0

ð¥1 −∞ −∞ −∞

✚ ＝

ð¥1 ð¥2 −∞ −∞

ð¥1 ð¥2 ð¥3 −∞

ð¥1 ð¥2 ð¥3 ð¥4

Attention matrix Masking matrix Masked scores

ð´ = ðð¾2

ð-3 = T−∞, 0, ð \> ð ð ≤ ð

ð´" =ð´+ð

MaskedAttention ð,ð¾,ð =Softmax ðð¾% + ð

ð(

ð

Entries with −∞ become 0 after softmax.

FC

ð$ ð£$

ℎ$

From encoder ð£ Cross-attention

ð¼$"

ð¼%"

ð¼&"

ð%ð£% ð&ð£&

ð

ℎ%

ℎ&

Encoder Masked self-attention

\<BOS\>

Cross-Attention

Liu et al. 2022. https://arxiv.org/abs/2005.08081

Cross-Attention

• In the original implementation, the decoder takes the last output of the encoder

Transformers: The Full Architecture

Credit: Mitesh Khapra Training Transformers

• Analogy: hidden layers

Transformer architecture as a stack of attention Every and encoder block has:

• 2 hidden FC layers

• 1 self-attention layer

Every decoder has:

• 2 hidden FC layers

• 2 self-attention layers

The network has 42 layers:

• 6 encoders

• 6 decoders

• How do we ensure gradient flow across the network?

• Residual connections

• How do we speed up the training process?

• Normalisation

Applications

“An image is worth 16x16 words”

Dosovitskiy et al. 2020. https://arxiv.org/abs/2010.11929

Vision Transformer (ViT)

Split image input patches Vectorise patches, and

add positional encoding

Vision Transformer (ViT)

Feed concatenated vectors into the transformer encoder

Perform classification with feedforward network

Image source

Split image input patches Vectorise patches, and

add positional encoding

Vision Transformer (ViT)

Additional ‘class token’ contains class label

Feed concatenated vectors into the transformer encoder

Perform classification with feedforward network

Image source

Shifted Window (SWin) Transformer

Karimi, Davood, Serge Vasylechko, and Ali Gholipour. "Convolution-Free Medical Image Segmentation using Transformers." (2021).

• Using the encoder part of the transformer to perform segmentation

Transformers in: Medical Image Segmentation

Results

BERT

…

• Training BERT requires 2 steps:

• (1) Pre-train BERT to understand language

• (2) Fine-tune BERT to learn a specific task

Devlin, Chang, Lee, and Toutanova. BERT: Pre-training of deep bidirectional transformers for language understanding. In ACL, 2019

BERT (2018)

• BERT: Bidirectional Encoder Representations from Transformers

• Stacked Encoder blocks

Pre-training

Masked Language Model (MLM)

The \<mask1\> brown fox \<mask2\> over the lazy dog.

\<mask1\> = quick

\<mask2\> = jumped

The \<mask\> sat on the mat. \<mask\> = cat

Training BERT

• Task 1: Masked Language Model (MLM)

• Randomly mask one or multiple words in a sentence

• Ask BERT to predict the masked word(s)

Masked Language Model (MLM)

the

ð Loss: ℒ = CrossEntropy(ð4567,ð8579)

softmax classifier

ð£\!

ð£)

ð£\#

ð£$

ð£\*

ð£+

Transformer Encoder

ℎ\!ℎ)ℎ\#ℎ$ℎ\*ℎ+Embedding Layer

\<mask\>

sat on the mat

Training BERT

• Training BERT requires 2 steps:

• (1) Pre-train BERT to understand language

• (2) Fine-tune BERT to learn a specific task Pre-training

Next Sentence Prediction (NSP)

Sentence 1: I am going out. Sentence 2: I will be back before 6pm.

Yes, Sentence 2 follows Sentence 1

\<IsNextSentence\>

Sentence 1: I am going out. Sentence 2: Pandas are native to Asia.

No, Sentence 2 does not follow Sentence 1

\<NotNextSentence\>

Credit: Shusen Wang Next Sentence Prediction (NSP)

ð¦

(between 0 and 1) Loss: ℒ = ð¶ððð ð ð¸ðð¡ðððð¦(ð¦4567,ð¦8579)

binary classifier

ð ð¢\!,ð¢",…,ð¢, ð 

ð£\!,ð£",…,ð£, Transformer Encoder

Embedding Layer

\<CLS\> first\_sentence \<SEP\>

second\_sentence

BERT

• BERT is self-supervised:

• Labels generated by MLM and NSP

• Does not require manually labelled data

• Can use large-scale data corpus

• e.g. English Wikipedia, 2.5 billion words

• Limitation:

• Requires heavy computation

• BERT Base: 110M parameters; 16 TPUs; 4 days of training

• BERT Large: 235M parameters; 64 TPUs; 4 days of training

Lee et al. BioBERT: a pre-trained biomedical language representation model for biomedical text mining, (2021).

BioBERT

• Standard BERT is pretrained on BooksCorpus and Wikipedia

• Clinical language differs substantially

• BioBERT is pretrained on large-scale biomedical corpora

ClinicalBERT (2020)

Example: Fine-tuned predict hospital to readmission

• Applies BERT to clinical notes

• Representations are learned from medical text

• Fine-tuned for downstream clinical tasks

Huang et al. ClinicalBERT: modelling clinical notes and predicting hospital readmission, (2019).

Credit

Huang et al. ClinicalBERT: modelling clinical notes and predicting hospital readmission, (2019).

ClinicalBERT

• Through fine-tuning, ClinicalBERT can be adapted to downstream tasks, e.g. prediction of 30-day hospital readmission

Slide credit: Serena Yeung

Transformers across modalities

Same architecture What changes

• Multi-head self-attention

• Residual connections

• LayerNorm

• Feedforward blocks

Structure of the inputs

• Tokens

• Patches

• Clinical notes

Training objective

• MLM

• Classification

• Segmentation

Data scale

Further Reading

Useful resources:

• “Attention is all you need” article \[link\]

• Blog on “The Illustrated Transformer” \[link\]

• Detailed explanations of positional encoding \[link\]\[link\]

• A list of (almost all) transformers \[link\]

• Articles on Layer Normalisation in transformers \[link\]\[link\]

• Article on Power Normalisation in transformers \[link\]

• Article on cross-attention \[link\]

<https://towardsdatascience.com/illustrated-self-attention-2d627e33b20a>   
<https://arxiv.org/abs/
