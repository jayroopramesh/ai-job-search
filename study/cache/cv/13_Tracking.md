# Computer Vision — Tracking
> Source: Google Drive file 1-wZQLntlQaYxPGw_N6tledmKdE5NQx-a · extracted 2026-09-16 · lossy text extraction — math glyphs may be mangled; verify formulas visually in the PDF before quizzing them. Page markers like [Page N] give slide numbers for citations.

Tracking

Computer Vision – Lecture 13

1

Further Reading

• Lecture from A Vedaldi and A Zisserman

• Open for suggestions…

2

Visual Tracking

Visual tracking involves the identification of some characteristic of the scene in successive images.

2D tracking

• follow and perhaps control the image position of some entity as it moves from frame to frame over time.

3D (or pose) tracking

• use image measurements (possibly involving 2D tracking) to update the 6 degrees of freedom (3 translation + 3 rotation) which define 3D pose.

3

w

h

Template ð

Image I

• Tracking by Detection (each frame processed individually)

• Very slow: (\#pixels\_image \* \#pixels\_template) comparisons 4

Recap: Template Tracking

Sum of squared differences between image I and template ð at every location (ð¢,ð£)

ð¸ ð¢,ð£ = ෍

ð¥,ð¦ ∈ −ð¤2,ð¤2 × −ℎ2,ℎ2

ð¼ ð¢ + ð¥,ð£ + ð¦ − ð ð¥ + ð¤2 ,ð¦ + ℎ2

2

Energy E

Lucas-Kanade Template Tracking

ð¸ ð¢,ð£ = ෍ð¼ ð¢ + ð¥,ð£ + ð¦ − ð ð¥,ð¦ 2

ð¥,ð¦

Improving the efficiency:

• Formulate search as an optimisation problem using brightness constancy as our objective function

• ð¸ is a non-convex function over the image ð¼

• Suppose frame

the starting point is ð¡ð¥,ð¡ð¦

ð e.g., detection in prev.

• LK searches for an update ð¿ð¥,ð¿ð¦

5 ð of the starting point

Lucas-Kanade Template Tracking

ð¡ð¥,ð¡ð¦

ð ð¡ð¥ + ð¿ð¥,ð¡ð¦ + ð¿ð¦

ð

Reformulate the energy relative to the update (ð¿ð¥,ð¿ð¦):

ð¸ ð¿ð¥,ð¿ð¦ = ෍ð¥,ð¦∈ð

1st order Taylor expansion (∇ð¼ = ð¼ð¥,ð¼ð¦

2

ð¼ ð¡ð¥ + ð¥ + ð¿ð¥,ð¡ð¦ + ð¦ + ð¿ð¦ − ð ð¥,ð¦

ð ∈ ℝ2 is the image gradient):

ð¸ ð¿ð¥,ð¿ð¦ ≈ ෍ð¥,ð¦∈ð

2

Local minimum where partial derivatives of ð¸ w.r.t to ð¿ are 0: ðð¸ðð¿ð¥ = 2ð¼ð¥ ෍ð¥,ð¦∈ð

ð¼ ð¡ð¥ + ð¥,ð¡ð¦ + ð¦ + ∇ð¼ð ð¿ð¥ð¿ð¦ − ð ð¥,ð¦

ð¼ ð¡ð¥ + ð¥,ð¡ð¦ + ð¦ + ∇ð¼ð ð¿ð¥ð¿ð¦ − ð ð¥,ð¦ = 0

ðð¸ðð¿ð¦ = 2ð¼ð¦ ෍ð¥,ð¦∈ð

ð¼ ð¡ð¥ + ð¥,ð¡ð¦ + ð¦ + ∇ð¼ð ð¿ð¥ð¿ð¦ − ð ð¥,ð¦ = 0

6

Lucas-Kanade Template Tracking

ð¡ð¥,ð¡ð¦

ð ð¡ð¥ + ð¿ð¥,ð¡ð¦ + ð¿ð¦

ð

Rewrite in matrix form:

σð¥,ð¦∈ð∇ð¼∇ð¼ð ð¿ð¥ð¿ð¦ = −σð¥,ð¦∈ð∇ð¼ ð¼ ð¡ð¥ + ð¥,ð¡ð¦ + ð¦ − ð ð¥,ð¦

2x2 matrix 2x1 vector 2x1 vector • We can solve for ð¿ð¥,ð¿ð¦ in closed form

• Update the current estimate ð¡ð¥,ð¡ð¦

• Keep iterating until convergence, i.e. ð¿ð¥,ð¿ð¦ is small

• This idea is very general

• The example was using translation only ð¡ð¥ + ð¿ð¥,ð¡ð¦ + ð¿ð¦

• Let’s generalise it to any transform W

7

Generalised LK tracking

• Transform ð

• Parameters ð

• Updates Δð

• Pixel ð = ð¥,ð¦ ð

• Previous ð = ð¡ð¡ð¦ ð¥example: translation

Δð = ð¿ð¥ð¿ð¦

ð ð,ð =

1 0 ð¡ð¥ 0 1 ð¡ð¦ 0 0 1

ð¥ð¦1

8

Generalised LK tracking

• Transform ð

• Parameters ð

• Updates Δð

• Pixel ð = ð¥,ð¦ ð

• Example: translation ð =

ð¡ð¡ð¦ð¥+ rotation ð

ð ð,ð =

cosð −sinð sinð cosð 0 0 ð¡ð¥ ð¡ð¦ 1

ð¥ð¦1

9

Generalised LK tracking

• Transform ð

• Parameters ð

• Updates Δð

• Pixel ð = ð¥,ð¦ ð

• Example: translation ð =

ð¡ð¡ð  ð¦ð¥+ scaling

ð ð,ð =

ð  0 0 0 ð  0 ð¡ð¥ ð¡ð¦ 1

ð¥ð¦1

10

Generalised LK tracking

• Transform ð

• Parameters ð

• Updates Δð

• Pixel ð = ð¥,ð¦ ð

• Example: affine

ð =

ð11⋮ð23

ð ð,ð =

ðð11 21 ðð12 22 ðð13 23 0 0 1

ð¥ð¦1

11

Generalised LK tracking

Energy in general form:

ð¸(ð) = ෍ð¼ ð(ð,ð) − ð ð 2

Warp each point ð in the template to its image

ð∈ð

location using the warp ð and its parameters ð.

Assume a current estimate ð is known, solve for an update Δð:

ð¸(ð«ð) = ෍ð∈ð

ð¼ ð(ð,ð + ð«ð) − ð ð 2 Same as before, update ð with ð + Δð and iterate.

To solve for Δð, approximate with 1st order Taylor expansion:

ð¸ ð«ð ≈ ෍ð∈ð

ð¼ ð(ð,ð) + ∇ð¼ð ðððð Δð − ð ð

2

ðððð is the Jacobian of the warp.

12

Jacobian

The Jacobian is the matrix of all 1st order derivatives of a function.

In our case:

ðððð =

ððð¥ ððð … ððð¥ ððð ððð¦ ððð … ððð¦ ððð

Example: translation + scaling

ð =

ð¡ð¡ð  ð¦ð¥ð ð,ð = ð  0 0 ð¡ð¥ ð  ð¡ð¦

ð¥ð¦1

ðððð = 1 0 0 ð¥ 1 ð¦

13

Generalised LK tracking

Partial derivative with respect to Δð:

Setting this to equal zero leads to:

2 ð¸ ð«ð ≈ ෍ð∈ð

2෍ð∈ð

ð¼ ð(ð,ð) + ∇ð¼ð ðððð Δð − ð ð

ð

ð¼ ð(ð,ð) + ∇ð¼ð ðððð Δð − ð ð

෍ð∈ð

∇ð¼ð ðððð

∇ð¼ð ðððð

ð

∇ð¼ð ðððð Δð = ෍ð∈ð

∇ð¼ð ðððð

ð

ð ð − ð¼ ð(ð,ð)

14

Generalised LK tracking

Simplifying:

∇ð¼ð ðððð

ð

∇ð¼ð ðððð Δð = ෍ð∈ð

∇ð¼ð ðððð

ð ෍ð ð − ð¼ ð(ð,ð)

ð∈ð

ð´ = ෍ð∈ð

∇ð¼ð ðððð

ð

∇ð¼ð ðððð ð = ෍ð∈ð

∇ð¼ð ðððð

ð

ð ð − ð¼ ð(ð,ð)

ð´Δð = ð

Compute update:

Δð = ð´−ðð

15

Generalised LK tracking

• Simple update rule that iteratively refines the tracked position

• Any differentiable warp works

• Further optimization: pre-compute template gradients and warp “the other way”

• In-depth LK analysis:

Lucas-Kanade 20 Years On: A Unifying Framework Simon Baker and Iain Matthews

16

LK Tracker Insights

• A general difficulty with trackers relying too heavily on the spatial relationships between pixels is that they are prone to break due to partial occlusion and orientation changes in the scene.

• Appearance changes can be compensated by updating the template from frame to frame

• But this can lead to “drift”:

• The template will gradually pick up the background and eventually “stick”.

• Can be avoided when background is simple, or with a segmentation mask.

17

Optical Flow – The Beginnings

• Assume timestep a Δð¡. pixel at (ð¥,ð¦,ð¡) with intensity ð¼(ð¥,ð¦,ð¡) has moved by Δð¥,Δð¦ in space during a • Assume, the pixel did not change intensity, so: ð¼ ð¥,ð¦,ð¡ = ð¼(ð¥ + Δð¥,ð¦ + Δð¦,ð¡ + Δð¡)

• If time and thus movement is small: Taylor expansion is a good approximation:

ð¼ ð¥ + Δð¥,ð¦ + Δð¦,ð¡ + Δð¡ ≈ ð¼ ð¥,ð¦,ð¡ + ðð¥ðð¼Δð¥ + ðð¦ðð¼Δy + ðð¡ðð¼Δt

• With above assumption:

ðð¥ðð¼Δð¥ + ðð¦ðð¼Δy + ðð¡ðð¼Δt = 0 or ðð¼ðð¥

Δð¥Δð¡ + ðð¦

ðð¼Δð¦Δð¡ + ðð¡ ðð¼= 0

• Using ∇ð¼ = ðð¼ðð¥, ðð¦

ðð¼ð and ð = Δð¥Δð¡ , Δð¦Δð¡

ð yields the motion constraint equation:

ððð ð = −ðð¼ðð¡

Horn and Schunck “Determining Optical Flow” Artificial Intelligence 17 (1981)

Optical Flow – The Beginnings

• ∇Idirection T ð = − of ðð¡ ðð¼the means image we gradient

are only estimating the flow in the

• Smoothness constraint helps to regularise (weight ð¼):

minð ׭ð ∇IT ð − ðð¡

ðð¼2 + ð¼( ∇ðð¥ 2 + ∇ðð¦

2\) ðð¥ðð¦

• Second term makes flow of close pixels similar

Optical Flow – The Beginnings

Raw estimate Smoothed estimate

Optical Flow – The Beginnings

• Intensity based optical flow

• Problems with uniform-coloured regions

• Difficult to regularise

• Can be combined with LK tracking

• Smoothness constraints

• Difficult evaluation on very few scenes

• Synthetic with ground truth

• Qualitative on real scenes

Motion Estimation

Point Tracking Long-term tracking of individual points

PIPs

TAP-Net

Optical Flow Dense correspondences between a pair of frames

RAFT

Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022 TAP-Vid: A Benchmark for Tracking Any Point in a Video. Doersch et al., NeurIPS D\&B 2022

RAFT: Recurrent All-Pairs Field Transforms for Optical Flow. Teed 22

et al. , ECCV 2020

Reading Computer Vision Papers

• Usually, papers have a main technical figure at the beginning of the “Methods” section.

• This figure is designed to give a holistic overview on how the method works.

• Example: Particle Video Revisited (Harley et al. ‘22).

23 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Particle Video Revisited

24 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Particle Video Revisited

25 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Particle Video Revisited

26 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Particle Video Revisited

27 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Particle Video Revisited

28 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Particle Video Revisited

29 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Particle Video Revisited

30 Particle Video Revisited: Tracking Through Occlusions Using Point Trajectories. Harley et. al. ECCV 2022

Single Point Tracking

• Tracking single points lacks global consistency

• Points drift relative to each other

31

Background points Object points

Tracking with Optical Flow

• Global consist
