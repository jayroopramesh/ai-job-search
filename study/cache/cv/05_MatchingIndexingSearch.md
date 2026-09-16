# Computer Vision — Matching, Indexing & Search
> Source: Google Drive file 1Q9jP0aO7dOZF6kX3kkPIX-rF29t2cuEt · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Matching Indexing Search

Computer Vision – Lecture 05

1

Further reading

• Slides from A Vedaldi

• Slides from S Lazebnik

• Slides from J Johnson and D Fouhey

2

So far

• Lectures 02 – 04:

• Various operations a single image

• Usually, we are dealing with more than one image.

• We want to relate one image to another in various ways.

• Points

• Transformations

• Images

3

What are the three most important problems in computer vision?

1\. Correspondence

2\. Correspondence

3\. Correspondence

4

Takeo Kanade (金出 武雄)

Image source

Correspondences

• Given two images of the same scene

• Find corresponding points

5

Correspondences

• Simply subtracting the images does not work

6

Correspondences

Point correspondences estimated by a classic algorithm: SIFT

7

Scale Invariant Feature Transform (SIFT)

Algorithm overview:

1\. Keypoint detection 2. Keypoint description 3. Keypoint matching

8

Keypoints

• What makes a good keypoint?

• Easy to find in other images\! Intuitions:

• A: untextured regions are difficult to reidentify

• B: good keypoint

• C: stable under viewpoint changes, but multiple occurrences

• D: hard to find exact point along the edge

9

A .

B .

C D

.

.

Image Transformations - again

• We know how to model rotation and translation:

ð ð¥,ð¦ = ð´

ð¥ð¦1

\= ðð11 21 ðð12 22 ðð13 23

ð¥ð¦1 This corresponds to

• Rotation around the optical axis

• Translation along the optical axis

10

Optical Axis

• Connects camera image plane. with the the centre centre of the of the • Camera axis its centre.

rotates rotation the image around around the optical axis

• Camera axis its centre.

scales translation the image along around the 11

Camera Motion vs. Image Motion

• Relating how 3D camera motions change the image is important to model viewpoint changes.

• We know: rotation and translation around/along the optical axis maps to affine 2D transformations.

• What about other viewpoint changes?

12

Homography

• We will assume that everything we see lies on a single 3D plane.

• A circle on the 3D plane maps to an ellipse in the image.

• We will see the mathematical derivation in lecture 16.

13

Image source

Homography

14

Homography

• We that in one are maps image looking 4 points to for another a (from transformation image.

a 3D plane) ð´1 ð´2ðµ1 ðµ2

• ð ð´ð = ðµð, ∀ð ∈ 1,2,3,4

• All positions.

8 points can be in arbitrary 2D ð´4

ð´3 ðµ4 ðµ3 • Degrees of freedom: 8 (2 equations for every 2D point pair)

15

Homogeneous Coordinates II

Geometric interpretation:

• We define an equivalence class:

ð¥ð¦1

z

ðð¥,ðð¦,ð ð ð¥= ð

ð¦,ð ∈ ℝ ∧ ð ≠ 0 1

0,0,1 ð

y ð¥,ð¦,1 ð

• This embeds ℝ2 in ℝ3.

• We identify the 2D point ð¥,ð¦ T with the class \[ ð¥,ð¦,1 T\].

0,0,0 ðx 16

Homogeneous Coordinates II

• Given a point in homogeneous coordinates

ð¥ð¦ð§ we can compute its 2D counterpart as ð¦/ð§

ð¥/ð§ if ð§ ≠ 0.

• Points with ð§ = 0 have a special meaning: they lie at infinity (later).

• Now we can describe homographies.

17

Homography

A coordinates homography ð of ð» the is a form

transformation of 2D homogeneous ð ð = ð»

ð¥ℎ11 ℎ12 ℎ13 ð¦ð§ ℎ21 ℎ22 ℎ23 ℎ31 ℎ32 ℎ33 ð¥= ð¦ð§

• Since points, homogeneous this matrix has coordinates only 8 degrees are equivalence of freedom: classes of ð»ð = \[ðð»ð\]

• We right often element rescale is 1.

the matrix by ð = ℎ133 such that the bottom

18

Homography

• When applying a homography, make sure renormalise points to treat them as 2D coordinates ð¦/ð§

ð¥/ð§ \!

• A homography is uniquely defined by 4 point- correspondences if no 3 points lie on the same line.

• Naturally, also images can be transformed with a homography. (Lecture 02)

19

ð´Estimating Homographies 1 ð´2ð»\[ð´ð\] = \[ðµð\], ∀ð ∈ 1,2,3,4

• Two equations per correspondence

ð´4 ð´3 ðµð¥,ð = ℎℎ3111ð´ð´ð¥,ð ð¥,ð + + ℎℎ1232ð´ð¦,ð ð´ð¦,ð + + ℎ13

ℎ33 ðµ1 ðµ2

ðµ4 ðµ3 , ðµð¦,ð = ℎℎ2131ð´ð¥,ð ð´ð¥,ð + + ℎ22ℎ32ð´ð¦,ð ð´ð¦,ð + + ℎ23

ℎ33

Multiplying by the denominator:

ðµðµð¥,ð ð¦,ð(ℎℎ3131ð´ð´ð¥,ð ð¥,ð + + ℎℎ3232ð´ð´ð¦,ð ð¦,ð + + ℎℎ3333 ) = = ℎℎ2111ð´ð´ð¥,ð ð¥,ð + + ℎℎ1222ð´ð´ð¦,ð ð¦,ð + + ℎℎ13 23

20

Estimating Homographies

Homogeneous linear system

−ð´ð¥,1 −ð´ð¦,1 −1 0 0 0 ðµð¥,1ð´ð¥,1 ðµð¥,1ð´ð¦,1 ðµð¥,1 0 0 0 −ð´ð¥,1 −ð´ð¦,1 −1 ðµð¦,1ð´ð¥,1 ðµð¦,1ð´ð¦,1 ðµð¦,1 −ð´ð¥,2 −ð´ð¦,2 −1 0 0 0 ðµð¥,2ð´ð¥,2 ðµð¥,2ð´ð¦,2 ðµð¥,2

⋮ 0 0 0 −ð´ð¥,4 −ð´ð¦,4 −1 ðµð¦,4ð´ð¥,4 ðµð¦,4ð´ð¦,4 ðµð¦,4

ℎ11 ℎ12 ℎ13 ℎ21 ℎ22 ℎ23 ℎ31 ℎ32 ℎ33

\= ð

• ð» is in the null-space of this matrix.

• Finding a non-trivial solution: solve for ð» using SVD.

21

Homography

22

Homography

23

Homography

24

Keypoints

What makes a good keypoint? Keypoints should stable under:

• Perspective changes (homographies).

• Contrast changes.

• Lighting changes.

• Other changes, as much as possible.

25

A .

B .

C D

.

.

Keypoints

• Keypoints on blobs, corners, and high-contrast regions are the most stable.

• We will describe each keypoint through its local neighbourhood (patch).

• If we make the patch small, we can assume mostly simple geometric transformations of the neighbourhood (e.g. homographies)

26

Scale

27

Scale

• To arrive at a good local neighbourhood descriptor, we need to define the size of the neighbourhood.

• This defines the scale of a keypoint.

28

Detecting Scale

29

Scale Space

• We need to define a unique scale for a keypoint: the characteristic scale.

• This turns the problem of finding keypoints into a search across three parameters: location and scale ð¥,ð¦,ð .

• We will find keypoints with scale by finding local minima in an energy function E ð¥,ð¦,ð .

30

\+

Source: J. Johnson and D. Fouhey

Gaussian ð

Laplacian of Gaussian

ððð¦ð

ððð¥ ð

ð2 ð2ð¦ð

ð2 ð2ð¥ ð

ð2 ð2ð¥ð + ð2

ð2ð¦ð

Laplacian of Gaussian

• This is a blob detector.

• It will have minima in space and scale when the filter “matches” a blob

• We will analyse why in 1D.

32

2D LoG filter

Laplacian of Gaussian 1D

• Laplacian of Gaussian is the spatial 2nd order derivative of a Gaussian.

• LoG ð¥ = − 1ðð2 1 − ð¥2ð2 ð− ð¥2 2ð2

• We will vary ð and convolve a simple signal with the filter.

• To make the output comparable, the response needs to be scaled by ð.

33

Laplacian of Gaussian 1D

\* =

34

Laplacian of Gaussian 1D

\* =

35

Laplacian of Gaussian 1D

\* =

36

minimum over all scales

Laplacian of Gaussian 1D

\* =

37

Laplacian of Gaussian 1D

\* =

38

2D Multiscale Blob Detection

• Convolve image with Laplacian of Gaussian filter at several values of ð.

• Find maxima of squared Laplacian response in space and across scales.

• In practice, this means looking at a 3x3x3 neighborhood in the ð¥,ð¦,ð space. If the center is larger than its 26 neighbours: you found a blob\!

39

Beyond Blob Detection

• Now we can detect blobs and their scale.

• Next, we want to find the orientation of a keypoint.

• This allows us to describe a keypoint invariant to rotation.

40

Keypoint Orientation

• Compute the angles of the local edges around the keypoint. (Sobel)

• Discretise into 45 deg. increments.

• Pick the most common direction as the overall orientation.

41

0 2 π Edge directions in the range of the keypoint Discretise angles and chose most common

Adapted from S. Lazebnik

SIFT Descriptor

• Compute a descriptor for a keypoint.

• A descriptor is a vector that characterises the local information around the keypoint so that it can be found in other images.

• Idea: use edge directions again (invariant to brightness changes, equivariant to rotation).

• Compute and store local edge histograms.

42

SIFT Descriptor

• Compute edge orientations and global orientation.

• Rotate all edges so that the global orientation is “up”.

• Split the local area around the keypoint into 4x4=16 regions.

• Compute edge histograms (8 directions) for each region.

• Concatenate histograms: descriptor 128 dimensional vector.

43

Feature Matching

• Many different strategies.

• Brute force matching:

• For each descriptor in the first image, return the one with the lowest distance (e.g. Euclidean distance).

• Sort all matches by their distance and take the top N.

• Later: better strategies such as RANSAC.

• Idea: check if matches are consistent with a transformation, e.g. homography. This is geometric verification.

44

Correspondences

Point correspondences estimated by a classic algorithm: SIFT

45

Local to Global Matching

• Given an image, we now want to find similar other images.

• We can use feature matching, but this means comparing all image features to all database features: very slow\!

1010 images \* 103 kpts \* 102 dims \* 103 query kpts = 1018ops\! Fastest super-computer: 1000 Peta-FLOPS (=1 sec for every image search)

• Idea: compute a single global descriptor for an image.

• The global descriptor should capture the local information form the keypoints.

46

K-means Clustering

• Divide the space into ð¾ clusters ð®.

• Minimise the sum of squared distances of points in a cluster.

argminð® ð¾ ෍ð=1|ð1ð| ð¥,ð¦∈ð෍ð

ð¥ − ð¦ 2

• We can treat the cluster assignment as a category for the point.

47

Visual Words

• Compute SIFT features on a large image dataset.

• Compute ð¾-means clustering and assign each feature to one of ð¾ “classes”.

• An image can now be described with a histogram of feature classes it contains.

• This is a reduction in descriptor size per image from \#features\*\#dimensions to ð¾.

48

Example

49

Slide from A Vedaldi

Bag of Visual Words

• When computing the histogram, it does not matter where each feature comes from in the image.

• This is similar to classic text-based retrieval systems: count how often each word appears in a document. Documents on similar topics have similar statistics.

• With large ð¾ (and a large dataset) the image descriptor is usually sparse (i.e. most entries are 0)

• Sparse vectors can be stored and compared efficiently: only store/compare non-zero elements.

50

Bag of Visual Words

51

Bag of Visual Words

52

Image Retrieval

1\. Given a query image, compute keypoints and descriptors. 2. Find keypoint labels from pre-computed (k-)means. 3. Compute bag of visual words for the query. 4. Compare BoW query to all database BoWs and retrieve top M. 5. Optional: perform additional (sl
