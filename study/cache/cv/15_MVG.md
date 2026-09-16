# Computer Vision — Multiple View Geometry
> Source: Google Drive file 1-h7Ds6o7kzHbN4_ClufJuJsglCfzYZzH · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Multiple View Geometry

Computer Vision – Lecture 15

1

Further Reading

• 7 lectures from S Lazebnik

• Slides from D Fouhey and J Johnson

• Many slides adapted from both sources

2

Multi-view geometry problems

? Camera 1 R1,t1 Recovering structure: Given cameras and correspondences, find 3D.

Camera 2 Slide credit: Noah Snavely

R2,t2

Camera 3 R3,t3 3

Multi-view geometry problems

Stereo/Epipolar Geomery: Given 2 cameras, find where a point could be

Slide credit:

4 Noah Snavely

Camera 1 R1,t1 Camera 2 R2,t2

Camera 3 R3,t3

Multi-view geometry problems

Motion: Figure out R, t for a set of cameras given correspondences

Slide credit: Noah Snavely

Camera R1,t1 1 ? Camera R2,t2 2 ? ?Camera 3 R3,t3 5

Epipolar constraint

Where can we find the ð′ corresponding to ð in the other image?

6

Epipolar geometry setup

ð¶ ð¶′

• Suppose we have two cameras with centers ð¶, ð¶′

• The baseline is the line connecting the origins

7

Epipolar geometry setup

ð¶ ð ð′

ð¶′

Epipoles ð, ð′ are where the baseline intersects the image planes, or projections of the other camera in each view

8

Epipolar geometry setup

ð¿

ð ð′

ð¶ ð ð′

ð¶′

• Consider a point ð¿, which projects to ð and ð′

9

Epipolar geometry setup

ð¿

ð ð′

ð¶ ð ð′

ð¶′

• The plane formed by ð¿, ð¶, and ð¶′ is called an epipolar plane

• There is a family of planes passing through ð¶ and ð¶′

10

Epipolar geometry setup

ð¿

ð ð′

ð¶ ð ð′

ð¶′

• Epipolar lines connect the epipoles to the projections of ð¿

• Equivalently, they are intersections of the epipolar plane with the image planes – thus, they come in matching pairs

11

Epipolar geometry setup: Summary

ð¿

Epipolar plane ð ð′

Epipolar lines

ð¶ ð Baseline

ð′ ð¶′

Epipoles

12

Example: Converging cameras

13

Example: Converging cameras

ð¶ ð ð′ ð¶′ • Epipoles are finite, may be visible in the image

14

Example: Motion parallel to image plane

ð¶ ð¶′

• Where are the epipoles and what do the epipolar lines look like?

15

Example: Motion parallel to image plane

ð ð′

ð¶ ð¶′

• Epipoles infinitely far away, epipolar lines parallel

16

Example: Motion perpendicular to image plane

http://vimeo.com/48425421

17

Example: Motion perpendicular to image plane

ð′ð

18

• Epipole is “focus of ð¶′

expansion” and coincides with the principal point of the camera

ð¶• Epipolar lines go out from

principal point

Epipolar constraint

ð¶

ð

Suppose we observe a single point ð in one image

19

Epipolar constraint

ðð¶ ð ð′

ð¶′

Where can we find the ð′ corresponding to ð in the other image?

20

Epipolar constraint

ðð¶ ð ð′

ð¶′

• Where can we find the ð′ corresponding to ð in the other image?

• Along the epipolar line corresponding to ð (projection of visual ray connecting ð¶ with ð into the second image plane) 21

Epipolar constraint

ð¶ ð ð′

ð¶′ ð′

Similarly, all points in the left image corresponding to ð′ have to lie along the epipolar line corresponding to ð′

22

Epipolar constraint

ð¶ ð ð′

ð¶′ ð

ð′ ð ð′ • Potential matches for ð have to lie on the matching epipolar line ð′

• Potential matches for ð′ have to lie on the matching epipolar line ð

23

Epipolar constraint: Example

24

Epipolar constraint

ð¿

ð

ð′ ð ð′ ð¶ ð ð′ ð¶′ Whenever two points ð and ð′ lie on matching epipolar lines ð and ð′, the visual rays corresponding to them meet in space, i.e., ð and ð′ could be projections of the same 3D point ð¿

25

Epipolar constraint

ð¶ ð ð′

ð¶′ ð ð′ Remember: in general, two rays do not meet in space\!

26

Epipolar constraint

ð¿ ð¿′

ð

ð′ ð ð′ ð¶ ð ð′ ð¶′ Caveat: if ð and ð′ satisfy the epipolar constraint, this doesn’t mean they have to be projections of the same 3D point

27

Epipolar Constraint: Calibrated ð¿

case

ð ð′ ðð¹

• Assume the intrinsic and extrinsic parameters of the cameras are known, world coordinate system is set to that of the first camera

• Then the projection matrices are given by ð²\[ð° | ð\] and ð²′\[ð¹ | ð\]

• We can pre-multiply the projection matrices (and the image points) by the inverse calibration matrices to get normalized image coordinates:

•ðnorm = ð²−ððpixel ≅ ð° ð\]ð¿, ð′norm = ð²′−ðð′ pixel ≅ ð¹ ð\]ð¿

28

Epipolar Constraint: Calibrated case

ðnorm ≅ ð° ð\]ð¿ ð¿

\= (ð,1)ð ð′norm ≅ ð¹ ð\]ð¿ ð° ð\] ð1 ð ð′ ð= ð¹ ð¹ð ð\] + ð1 ð ð¹

ð′ ≅ ð¹ð + ð

• This means the three vectors ð′, ð¹ð, and ð are linearly dependent

• This constraint can be written using the triple product

•ð′ ∙ ð × ð¹ð = 0

29

Epipolar Constraint: Calibrated case

•ð′ ∙ ð × ð¹ð = 0

ð¿ = (ð,1)ð

ð° ð\] ð1 ð ð′

ð= ð¹ ð¹ð ð\] + ð1 ðð¹

ð′ð\[ð×\]ð¹ð = 0

0 −ð3 ð2 ð1Recall: ð × ð =

ð3 0 −ð2 ð1 −ð1 0

ð2ð3

\= \[ð×\]ð

30

Epipolar Constraint: Calibrated case

•ð′ ∙ ð × ð¹ð = 0

ð¿ = (ð,1)ð

ð° ð\] ð1 ð ð′

ð= ð¹ ð¹ð ð\] + ð1 ð ð¹

ð′ð\[ð×\]ð¹ð = 0

ð′ðð¬ð = 0

Essential Matrix

H. C. Longuet-Higgins. A computer algorithm for reconstructing a scene from two projections. Nature, 1981

31

The essential matrix

ð¿

ð ð′

ð′ðð¬ð = 0

ð¥′,ð¦′,1

ððð11 21 31 ððð12 22 32 ððð13 23 33

ð¥ð¦1

\= 0

32

The essential matrix: Properties

ð¿

ð ð′

ð′

ð′ðð¬ð = 0

ð¬ð is the epipolar line associated with ð (ð′ = ð¬ð)

Recall: a line is given by ðð¥ + ðð¦ + ð = 0 or ðð»ð = 0 where ð = (ð,ð,ð)ð and ð = (ð¥,ð¦,1)ð 33

The essential matrix: Properties

ð¿

ð ð

ð′

ð′ðð¬ð = 0

• ð¬ð is the epipolar line associated with ð (ð′ = ð¬ð)

• ð¬ðð′ is the epipolar line associated with ð′ (ð = ð¬ðð′)

• ð¬ð = ð and ð¬ðð′ = ð

• ð¬ is singular (rank two) and has five degrees of freedom

34

Epipolar constraint: Uncalibrated case

ð¿

ð ð′

• The calibration matrices ð² and ð²′ of the two cameras are unknown

• We can write the epipolar constraint in terms of unknown normalized coordinates:

•ð′ð norm ð¬ðnorm = 0,

•where ðnorm = ð²−ðð, ð′norm = ð²′−ðð′

35

Epipolar constraint: Uncalibrated case

•ð′ð norm ð¬ðnorm = 0

ð¿

ð′ðð­ð = 0, where ð­ = ð²′−ðð¬ð²−1

ðnorm = ð²−ðð

ð′norm = ð²′−ðð′

ð ð′

Fundamental Matrix

Faugeras et al., (1992), Hartley (1992)

36

The fundamental matrix

ð¿

ð ð ð′

ð′

ð′ðð­ð = 0

ð¥′,ð¦′,1

ð11 ð12 ð13 ð21 ð22 ð23 ð31 ð32 ð33

ð¥ð¦1

\= 0

37

The fundamental matrix: Properties

ð¿

ð ð ð′

ð′

ð′ðð­ð = 0

• ð­ð is the epipolar line associated with ð (ð′ = ð­ð)

• ð­ðð′ is the epipolar line associated with ð′ (ð = ð­ðð′)

• ð­ð = ð and ð­ðð′ = ð

• ð­ is singular (rank two) and has seven degrees of freedom

38

Estimating the fundamental matrix

• Given: correspondences ð = (ð¥,ð¦,1)ð and ð′ = (ð¥′,ð¦′,1)ð

39

Estimating the fundamental matrix

• Given: correspondences ðð = (ð¥ð,ð¦ð,1)ð and ð′ ð= (ð¥ð′,ð¦ð′,1)ð

• Constraint: ð′ð»ð­ð = 0

• ð¥′,ð¦′,1

ð11 ð12 ð11 ð12 ð13 ð21 ð22 ð23 ð31 ð32 ð33 ð¥ð¦ð13 = 0 1

ð¥′ð¥,ð¥′ð¦,ð¥′,ð¦′ð¥,ð¦′ð¦,ð¦′,ð¥,ð¦,1

ð21 ð22 ð23 ð31 ð32 ð33

\= 040

The eight point algorithm

⋮ ð¥′ð¥ ð¥′ð¦ ð¥′ ð¦′ð¥ ð¦′ð¦ ð¦′ ð¥ ð¦ 1

⋮

ð11 ð12 ð13 ð21 ð22 ð23 ð31 ð32 ð33

\= ð

Homogeneous least squares to find ð:

arg min

ð =1 ð¼

ð¼ð 2 2Eigenvector of ð¼ð»ð¼ with

smallest eigenvalue

41

Enforcing rank-2 constraint

• We know ð­ needs to be singular/rank 2. How do we force it to be singular?

• Solution: take SVD of the initial estimate and throw out the smallest singular value

ð­init = ð¼ðºð½ð ðº =

ð0 1 0 ð0 1 0 0 0 ð0 2 0 0

42 0 ð0 2 0 0 ð3

ðº′ =

ð­ = ð¼ð®′ð½ð

Enforcing rank-2 constraint

Initial ð­ estimate Rank-2 estimate

43

The Fundamental Matrix Song

http://danielwedge.com/fmatrix/

44

Large-scale SfM

• 2006: Photo Tourism (Snavely et al,, SIGGAPH’06)

• 3D reconstruction from internet images

• Large scale compute

• 2009: Building Rome in a Day (Agarwal et al. ICCV’09)

• Search “rome” on flickr

• Reconstruction: 150k images, 21h, 500CPUs

45

Neural Rendering

46

1850: Photosculpture

• 24 photographs of an object/person

• Cut contour from wood

• Assemble radial sculpture

47

1986: The Rendering Equation

How much light (of wavelength ð) is leaving a point ð¥ in the direction of ðð at time ð¡?

ð¿ð ð¥,ðð,ð,ð¡ = ð¿ð ð¥,ðð,ð,ð¡ + ð¿ð(ð¥,ðð,ð,ð¡)

emitted radiance

reflected radiance (glowing things)

Immel, David S.; Cohen, Michael F.; Greenberg, Donald P. "A radiosity method for non-diffuse environments”, SIGGRAPH 1986 Kajiya, James T."The rendering equation". Conference on Computer graphics and interactive techniques 1986

48

1986: The Rendering Equation

ð¿ð ð¥,ðð,ð,ð¡ = නΩ incoming radiance at ð¥

from direction ðð

ðð ð¥,ðð,ðð,ð,ð¡ ð¿ð ð¥,ðð,ð,ð¡ ðð ⋅ ð ððð

bidirectional reflectance

surface normal distribution function (BRDF)

49

ð

1965: The BRDF

ðð ðð,ðð = ðð¿ð(ðð)

ð¿ð ðð ðð ⋅ ð ððð

• Positivity: ðð ðð,ðð \> 0

• Reciprocity: ðð ðð,ðð = ðð ðð,ðð

• Energy conservation: ∀ðð,නΩ ðð ðð,ðð ðð ⋅ ð ððð ≤ 1

50 Nicodemus, Fred (1965). "Directional reflectance and emissivity of an opaque surface". Applied Optics

diffuse specular mirror

Lightfield camera arrays

• Use many synchronized cameras to capture a scene from many angle simlutaneously

• Film use: The Matrix (1999)

51

Mildenhall, Ben, et al. "Nerf: Representing scenes as neural radiance fields for view synthesis.“, ECCV 2020

Neural Radiance Fields

• Input: Image collection

• Learning: mapping coordinates (x,y,z) to color and occupancy

• Output: rendering from novel viewpoints

52

Neural Fields

Φ:ℝ2 → ℝ2

(x,y)

Neural Network (Φ)

Φ:ℝ2 → ℝ2

(x,y)

Neural Network (Φ)

Eulerian Flow Field

53 \[Slide: Srinath Sridhar, Towaki Takikawa at CVPR ‘22 Tutorial on Neural Fields in Computer Vision \]

Magnetic Field

\[Koldora CC\]

Neural Fields

54 \[Slide: Yiheng Xie, at CVPR ‘22 Tutorial on Neural Fields in Computer Vision \]

What we want to

reconstruct: What we can

measure:

Radiance Field

z

RGB Image

Spatial

x

y Temporal

Signed Distance Field

tCoordinate Sampling

Neural Network Reconstruction Reconstruction Domain

Domain Forward Forward Map

Map Sensor Sensor Domain Domain

The bridge: forward maps

Volume Rendering

Sphere Tracing

Supervision

Depth Normal

Slide credit: Angjoo Kanazawa, ECCV 2022 Tutorial Neural Volumetric Rendering for Computer Vision

Neural Radiance Fields

55

Neural Radiance Fields

3D World

ð Neural F
