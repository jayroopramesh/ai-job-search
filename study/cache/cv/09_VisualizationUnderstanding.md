# Computer Vision — Visualization & Understanding
> Source: Google Drive file 1PLgDc_gyA88SeH_ytGzHlFoWndEfJyTk · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Visualizations and Explanations

Computer Vision – Lecture 09

1

Further Reading

• Slides from L Fei-Fei.

• CVPR’18 Tutorial on Interpretable ML for CV

• Many posts on https://distill.pub

2

3

Which insights can we derive?

4

Does the orangutan know what a hammer is?

• Does she know hammering (Task)?

• Can she hammer (Task)?

• Does she know what a hammer is (Concept)?

YesNo Maybe?

5

Clever Hans

• 1895-1916 German horse that was doing arithmetic.

• Formal investigation: horse was watching the reactions of his trainer.

• Trainer was entirely unaware that he was providing such cues.

• -\> Clever Hans Effect.

6

• Benchmark: PASCAL Visual Objects in Context (2004 - 2012)

• 20 classes:

person, bird, cat, cow, dog, horse, sheep, aeroplane, bicycle, boat, bus, car, motorbike, train, bottle, chair, dining table, potted plant, sofa, tv/monitor

• 10,000 images with 25k objects

The PASCAL Visual Object Classes Challenge: A Retrospective Everingham, M., Eslami, S. M. A., Van Gool, L., Williams, C. K. I., Winn, J. and Zisserman, A. International Journal of Computer Vision, 111(1), 98-136, 2015

Example: Image Classification

7

Evaluation – test on unseen data

“AI” • horse

• person

89.496.4 92 94 92.290.587.377.18 100

95.2

91.384

94.194.693.495.2mean

bicycle bird 78.174.9boat

bottle bus car cat chair cow dining table dog horse motorbike person potted plant

accuracy

sheep sofa 91.984.294.3 90

80706050403020100Jincao Yao Cross-layer sparse atrous convolution network http://host.robots.ox.ac.uk:8080/leaderboard/displaylb\_main.php

Does the model know what a horse is?

• Evaluation accuracy is high - does that mean yes?

average heatmap for all horse images

• No\! It uses spurious correlations: many horse images have a copyright notice in this dataset

Analyzing Classifiers: Fisher Vectors and Deep Neural Networks Sebastian Bach, Alexander Binder, Grégoire Montavon, Klaus-Robert Müller, Wojciech Samek

9 International Conference on Computer Vision and Pattern Recognition, 2015

input heatmap for “horse”

Explainability

• Helps to uncover biases in data and models.

• Additional tool beyond test set evaluation.

• Another layer of verification.

• Help to create trust.

• Allows for non-expert interaction.

• Can lead to new insights.

• Is in the law: (GDPR Art. 13,14,22) “the right for explanation”. 10

GDPR, Art. 13.2.f

Ke Jie vs. AlphaGo

Explanations

Recipient

Content

Explanations need to

Explanations provide adapt to the recipient

different types of of the information.

information.

• Developers

• Representations

• Domain experts

• Individual predictions

• Users

• Behaviour

• Examples

11 Purpose

Explanations differ based on use-cases.

• What question is answered by the explanation?

• What is the

Towards explainable artificial intelligence explanation used for? Samek Wojciech, and Klaus-Robert Müller Explainable AI: interpreting, explaining and visualizing deep learning Springer, Cham, 2019

Taxonomy - Approaches

Post-Hoc Analysis

Transparent Models

Learned Explanations

Explanations are derived The model is constructed The model is trained to from a fixed, pre-trained such that (some) deliver explanations model via analysis.

mechanisms have

together with predictions. semantic meaning.

• No impact on • Explanations can be very performance

• Does not need post-hoc

semantic

• Difficult

• Explanations are often local around predictions

• Main focus today\!

analysis

• Task-specific architecture

• Can affect performance

• Might need meta- explanations

• Can affect performance

12

Post-Hoc Analysis: First Layer

First-layer filters from ResNet18 ( \[7 × 7 × 3\] filters):

First-layer learned features include basic elements, such as edges, blobs, colors, etc.

Deeper layers depend on the features computed in the layers before: hard to directly understand the weights.

13

Second Layer

The second layer has 64 3x3 convolutions, each operates on 64 channels.

Not very interpretable\!

14

Last Layer

• ResNet18: last layer 512x1000 (1000 class output)

• Dimensionality reduction with PCA (use the first 2 principal components)

• Observe groupings.

15

Post-Hoc Analysis

• So far: we have looked at the learned weights after training.

• This can show what the model has learned.

• We also want to understand what the model does with its inputs.

• We can also look at activations (=outputs of layers) instead.

• For that, we need to input data.

• Use data that was unseen during training: we want to understand generalisation.

16

Last Layer Activations

• Compute inputs to the last layer of validation set images.

• Compute PCA.

• Visualise embedding with class labels.

• Last layer: linear+softmax, so we want linear separability.

17

t-SNE Embedding

• PCA gives us a linear projection from a high dimensional space to 2 dimensions for visualisation.

• There are non-linear embedding techniques: e.g. t-SNE.

• Nicer plots, but less interpretable embedding.

• Further reading.

Hinton, Geoffrey; Roweis, Sam. Stochastic neighbor embedding. NeurIPS, 2021

18

Comparisons

19

Comparisons

20

Comparisons

21

ResNet20 – 92.6% Accuracy ResNet56 – 94.4% Accuracy

Comparisons

22

ResNet20 – 92.6% Accuracy ResNet56 – 94.4% Accuracy

Comparisons

• Large visual difference to random network – we have clearly learned something\!

• Differences between trained networks small, and hard to interpret.

• Careful: t-SNE uses randomness – every run will show you a different embedding.

23

Input Reconstruction

• To understand what a model has learned, we can also search for an input that maximised a class probability.

• Search with gradient ascent on the image.

• But: generates adversarial example.

24

Input Reconstruction - Tricks

• Regulariser: smoothness (total variation = L1 on image gradients).

• Image jittering: randomly move image by some pixels at every step.

• Better regularisers: better reconstructions.

• Works also for intermediate neurons.

• https://distill.pub/2017/feature-visualization/

25

Understanding Samples

• We can also try to understand the decision process for a single sample.

• ResNet50: “Dingo” (22%)

• AlexNet : “Mountain Lion” (89%)

• ConvNeXt\_Large: “Dingo” (66%)

26

Dingo

https://en.wikipedia.org/wiki/Dingo

27

Black-Box Visualisations

• No access to model itself, observe only input/output.

• Idea: make changes to the input and observe what happens.

• Occlusion method (Zeiler & Fergus, 2015)

• Occlude a part of the image and measure the change in response.

• The bigger the change, the more important the occluded region was.

• Measure the change in target/predicted class probability (other classes can change too, but do not matter)

28

Occlusion Method

29

ResNet50: “Dingo”

Occlusion Method

30

ResNet18: “Dingo”

Occlusion Method

31

ResNet18 (random init.): “spiny lobster”

Occlusion Method

• Depends on this size of the occlusion.

• What do we fill in when we occlude? (0, random noise, avg, …)

• Is a square occlusion meaningful?

• Slow: needs many network evaluations – one for each patch.

Several improvements, for example:

• Fong, Ruth C., and Andrea Vedaldi, Interpretable explanations of black boxes by meaningful perturbation ICCV, 2017

32

White-Box Visualisations

• We do have access to the weights and computations inside the model.

• How can we use this information to extract understanding.

• Idea: use the gradient magnitude ∇ð¥ð ð¥ 1.

• “In which direction does the input need to change to affect the output the most.”

33

Gradient Method

34

AlexNet: “Mountain Lion”

Gradient Method

35

AlexNet (random init)

Gradient Method

36

ResNet18 “Dingo”

Gradient Methods

• Not limited to last layer.

• Several improved variants.

• Mainly:

• Ideas how to deal with ReLU and pooling layers.

• Average gradients over multiple slightly noised version of the image.

• How can we benchmark visualisation techniques?

37

Attribution Methods

• Visualisation techniques that highlight which input pixels are important are often called Attribution Methods or Saliency Methods.

• The (un) reliability of saliency methods, Kindermans, Hooker, et al., 2017

• A benchmark for interpretability methods in deep neural networks, Hooker et al., 2019

38

ROAR: Remove and Retrain

• Run your attribution method on the train & test set.

• For each image: sort all pixels by attribution performance.

• Delete X% of most important pixels.

• Retrain your network on this new data.

• Measure performance change on test set.

• If you removed many critical pixels, the performance will be lower.

• Need for re-training: images look very different after deletion.

39

ROAR

10% removed

90% removed

40 Image source

A benchmark for interpretability methods in deep neural networks, Hooker et al., 2019

ROAR

• Gradient Image works even slightly worse than randomly deleting pixels.

• Ensemble approaches are much better: average the gradients over many small perturbations (add noise to the image).

41

Sanity Checks

Sanity Checks for Saliency Maps, Adebayo et al, 2018.

• Test 1: randomising the model weights should affect the attribution method. (Otherwise we are not visualising what the model has learned)

• Test 2: Train another model on the same data but random labels. This should also affect the visualisations.

42

Attention

• Self-Attention on 14x14 patches means attention weights are a matrix of size 196x196 (or equiv. 14x14x14x14)

• For every token, 14x14 attention map for each layer (12). centre token (7,7):

top left (1,1):

middle right (12,6):

43

Visualising Attention

• Many choices: layer, token, MHA head.

• Trained models seem to do the “right thing”.

• Last layer looks task focused: most attention is on the object independent of which token we are looking at.

• Often difficult to choose what to visualise, some choice will always look similar to what you are looking for → confirmation bias.

44

Taxonomy - Approaches

Post-Hoc Analysis

Transparent Models

Learned Explanations

Explanations are derived The model is constructed The model is trained to from a fixed, pre-trained such that (some) deliver explanations model via analysis.

mechanisms have

together with predictions. semantic meaning.

• No impact on • Explanations can be very performance

• Does not need post-hoc

semantic

• Difficult

• Explanations are often local around predictions

• Main focus today\!

analysis

• Task-specific architecture

• Can affect performance

• Might need meta- explanations

• Can affect performance

45

Example: Transparent Models (1)

In the first quarter, Buffalo trailed early as Chiefs QB Tyler Thigpen completed a 36-

Who kicked the longest field yard TD pass to RB Jamaal Charles. The Bills responded with RB Marshawn Lynch getting a 1-yard TD run. In the second quarter, Buffalo took the lead as kicker Rian

goal in the second quarter?

Lindell made a 21-yard field goal. Kansas City answered with Thigpen completing a 2- yard TD pass to TE Tony Gonzalez. Buffalo regained the lead as Lindell got a 39-yard field goal, while rookie CB Leodis McKelvin returned an interception 64 yards for a touchdown. The Chiefs struck back with kicker Connor Barth getting a 45-yard field goal, yet the Bills continued their offensive explosion as Lindell got a 34-yard field goal, along with QB Trent Edwards getting a 15-yard TD run. In the third quarter, Buffalo continued its poundings with Edwards getting a 5-yard TD run, while Lindell got himself a 38-yard field goal. Kansas City tried to rally as Thigpen completed a 45-yard TD pass to WR Mark Bradley, yet the Bills replied with Edwards completing an 8-yard TD pass to WR Josh Reed. In the fourth quarter, Buffalo pulled away as Edwards completed a 17-yard TD pass to TE Derek Schouman.

• Decompose the problem in smaller parts that can be interpreted individually

• Increases interpretability of the whole system

• Some steps might need further decomposition/explanation 46

Neural Module Networks for Reasoning over Text Gupta, N., Lin, K., Roth, D., Singh, S., & Gardner, M. ICLR 2019

Example: Transparent Models (2)

47 Gupta, Tanmay, and Aniruddha Kembhavi. "Visual programming: Compositional visual reasoning without training.“, CVPR 2023, best paper award

Hendricks, L. A., Akata, Z., Rohrbach, M., Donahue, J., Schiele, B., & Darrell, T. Generating visual explanations European Conference on Computer Vision, 2016

Example: Learned Explanations

• The model predicts an explanation

• Training contains explanations together with input-output pairs

• Explanation needs to be both:

• input specific

• output specific

• How do we explain the explanation?

48

<http://cs231n.stanford.edu/slides/2023/lecture_12.pdf>   
<https://interpretablevision.github.io/index_cvpr2018.html>   
<https://distill.pub/>   
<https://distill.pub/2016/misread-tsne/>   
<https://cs.nyu.edu/~roweis/papers/sne_final.pdf>   
<https://github.com/google-research/google-research/blob/master/interpretability_benchmark/READ
