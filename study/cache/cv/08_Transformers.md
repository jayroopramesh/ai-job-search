# Computer Vision — Transformers
> Source: Google Drive file 1EtOt3oMta5NTEBSlBTtpWxryr3HKXmet · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Transformers

Computer Vision – Lecture 08

1

Further Reading

• Slides from F Li

• Slides from J Johnson

• Slides from M Niessner

• None of the books I know contains transformers. Foundations of Computer Vision covers transformers

2

CNNs to Transformers

An image is worth 16x16 words: Transformers for image recognition at scale, A Dosovitskiy et al., 2021

3

Attention

Attention Is All You Need, A Vaswani et al., 2017 (100k citations now)

• Before: main building block is a convolution.

• After: main building block is multi- head attention.

4

1D Attention

• Attention was first developed for natural language processing.

• Used to process a sequence of tokens (e.g. words).

• Each token is embedded into a vector space.

• Idea: long-range context is important.

5

Bahdanau et al, “Neural machine translation by jointly learning to align and translate”, ICLR 2015 Slide adapted from J Johnson

1D Attention

Example machine translation:

• Languages tend to vary in word order.

• The model cannot translate word-by-word but must be able to look at all words.

6

Bahdanau et al, “Neural machine translation by jointly learning to align and translate”, ICLR 2015 Slide adapted from J Johnson

1D Attention

Example machine translation:

• English: “The agreement on the European Economic Area was signed in August 1992.”

• French: “L’accord sur la zone économique européenne a été signé en août 1992. ”

7

1-to-1 matching in word order

1D Attention

Example machine translation:

• English: “The agreement on the European Economic Area was signed in August 1992.”

• French: “L’accord sur la zone économique européenne a été signé en août 1992. ”

8

Bahdanau et al, “Neural machine translation by jointly learning to align and translate”, ICLR 2015 Slide adapted from J Johnson

1-to-1 matching in word order 1D Attention

reverse word order

Example machine translation:

• English: “The agreement on the European Economic Area was signed in August 1992.”

• French: “L’accord sur la zone économique européenne a été signé en août 1992. ”

9

Bahdanau et al, “Neural machine translation by jointly learning to align and translate”, ICLR 2015 Slide adapted from J Johnson

1-to-1 matching in word order 1D Attention

reverse word order

different number of words

Example machine translation:

• English: “The agreement on the European Economic Area was signed in August 1992.”

• French: “L’accord sur la zone économique européenne a été signé en août 1992. ”

Bahdanau et al, “Neural machine translation by jointly learning to align and translate”, ICLR 2015 Attention

10 Slide adapted from J Johnson

Setup for attention

Input: sentence to translate

L’accord

sur

1992

Input: sequence of tokens that should

ð§1

ð§211

…

ð§ð

predict the words of the translation

input token 1 ð¥1 input token 2

input token ð

…

Output: sequence of tokens, e.g. each with a probability distribution over words

ð¥2ð¥N

ð¦1ð¦2Attention

ð¦N

…

output token 1

output token 2

output token ð

Input/Output Behaviour

• ð input tokens ð¥ð ∈ ℝð

• ð “condition” tokens ð§ð ∈ ℝð

• Predict: ð output tokens ð¦ð ∈ ℝð

• We assume all vectors are in ℝð, if not a linear layer can fix it.

• Similar to convolution, many of these layers can be stacked.

• Example translation: we can add a final linear layer that maps each output token to word probabilities (use softmax)

12

Attention

• Each input token is processed in the same way:

ð¦ð = ð´ð¡ð¡ð(ð¥ð,ð) – analyse only one for now.

• Intuition: ð¥ð looks at all ð§ð and decide what is relevant.

ð§1 ð§2 … ð§ð ð¥1 ð¦1

13

Attention

• We do this by introducing three functions:

• A query function ð:ℝð → ℝð

• A key function K:ℝð → ℝð

• A value function V:ℝð → ℝð

ð§1 ð§2 ð§ð

• They are used like this:

…

• ðð = ð(ð¥ð)

• ðð = ð¾(ð§ð)

ð1 ð£1 ð2 ð£2 ðð ð£ð

• ð£ð = ð(ð§ð)

ð¥1

ð1

• Naming: we will use queries to find keys and retrieve values.14

Attention

• Compute similarities between keys and values using a dot product.

• Intuition: large if key is similar to query.

ðð,ð = √ð 1ððððð ∈ ℝ

ð§1 ð§2 ð§ð

ð¥1

15 …

ð1 ð£1 ð2 ð£2 ðð ð£ð

ð1

ð11 ð12 ð1ð

Attention

• Intuition: interpret ðð,ð as weights to combine their values ð£ð.

• Problem: ðð,ð ∈ ℝ, unbounded

• Solution: ðð,ð = softmaxj(ðð,1,…,ðð,ð)

ð§1 ð§2 ð§ð

• Normalises: 0 ≤ ðð,ð ≤ 1

• Weights sum to 1: σð ð=1 ðð,ð = 1

ð¥1

16 …

ð1 ð£1 ð2 ð£2 ðð ð£ð

ð1

ð11 ð12 ð1ð

ð11 ð12 ð1ð

Attention

We can now compute the output as the weighted sum of values:

ð ð¦ð = ෍ðð,ðð£ð

ð=1ð§1 ð§2 ð§ð

• ðð,ð are the attention weights.

ð¥1

17 …

ð1 ð£1 ð2 ð£2 ðð ð£ð

ð1

ð11 ð12 ð1ð

ð11 ð12 ð1ð

ð11ð£1 + ð12ð£2 + + ð1ðð£ð =

ð¦1

Attention Weights

18 Bahdanau et al, “Neural machine translation by jointly learning to align and translate”, ICLR 2015

Attention (to) Details

• The three functions for query, key, and value are linear functions, of appropriately sized matrices.

• Query function ð ð¥ = ð¸ð¥

• Key function K ð§ = ð²ð§

• Value function V ð§ = ð½ð§

• All operations (except softmax) can be implemented by matrix-vector (or tensor) products: fast.

Attn ð,ð¾,ð = softmax ðð¾ð

√ð ð

• Attention is permutation-equivariant: changing the order of inputs ð¥ð will simply change the order of outputs ð¦ð.

19

Attention (to) Details

• Permutation equivariance is sometimes unwanted: e.g. word-order matters in NLP.

• Idea: add a signal to the inputs, that identifies the order: ð¥ð′ = ð¥ð + ð(ð)

• ð:ℕ → ℝð can be simply learned by the network, or handcrafted: e.g. combining sin and cos frequencies sampled at ð.

20

Attention

What if we do not have a conditional task?

ð§1 ð§2 ð§ð

ð¥1

21 ð1 ð£1 ð2 ð£2 ðð ð£ð

ð1 ð11ð£1 + ð12ð£2 + … + ð1ðð£ð = ð¦1 ð¥2 ð2 ð21ð£1 + ð22ð£2 + … + ð2ðð£ð = ð¦2

ð¥N ðN ðð1ð£1 + ðð2ð£2 + … + ðððð£ð =

ð¦N

… …

Self-Attention

We simply predict the keys and values also from the input.

ð1 ð£1 ð2 ð£2 ðð ð£ð

ð¥1

ð1 ð11ð£1 + ð12ð£2 + … + ð1ðð£ð = ð¦1 ð¥2 ð2 ð21ð£1 + ð22ð£2 + … + ð2ðð£ð = ð¦2

ð¥N ðN ðð1ð£1 + ðð2ð£2 + … + ðððð£ð =

ð¦N

22

… …

(Self-)Attention

• Without positional encoding: permutation invariant.

• Complexity: ðª(ð2) in the number of input tokens.

• What to pay attention to is learned automatically.

• Attention is thus somewhat interpretable (Lecture 09).

23

Multi-Head (Self-)Attention

Similar to convolutions, by applying several different filters per layer, we can use multiple SA heads simultaneously.

ð¦(ℎ) = SAttn ð² ℎ ð¥,ð½ ℎ ð¥,ð¸ ℎ ð¥ , 1 ≤ ℎ ≤ ð»

• Each attention head has its own weights ð² ℎ , ð½ ℎ , ð¸ ℎ .

• Results are combined with a linear projection ð¾ ∈ ℝð»ð×ð.

• By stacking all outputs: ð¦ = ð¾ ð¦ 1 ð¦ 2 …ð¦ ð» ð

24

Transformer

• Built from several transformer blocks.

• Each block contains:

• Multi-Head Attention.

• Residual connection ð¦ = ð¥ + MHA(ð¥).

• Normalisation.

• Feed forward (fully connected) layer (operates per token).

25

Residual Connections

• Idea: ð¦ = ð(ð¥) means that ð needs to learn to pass on all necessary information to the following layer.

• It can be easier to only learn the changes in the representation: ð¦ = ð ð¥ + ð¥.

• Bonus: gradients flow much easier through the network.

• Residual blocks are now in almost all architectures CNNs and Transformers alike.

26

Normalisation

• Consider a single linear layer with ReLU ð¦ = max 0,ðð¥ + ð .

• After initialisation with random (normal) noise, ð and ð can sometimes be hard to learn.

• For example:

• If ð¥ are very close to 0, ð needs to be very large.

• If ð¥ is very negative -\> large ð to avoid 0 gradient from ReLU.

• Etc.

• Idea: just normalise ð¥ so that it is “well-behaved” for optimisation.27

Normalisation

• Typical training happens in mini-batches where we pass ðµ samples through the model together.

• Gradients are computed using the full batch.

• More stable than using only a single sample.

• Much faster than computing the gradient using the whole dataset.

• Let’s use the batch statistics to normalise outputs of layers\!

28

Batch-Normalisation

Ioffe and Szegedy, 2015

• Input: ð¥ ∈ ℝðµ×ð (a batch of ðµ vectors in ℝð)

• Output: ð¦ = BN ð¥ ∈ ℝðµ×ð

• Mean: ð = 1ðµσð=1 ðµ ð¥ð ∈ ℝð

• Variance: ð2 = 1ðµσð=1 ðµ ð¥ð − ð 2 ∈ ℝð

• Normalisation: ð¥ð,ð′ = 1

ðð2+ð(ð¥ð,ð − ðð)

• Learnable (ð¾,ð½ ∈ ℝð) rescaling: ð¦ð,ð = ð¾ðð¥ð,ð′ + ð½ð 29

Batch-Normalisation

• Learning ð¾ = ð2,ð½ = ð turns BN into an identity function.

• Usually requires reasonably sized batches to compute stable statistics.

• Depends on training statistics\! For testing: use fixed statistics (exponential moving average) from train-set.

• Usually: after Fully Connected or Convolutional layers, and before nonlinearity.

• Idea: ReLU will 0-out about 50% activations.

30

Batch-Normalisation

• Makes deep networks much easier to train.

• Improves gradient flow.

• Allows higher learning rates, faster convergence.

• Networks become more robust to initialization.

• Acts as regularization during training.

• Zero overhead at test-time: statistics are fixed and can be fused with previous layer\!

• Behaves differently during training and testing: very common source of bugs\!

31Slide from F Li

Wu and He, “Group Normalization”, ECCV 2018

Other Normalisation Layers

32

Creativity of CV Researchers

• “Show, attend, and tell” (Xu et al., ICML 2015)

Look at image, attend to image regions, produce queston

• “Ask, attend, and answer” (Xu and Saenko, ECCV 2016) “Show, ask, attend, and answer” (Kazemi and Elqursh, 2017)

Read text of question, attend to image regions, produce answer

• “Listen, attend, and spell” (Chan et al., ICASSP 2016)

Process raw audio, attend to audio regions while producing text

• “Listen, attend, and walk” (Mei et al., AAAI 2016)

Process text, attend to text regions, output navigation commands

• “Show, attend, and read” (Li et al., AAAI 2019)

Process image, attend to image regions, output text

• “Show, attend, and interact” (Qureshi et al., ICRA 2017)

Process image, attend to image regions, output robot control commands

33 Slide adapted from J Johnson

Vision Transformers

An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale, A Dosovitskiy et al., 2021

• Split image into 16x16 patches.

• A linear layer that maps each patch to a vector (token).

• Add 2D positional encoding.

• Add one extra token to the sequence of 256. This token will in the end map to the class distribution.

• Train a transformer on sequences of length 257.

34

Vision Transformer

35

Vision Transformer

• Still seems to learn reasonable “filters” in the first layer.

• Trained with ADAM optimiser.

Tricks

• Checkpoint averaging

• Residual dropout

• Label smoothing

36

Attention Visualisation

• Attention weights are single scalars per token than sum to 1.

• We can visualise them as a heat-map and overlay them over the image.

• Seems to align with human intuition about what is important in an image.

37

Positional Encoding

• ViT learns the positional encoding from scratch, instead of hand-crafting it.

• The learned embeddings have a strong local similarity.

• They can thus identify where a token comes from in the image.

38

Data

• ViTs benefit from very large datasets.

• BiT is a CNN (ResNet).

• Transfer learning becomes even more important\!

39

Transfer Learning

• Train on a large dataset for some (related) task.

• Then fine-tune on your task that has less data.

• Fine-tuning usually with a lower learning rate or some layers frozen.

• Intuition: learned weights for another task often still much better than random initialisation.

• Evidence: first layer filters almost always look the same.

40

The Encoder-Decoder Transformer

41

Image source

Encoder block

42

Image source

Encoder block

Encoder self-attention

All tokens interact with each other

Image source

43

Encoder block

Residual connection & Layer normalization

All tokens interact with each other

Image source

44

Encoder block

MLPs independently on each token (no interaction)

Residual connection & Layer normalization

All tokens interact with each other

Image source

45

Encoder block

MLPs independently on each token (no interaction)

Residual connection & Layer normalization

All tokens interact with each other

Image source

46

Decoder block

• Similar to encoder block

• Input defined/learned tokens are pre- • Encoder-Decoder attention

• Queries previous ð¸ layer from of the the output decoder of the • Keys output ð² of and the values encoder ð½ from the • Every attends all positions position over in in the the input decoder sequence

• Often also called “cross attention”

47

ConvNeXt? – Probably not

A ConvNet for the 2020s, Liu et al., 2022

• Main cha
