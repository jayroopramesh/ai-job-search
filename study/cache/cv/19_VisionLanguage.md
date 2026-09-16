# Computer Vision — Vision & Language
> Source: Google Drive file 1bMpf72fiM7Lb8PPrezaVBz4zLbhFOTQB · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Vision & Language

Computer Vision – Lecture 19

1

Further Reading

• Slides from J Redmon

• Slides from V Ordóñez-Román

• Slides from J Mu

2

What is Vision and Language?

Anything at the intersection of Computer Vision and Natural Language Processing. Systems and models that depend a little bit on both.

• Computer Vision: How do we teach machines to process, represent and understand images? E.g. to recognize objects in images.

• Natural Language Processing: How do we teach machines to process, represent and understand text? E.g. to classify or generate text.

3

Word Representations

dog

0\[1 0 0 0 0 0 0 0 0 0 \]

cat

1\[0 1 0 0 0 0 0 0 0 0 \]

person

2\[0 0 1 0 0 0 0 0 0 0 \]

holding

3\[0 0 0 1 0 0 0 0 0 0 \]

tree

4\[0 0 0 0 1 0 0 0 0 0 \]

computer

5\[0 0 0 0 0 1 0 0 0 0 \]

using

6

\[0 0 0 0 0 0 1 0 0 0 \] one-hot encodings

4

Word Representations

• Represent each word as a vector.

• Learn the vector representation together with the task.

• Problem: English has 170,000 words in current use, with an additional 47,000 obsolete words.

• Problem: word variations, typos, new words, other languages, etc.

5

Issues with Word based Tokenization

• Hard for other languages that do not use spaces in-between words.

• Word tokenization can also be bad for languages where the words can be “glued” together like German or Turkish.

• 555 = fünfhundertfünfundfünfzig.

• Infeasible to have a word embedding for every number in the German language.

• It is problematic to handle words that are not in the vocabulary e.g. a common practice is to use a special \<OOV\> (out of vocabulary) token.

6

Words to Tokens

• Instead of splitting by words, learn the splitting from data.

• Budget: ð Tokens.

• Target: find assignment of strings to tokens that minimizes the number of used tokens to represent all data.

• Substrings that occur often will be represented by a single token.

7

Solution: Sub-word Tokenization

• Byte-pair Encoding Tokenization (BPE)

• Start from small strings and based on substring counts iteratively use larger sequences until you define a vocabulary that maximizes informative subtokens. That way most will correspond to words at the end.

• Byte-level BPE Tokenizer

• Do the same but at the byte representation level not at the substring representation level.

8

huggingface/tokenizers

Tokenization used in GPT-4 https://platform.openai.com/tokenizer

The cat is in the house The geologist made an effort to rationalize the

explanation

fünfhundertfünfundfünfzig (555 – German)

9

Η γάτα είναι στο σπίτι (The cat is in the house – Greek)

Tokenization used in GPT-4o https://platform.openai.com/tokenizer

The cat is in the house The geologist made an effort to rationalize the

explanation

fünfhundertfünfundfünfzig (555 – German) Η γάτα είναι στο σπίτι (The cat is in the house – Greek)

10

Tokenization used in GPT-4 https://platform.openai.com/tokenizer

深層学 (deep learning - Japanese)

কেমন আছেন (how are you – Bengali) வணககம (hello – Tamil)

11

Le chat est dans la maison (the cat is in the house - French)

Tokenization used in GPT-4o https://platform.openai.com/tokenizer

Le chat est dans la maison

深層学 (deep learning - Japanese) (the cat is in the house - French)

কেমন আছেন (how are you – Bengali) வணககம (hello – Tamil)

12

Language Models

• 2 types of transformer architectures:

• Encoder transformer: Encode a sequence into a fixed-size representation. e.g. ViT, BERT, …

• Decoder transformer: Decode a fixed-size representation into a sequence. e.g. GPT-3

• Can be used together (e.g. T5) or separately (GPT).

13

Attention is all you need

• Encoder-Decoder

• Decoder needs masking to only look at previous tokens.

• Predict next token probabilities.

• Often: cross attention in decoder.

14 Vaswani et al. “Attention Is All You Need”, 2017

Masked Language Modelling

• Train self-supervised: input recovery.

• Mask words from the input.

• Fill in the blanks.

• GPT-4: train on 13T tokens (ca. 50TB of text\!)

• This model itself is not very useful. It can only generate text.

15

Brown, Tom, et al. "Language models are few-shot learners”, 2020

Generation (GPT-3)

16

Chung, Hyung Won, et al. "Scaling instruction-finetuned language models.“, 2022

Instruction Tuning (e.g. FLAN-T5)

17

source Instruction Tuning (e.g. OPT-IML by Facebook)

18

ChatGPT

19 Ouyang, Long, et al. "Training language models to follow instructions with human feedback, 2022

Step by Step: Train a Reward Model that learns from Human Ratings e.g. from 1 to 520 source

source

Step by Step: Train the LM to generate text that gets high reward but still produces stuff that makes sense

21

Direct Preference Optimization

22 img source Rafailov, et al., NeurIPS’23

source

Jailbreaks

23

Jailbreaks

24

Referring Expressions

• Referring expressions have been studied since the 70’s.

• Attributes: color, orientation, location, relative locations, size modifiers.

• Single and multiple objects.

• Early work analyzed simpler synthetic images

• Recent work has moved to realistic scenarios.

25

Referring Expression

TUNA Corpus van Deemter et al 2006

Size Corpus Mitchell et al 2011 \[96 scenes\]

GenX Corpus FitzGerald et al 2013 \[269 scenes\]

26

GRE3D3 Corpus

Viethen and Dale 2008 \[20 scenes\]

Typicality Corpus Mitchell et al 2013 \[35 scenes\]

Referring to objects

27

The dog in the middle

The gray dog in the middle

The gray dog

Referit Game

28

Player 1

Player 2

Orange bottle on the right

Orange bottle on the right

Referit Game Dataset

29

ReferItGame Dataset 130k Referring expressions for 90k Objects in 19k images

Blue shirt man

Blue guy

Second guy from left

MAttNet: Modular Attention Network for Referring Expression Comprehension Licheng Yu, Zhe Lin, Xiaohui Shen, Jimei Yang, Xin Lu, Mohit Bansal, Tamara L.Berg, 2018

Referring Expression Comprehension

30

Visual Question Answering

• Given image and question, predict answer.

• Answer and question can be anything.

• Evaluation: tricky\!

31 Antol, Stanislaw, et al. "VQA: Visual question answering.“, 2015

Visual Question Answering

32

MDETR: Modulated Detection for Multimodal Understanding

Kamath, Aishwarya, et al. "MDETR: Modulated detection for end-to-end multi-modal understanding, 2021

MDETR: For Question Answering

Vision-and-Language Transformers

35

Vision-and-Language for Navigation

36

Fairness in Vision and Language Models

37

Robotics: Instruction Following

38

Assistive Technologies

39

CLIP

40 Radford, Alec, et al. "Learning transferable visual models from natural language supervision, 2021

Visual Grounding

• Ground text in images and vice versa.

• Region as Text: insert coordinate predictions into the text. “A cat \[10, 25, 204, 400\] on a chair \[120, 359, 200, 300\]”.

• Region as Embedding: learn special embeddings for regions.

• Increases trust, allows verification beyond metrics.

41

GLIP

42 Zhang, Haotian, et al. "Glipv2: Unifying localization and vision-language understanding, 2022

https://towardsdatascience.com/what-are-stable-diffusion-models-and-why-are-they-a-step-forward-for-image-generation-aa1182801d46

Stable Diffusion v2

43

Vision & Language Now

Two options:

• Train a large-scale LVM-VisionLanguageModel (GPT-4o, Gemini, LLaVa,…) that solves all tasks zero-shot.

• Use a large LLM and add some vision capabilities to it by fine-tuning or other means.

44

Multi-Modal Few-Shot Learning

45 Tsimpoukelli, Maria, et al. "Multimodal few-shot learning with frozen language models." 2021

Inference:

Training:

46

Flamingo

Alayrac, Jean-Baptiste, et al. "Flamingo: a visual language model for few-shot learning." 2022

47

48 Alayrac, Jean-Baptiste, et al. "Flamingo: a visual language model for few-shot learning." 2022

Flamingo

Flamingo

49

Model: molmo, source

Pointing to things

50

source

VLM Benchmarks

51

Jailbreak

52

<https://courses.cs.washington.edu/courses/cse455/23wi/>   
<https://www.cs.rice.edu/~vo9/deep-vislang/>   
<http://web.stanford.edu/class/cs224n/slides/cs224n-2023-lecture11-prompting-rlhf.pdf>   
<https://platform.openai.com/tokenizer>   
<https://platform.openai.com/tokenizer>   
<https://platform.openai.com/tokenizer>   
<https://platform.openai.com/tokenizer>   
<https://arxiv.org/pdf/2212.12017.pdf>   
<https://gist.github.com/JoaoLages/c6f2dfd13d2484aa8bb0b2d567fbf093>   
<https://gist.github.com/JoaoLages/c6f2dfd13d2484aa8bb0b2d567fbf093>   
<https://medium.com/@joaolages/direct-preference-optimization-dpo-622fc1f18707>   
<https://www.reddit.com/r/ChatGPT/comments/12uke8z/the_grandma_jailbreak_is_absolutely_hilarious/>   
<https://x.com/goon_nguyen/status/1839130119484645410>   
<https://molmoai.org/#features>
