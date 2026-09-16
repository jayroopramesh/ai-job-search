# Computer Vision — Camera Models
> Source: Google Drive file 1s9UvaNQl12mVGAQpJg6DQpw35l3nB2k7 · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

PowerPoint Presentation 

Camera Models

Computer Vision – Lecture 14

(Generative Models postponed to Lecture 16)

1

Further Reading

• 7 lectures from S Lazebnik

• Slides from D Fouhey and J Johnson

• Many slides adapted from both sources

2

Multi-view geometry “Bible”

3

Perspective in Art

• Eastern art: planar perspective 11th century.

• Western art: early Renaissance: 15th century

• Before: attempts to simulate perspective but no good understanding.

Diane Morgan in “Cunk on Earth”, 2022

4

Things aren’t always as they appear…

5

Video source

Single-view ambiguity

ð

ð¿? ð¿? ð¿?

6

Single-view ambiguity

Rashad Alakbarov shadow sculptures 7

Anamorphic perspective

Image source

8

https://en.wikipedia.org/wiki/Anamorphosis

Anamorphic perspective

H. Holbein The Younger, The Ambassadors, 1533

9

Camera Obscura

10

Pinhole Camera

ð

ð′

11

Perspective Projection

ð§

ð¥

Camera Coordinate System

• The optical center (ð) is at the origin

• The z axis is the optical axis perpendicular to the image plane

• The xy plane is parallel to the image plane, x and y axes are horizontal and vertical directions of the image plane

ð

ð¦

ð

ð′

12

Perspective Projection

ð ð§ Focal length

ð

ð¦ð¦′

\= ð ð¦ð§

ð

ð′

Image plane

(ð¥,ð¦,ð§) → ð ð¥ð§ ,ðð¦ð§

3D point 2D point

13

Perspective Projection

Instead of dealing with an image that is upside down, most of the time we will pretend that the image plane is in front of the camera center

14

Single View Ambiguity

From a single image, there is an inherent ambiguity about the scale of the observed object.

15

Projection of lines

Piero della Francesca, Flagellation of Christ, 1455-1460

16

Projection of lines

• Parallel lines meet at a vanishing point

Image source

Piero della Francesca, Flagellation of Christ, 1455-1460

17

Perspective Cues

Slide by Steve Seitz

18

Projection of 3D shapes

What is the shape of the projection of a sphere?

Image source: F. Durand 19

Projection of 3D shapes

• What is the shape of the projection of a sphere?

20

Homogeneous Coordinates III

To form homogeneous coordinates from normal Euclidean coordinates, append 1 as the last entry:

homogeneous image coordinates

ð¥ð¦ð§1

ð¥ ð¦ ð¤

ð¥ (ð¥,ð¦) ⟹

ð¦ (ð¥,ð¦,ð§) ⟹ 1

homogeneous scene coordinates

To convert from homogeneous coordinates, divide by the last entry:

ð¥ ⟹ (ð¥/ð¤,ð¦/ð¤)

ð¦ ð§⟹ (ð¥/ð¤,ð¦/ð¤,ð§/ð¤) ð¤

In homogeneous coordinates, all scalar multiples represent the same point\! 21

Perspective Projection Matrix

• Projection is a matrix multiplication using homogeneous coordinates:

ð 0 0 0 0 ð 0 0 0 0 1 0

ð¥ð¦ð§1

ðð¥= ðð¦ð§

⟹ ðð¥ð§ ,ðð¦ð§

divide by the third coordinate

22

Orthographic projection

Special case of perspective projection

• Distance from center of projection to image plane is infinite

• Also called “parallel projection”

Image World

Slide by Steve Seitz

23

Orthographic projection

Special case of perspective projection

• Distance from center of projection to image plane is infinite

• Also called “parallel projection”

24

Orthographic projection

Special case of perspective projection

• Distance from center of projection to image plane is infinite

• Also called “parallel projection”

Image World

• Assuming projection along the ð§ axis, what’s the matrix?

1 0 0 0 0 1 0 0 0 0 0 1

ð¥ð¦ð§1

ð¥=

ð¦1 25

Slide by Steve Seitz

Approximating an orthographic camera

center at infinity

Source: Hartley & Zisserman 26

Normalized Coordinates

Normalized (camera) coordinate system: camera center is at the origin, the principal axis is the ð§-axis, ð¥ and ð¦ axes of the image plane are parallel to ð¥ and ð¦ axes of the world

27

Perspective projection in normalized coordinates

ððððð

(ð,ð,ð) (ð¥,ð¦)

ð¥ = ð ðð ,ð¦ = ð ðð

ð¥ð¦1

≅ ð 0 0 0

\=

0 ð 0 0 0 0 1 0

ððð1

ð ≅ ð·ð¿

Homogeneous coord. vec. ð of image pointEquality up to scale 28

Homogeneous coord. vec. ð¿ of 3D point

Camera projection matrix ð·

Camera Calibration

Camera calibration: figuring out transformation from world coordinate system to image coordinate system

2D point ð (3x1)

≅

world coordinate system

Camera to

World to

3D pixel coord.

camera coord. trans. matrix ð² (3x3)

trans. matrix ð¹ ðð ð 1 (4x4)

point ð¿ (4x1)

Intrinsic camera parameters: principal point, scaling factors

Canonical projection matrix \[ð° | ð\] (3x4)

Extrinsic camera parameters: rotation, translation 29

Camera Calibration

Camera calibration: figuring out transformation from world coordinate system to image coordinate system

ð· = ð²\[ð¹|ð\]

General camera projection matrix

2D point ð (3x1)

≅

Camera to pixel coord. trans. matrix ð² (3x3)

Canonical projection matrix \[ð° | ð\] (3x4)

world coordinate system

World to camera coord. trans. matrix ð¹ ð ðð 1 (4x4)

3D point ð¿ (4x1)

30

Intrinsic parameters: Principal point

Principal point (ð): point where principal axis intersects the image plane

• In the normalized coordinate system, the origin of the image is at the principal point

• In the image coordinate system: the origin is in the corner

31

Intrinsic parameters: Principal point

py

ðð + ððð¥ ðð + ððð¦ ð

ð¥ = ð ðð + ðð¥, ð¦ = ððð + ðð¦

ð¥ð¦1

ð 0 ðð¥ 0 ≅

0 ð ðð¦ 0 0 0 1 0

We want the principal point to map to (ðð¥,ðð¦) instead of (0,0)

px

\=

ððð1

32

Intrinsic parameters: Principal point

py

Principal point: (ðð¥,ðð¦)

ð 0 ðð¥ 0 ð ðð¦

1 0 0 0

ð 0 ðð¥ 0 0 1 0 0

\=

0 ð ðð¦ 0 0 0 1

0 0 1 0

0 0 1 0

calibration

Canonical

ð· = ð²\[ð°|ð\] matrix ð²

projection matrix \[ð° | ð\]

33

px

Intrinsic parameters: Principal point

• What are the units of the focal length ð and principal point coordinates (ðð¥,ðð¦)?

• Same as world units – likely metric units

• What units do we want for measuring image coordinates?

• Pixel units

• Thus, we need to introduce scaling factors for mapping from world to pixel units

ð 0 ðð¥ 1 0 0 0

ð 0 ðð¥ 0 0 ð ðð¦

0 1 0 0

\=

0 ð ðð¦ 0 0 0 1

0 0 1 0

0 0 1 0

calibration

Canonical

ð· = ð²\[ð°|ð\] matrix ð²

projection matrix \[ð° | ð\]

34

Intrinsic parameters: Scaling factors

ððð¥ ð¦ pixels/m pixels/m Camera sensor

in horizontal direction, in vertical direction

Pixel size (m): ð1ð¥ × ð1ð¦

Calibration matrix

Calibration matrix Scaling factors

ð² in metric units ð² in pixel units

ð0 ð¥ 0 ðð¦ 0 0 0 0 1

pixels/m m pixels

ð 0 ðð¥ 0 ð ðð¦ 0 0 1

ð¼ð¥ 0 ð½ð¥ = 0 ð¼ð¦ ð½ð¦ 0 0 1

35

Extrinsic Parameters

In general, the camera coordinate frame will be related to the world coordinate frame by a rotation and a translation.

camera coordinate

system world coordinate

system In non-homogeneous coordinates, the transformation from world to normalized camera coordinate system is given by:

෩ð¿cam = ð¹ ෩ð¿ − ðª ෩= ð¹෩ð¿ + ð

coords. of point in normalized camera frame

3x3 rotation matrix

coords. of camera center

coords. of a point

in world frame in world frame

36

Extrinsic Parameters

In non-homogeneous coordinates:

In homogeneous coordinates:

3D transformation matrix (4 x 4) ෩ð¿cam = ð¹෩ð¿ + ð

Transformation from normalized 3D coordinates to pixel image coordinates: ð ≅ ð²\[ð°|ð\]ð¿cam

37

ð¿cam = ð¹ ð

ðð» 1 ð¿

Extrinsic Parameters

ð ≅ ð²\[ð°|ð\] ð¹ ð

ðð» 1 ð¿

Simplifying:

ð ≅ ð²\[ð¹|ð\]ð¿ ð = −ð¹෩ðª

38

Camera calibration

ð ≅ ð² ð¹ ð ð¿

ð¥ð¦1

ððð11 21 31 ððð12 22 32 ððð13 23 33 ≅

ððð14 24 34

ððð1

39

Camera calibration

Given ð points with known 3D coordinates ð¿ð and known image projections ðð, estimate the camera parameters

ð¿ð

ðð

ð·

40

Image credit: J. Hays 41

Camera calibration

Given ð points with known 3D coordinates ð¿ð and known image projections ðð, estimate the camera parameters

Camera calibration: Linear method

ðð ≅ ð·ð¿ð

ð·ð =

ððððð1 ð2 ð3 ð4

ð¥ð¦ðð≅ ð¿1

One match gives two linearly independent constraints

ððð·1 ð¿ððð·2 ð¿ððð·3 ð¿ð¿ððððððð 0 −ð¥ðððð 0 ððð −ð¦ðððð

ð·1 ð·2 − − ð¥ðð¦ðð¿ð¿ððððð·3 ð·3 = 0 = 0 ð·ð·ð·123

\= 0

42

Camera calibration: Linear method

Final linear system:

ðð ð¿1ð −ð¦1ð¿1ð ð¿… 1ð ðð … −ð¥…

1ð¿1ð

ðð ð¿ð ð−ð¦ðð¿ð ðð¿ð ððð −ð¥ðð¿ð

ðð·ð·ð·123

\= 0

ð¨ð = 0

• One 2D/3D correspondence gives two linearly independent equations

• The projection matrix has 11 degrees of freedom

• 6 correspondences needed for a minimal solution

• Homogeneous least squares: find ð minimizing ð¨ð 2

• Solution is eigenvect
