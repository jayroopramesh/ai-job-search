# Computer Vision — Object Detection
> Source: Google Drive file 1neLIZ61qlSTW8VPDS0hA1dcj774rUdHw · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Object Detection

Computer Vision – Lecture 10

1

Further Reading

• Slides from F Li.

• Slides from A Zisserman.

• Slides from S Lazebnik.

• CVPR 2019 Tutorial.

2

Classification

• So far: one class per image.

• Fixed output size: one image in, one probability distribution out.

• Real world: not that simple.

• Scene understanding:

• what is in the image and where.

• Object categories, instances, identities, properties, activities, relations, …

3

Object detection

Image source 4

Object Detection

• Task: find the location of an object in the image.

• Typically, with a bounding box (ð¥,ð¦,ð¤,ℎ).

• Very often: add class prediction to the bounding box (ð¥,ð¦,ð¤,ℎ,ð).

ð¤

ℎ

(ð¥,ð¦)

5

background background background car

6

Sliding Window

If we have a binary classifier to predict “object” or “background”, we can use it iteratively to detect objects.

Sliding Window

• Exhaustive search over locations.

• Often also search over scale and aspect ratio\!

• Needs to train on a dataset of object vs. background examples.

• What are representative negative examples?

7

Sliding Window

Typical Problems:

• Computational cost

• Occlusion & truncation

• Multiple responses

8

Pedestrian Detection

Dalal & Triggs, CVPR 2005

Objective: detect standing people

• Sliding window classifier

• Train a binary SVM classifier: person or not

• Histogram of Oriented Gradients (HOG) feature

9

Histogram of Oriented Gradients

split into 8x8 px patches

per patch: histogram of gradient directions

10

Image

Dominant gradient

HOG

Examples

11

Image from A Zisserman

HoG as a CNN

Apply edge filters

8x8 average pooling with stride 8

LayerNorm to normalise histograms

Flatten into a single feature vector

12

HoG with SVM

We can interpret the weights of the decision function by visualising their gradient histograms.

Positive weights vote for person, negative weights vote for background.

13

Slide from Deva Ramanan

HoG Summary

• Edges are useful to describe shapes.

• Spatial sub-sampling: invariant to small shifts.

• Grid structure allows spatial comparisons (in contrast to a single descriptor for the whole patch).

• Has been used for many objects afterwards\!

14

Measuring Performance

• Given the ground truth, how do we measure/score predictions?

• Continuous task: it is unlikely that the prediction will exactly match the ground truth.

• Yet, some predictions are better than others.

15

Intersection over Union

Prediction

• The IoU metric is based on area overlap.

• IoU = Area( Area( GT GT ∩ ∪ Pred Pred ) )

Ground truth

• IoU overlap.

is 1 for perfect overlap and 0 for no Union

Intersection

• Often: counting threshold as a positive (e.g. 50% match.

IoU) for 16

Intersection of Union

• High IoU requires tightly fitting predictions.

• Lower IoU allows loose fits.

• Examples

17 Image from Ross Girshick

False Negative

• False negatives are missed predictions.

• Common causes:

• Occlusion

• Truncation

• Small size

• …

False Negative Person on the edge of the image was not detected.

18

False Positives

• Prediction that does not match a GT annotation

• Or, the GT annotation is already “covered” by a better-fitting prediction.

• Common cause: multiple detections for the same object.

19

False Positive

Multiple Objects

• During evaluation we are given a list of ground truth boxes and a list of predicted boxes.

• Per-class evaluation.

• For each GT box, find the best match in the predictions (IoU) and score it.

• Remove this box from predictions.

• Continue with next GT box.

20

Recall: Precision and Recall

• Precision = TP/(TP+FP)

• Recall = TP/(TP+FN)

• Object detection: each predicted box has a confidence.

• Intuition: thresholding the confidence gives us more or less detections.

21

Precision Recall Curves

IoU threshold = 0.5

• Lower confidence threshold gives us more objects but many will be wrong (high

Varying the confidence threshold changes precision and recall recall, low precision).

• Higher confidence threshold yields less objects but they are more likely to be correct (low recall, high precision).

22

Average Precision (AP)

• We want: high precision and recall at all thresholds.

• AP metric: area under the precision recall curve.

• AP high: always good precision and recall.

23

Average Precision

• The metric still depends on the IoU threshold.

• Compute the average over many thresholds.

24

AP(class) = 1

\#thresholds ෍

iou∈thresholdsAP(class,iou)

Thresh=0.5

… …

Thresh=0.7

Thresh=0.9

…

Overall Precision

• To combine AP from different classes, we average again.

AP = \#classes 1

෍ class∈classesAP(class)

• AP is an average, average, average precision.

iou thresholds

classes

precision @ different recall levels

25

Detection Evaluation

• Task: given an image, predict objects as (ොð¥, ොð¦, ෝð¤, ෠ℎ,ð). ð ∈ ℝð¶

• Evaluation: for each image, class ð, IoU threshold ð¡iou • Set of predictions (ොð¥ð, ොð¦ð, ෝð¤ð, ෠ℎð,ðð,ð) (class confidence ðð,ð)

• For each confidence threshold ð¡conf :

• Ignore any boxes with ðð,ð \< ð¡conf.

• For each GT annotation (ð¥ð,ð¦ð,ℎð,ð¤ð):

• find highest IoU prediction

• If IoU ොð¥ð, ොð¦ð, ෝð¤ð, ෠ℎð , ð¥ð,ð¦ð,ℎð,ð¤ð ≥ ð¡iou: TP (remove from predictions) otherwise FN

• Remaining predictions: FP

• This gives us the PR-curve. Compute the area under the curve.

• Compute AP: average over classes and IoU thresholds of area under the PR-curve.

26

Object Detection as Classification

• Inherently unbalanced: many more negatives than positives.

• Background class is visually much more complex than the object.

• Good performance: low false positive rate.

27

Bootstrapping or Self-Training

1\. Create a training dataset of positive and negative patches. 2. Train classifier. 3. Detect objects in training data. 4. Add false positives to training data. 5. Goto 2.

• Automatically includes difficult examples into the training set.

• Also called: hard negative mining.

28

Non-Maximum Suppression

• Close-by patches look similar

• Often: multiple detections for the same object.

• For overlapping boxes: choose the one with highest confidence and remove/down- weigh others.

29

Cascaded Classifiers

• Sliding window detection is slow.

• Many windows are clearly not the object.

• Instead of one slow/big classifier, build a sequence to quickly throw out true negatives.

…

patch Classifier 1 Classifier 2 Classifier N

no car no car no car

30

car maybe? maybe? maybe?

Cascaded Classifiers

• Early classifiers can have low precision but high recall: eliminate easy negatives.

• Cascade from fast, simple classifiers to slower, complex classifiers with lower false positive rate.

• Viola & Jones, 2001: Face detection

31

Slide adapted from A Zisserman

Object Proposals

• Same idea: restrict the number of patches/windows to a better subset.

• Algorithm to suggest proposals for boxes.

• Needs high recall but can be low precision.

• Aim to cover all the objects in the image with a small number of proposals, e.g. 100-1000 per image.

32

Selective Search

Uijlings, van de Sande, Gevers, and Smeulders, IJCV 2013

• hierarchical segmentation

• colour uniformity

• image edges

• ca. 2000 regions / image.

• \> 95% probability of hitting any relevant object in the image

33

Object Detection with CNNs

Let’s build a simple detector:

1\. Compute proposals with Selective Search. 2. For each proposal: feed to CNN classifier (ImageNet trained). 3. If class probability \> 80%: detection. 4. Optional: non-maximum suppression.

34

Simple CNN Object Detection

• ImageNet trained model is not trained to predict background.

• Simple thresholding confidences is not enough.

• Works to a certain degree: “seashore”

35

R-CNN

Girshick, Donahue, Darrel, Malik, 2013

36

R-CNN

SVMsClassify regions with SVMs

SVMs

SVMs

ConvNet

ConvNet

Forward each region through ConvNet

Regions: Search proposals \~2000 Selective Network: trained classes), PASCAL on (21 fine-tuned ImageNet AlexNet classes) pre- on (1000 Warped image regions

Region proposals ConvNet

Final proposal fc7 (4096 with network linear detector: dimensions), regions, SVM activations warp extract classify Input image Bounding to refine box box locationsregression 37

Source: R. Girshick

Bounding box regression

Ground truth box Target offset

Region proposal to predict\*(a.k.a default box, prior,

Loss

Predicted offset reference, anchor)

Predicted box

\*Typically in transformed, normalized coordinates

38

R-CNN

Pros• Much more accurate than previous approaches\!

• Any deep architecture can immediately be “plugged in” Cons

• Not a single end-to-end system

• Fine-tune network with softmax classifier (log loss)

• Train post-hoc linear SVMs (hinge loss)

• Train post-hoc bounding-box regressions (least squares)

• Training was slow (84h), took up a lot of storage

• 2000 CNN passes per image

• Inference (detection) was slow (47s / image with VGG16)

39 Source: S. Lazebnik

Fast R-CNN

Softmax classifier

Region proposals

40 Linear Bounding-box regressors

R. Girshick, Fast R-CNN, ICCV 2015 Source: R. Girshick

Linear + softmax

FCs Fully-connected layers

ConvNet

RoI Pooling layer

Conv5 feature map of image

Forward whole image through ConvNet

Key innovation in SPP-net \[He et al. 2014\]

41 (Conv feature map) Source: R. Girshick

RoIPool Operation (on each Proposal)

ðð¼ = FCN(ð¼)

Region of Interest (RoI)

(Variable size RoI)

RoIPool Operation (on each Proposal)

ðð¼ = FCN(ð¼)

Region of Interest (RoI)

Snapped RoI

(Variable size RoI)

42 (Conv feature map) Source: R. Girshick

RoIPool Operation (on each Proposal)

(Fixed dimensional representation) ðð¼ = FCN(ð¼)

RoIPool transform

Feature value is max over input cells

Transform arbitrary size proposal into a fixed-dimensional representation (e.g., 2x2)

Region of Interest (RoI)

Snapped RoI

(Variable size RoI)

MLP

43 (Conv feature map) Source: R. Girshick

RoI Pooling

44

Image source

Multi-task loss

Loss for ground truth class ð¦, predicted class probabilities ð(ð¦), ground truth box ð, and predicted box ෠ð:

ð¿ ð¦,ð,ð, ෠ð = −logð(ð¦) + ðð\[ð¦ ≥ 1\]ð¿reg(ð, ෠ð)

Regression loss: smooth ð¿1 loss on top of log space offsets relative to proposal

ð¿reg ð, ෠ð = ෍

ð={ð¥,ð¦,ð¤,ℎ}smoothð¿1(ðð − ෠ðð)

softmax loss regression loss

Anchor is an object?

Figure source: J. Johnson 46

Region proposal network (RPN)

Idea: put an “anchor box” of fixed size over each position in the feature map and try to predict whether this box is likely to contain an object

Anchor is an object?

Figure source: J. Johnson 47

Region proposal network (RPN)

Idea: put an “anchor box” of fixed size over each position in the feature map and try to predict whether this box is likely to contain an object

Conv

Figure source: J. Johnson 48

Region proposal network (RPN)

Idea: put an “anchor box” of fixed size over each position in the feature map and try to predict whether this box is likely to contain an object

Anchor is an object?

Conv

Figure source: J. Johnson 49

Region proposal network (RPN)

Introduce anchor boxes at multiple scales and aspect ratios to handle a wider range of object sizes and shapes

Anchor is object? Anchor is object? Anchor is object? Anchor is object?

Faster R-CNN RPN design

Ren, He, Grishick, Sun, 2015

50

Two-Stage Detectors

So far: two-stage detectors.

1\. Create proposals 2. Classify & update/move proposals

Can we do it in one step?

51

J. Redmon, S. Divvala, R. Girshick, and A. Farhadi, You Only Look Once: Unified, Real-Time Object Detection, CVPR 201652

Single Stage Detector: YOLO

Divide the image into a coarse grid and directly predict class label and a few candidate boxes for each grid cell

YOLO – Training Loss

Regression

Object/no object confidence

Class predictionSource: S. Lazebnik

YOLO – Training Loss

Cell i contains object, predictor j is responsible for it

Small deviations matter less for larger boxes than for smaller boxes

Confidence for object

Confidence for no object

Class probability Down-weight loss from boxes that don’t contain objects

(ðnoobj = 0.5) Source: S. Lazebnik

Single vs Two-Stage Detectors

• Single stage is usually faster.

• Two stage is usually better.

• Application dependent: speed vs. accuracy.

55

Detection Transformer (DETR)

N. Carion et al., End-to-end object detection with transformers, ECCV 2020

<http://cs231n.stanford.edu/slides/2023/lecture_11.pdf>   
<https://www.robots.ox.ac.uk/~az/lectures/aims-cv/detection-part1.pdf>   
<https://slazebni.cs.illinois.edu/spring23/>   
<https://feichtenhofer.github.io/cvpr2019-recognition-tutorial/>   
<https://medium.com/@alexeyab84/yolov4-the-most-accurate-real-time-neural-network-on-ms-coco-dataset-73adfd3602fe>   
<http://arxiv.org/pdf/1504.08083.pdf>   
<https://deepsense.ai/region-of-interest-pooling-explained/>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/FA2020/598_FA2020_lecture15.pdf>   
<https://web.eecs.umich.edu/~justincj/slides/eecs498/FA2020/598_FA2
