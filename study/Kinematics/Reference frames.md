---
date: 2024-09-01
tags:
  - theory
  - ReferenceFrame
---
# Reference Frames
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 2.1

### Earth-Centered Reference Frames
**ECI:** The Earth-centered inertial (**ECI**) frame $\{i\}=(x_i, y_i, z_i)$ is an inertial frame for terrestrial navigation, that is a non accelerating reference frame in which Newton’s laws of motion apply. This includes inertial navigation systems. The origin of $\{i\}$ is located at the center $O_i$ of the Earth with axes as shown in Figure.
**ECEF**: The Earth-centered Earth-fixed (**ECEF**) reference frame $\{e\}=(x_e, y_e, z_e)$ has its origin $O_e$ fixed to the center of the Earth but the axes rotate relative to the inertial frame **ECI**, which is fixed in space. The angular rate of rotation is $ω_e = 7.2921 × 10^{−5}$ rad/s. For marine craft moving at relatively low speed, the Earth rotation can be neglected and hence $e$ can be considered to be inertial. Drifting ships, however, should not neglect the Earth rotation. The coordinate system $e$ is usually used for global guidance, navigation and control, for instance to describe the motion and location of ships in transit between different continents. [[Vectoral Notation]]
![[Pasted image 20240829113927.png]]
### Geographic Reference Frames
**NED**: *The North-East-Down* (**NED**) coordinate system $\{n\} = (x_n, y_n, z_n)$ with origin $O_n$ is defined relative to the Earth’s reference ellipsoid (World Geodetic System, 1984). This is the coordinate system we refer to in our everyday life. It is usually defined as the tangent plane on the surface of the Earth moving with the craft, but with axes pointing in different directions than the body-fixed axes of the craft. For this system the $x$ axis points towards true North, the $y$ axis points towards East while the $z$ axis points downwards normal to the Earth’s surface. The location of $\{n\}$ relative to $\{e\}$ is determined by using two angles $l$ and $\mu$ denoting the longitude and latitude, respectively.
**BODY**: The body-fixed reference frame $\{b\} = (x_b, y_b, z_b)$ with origin $O_b$ is a moving coordinate frame that is fixed to the craft. The position and orientation of the craft are described relative to the inertial reference frame (approximated by $\{e\}$ or $\{n\}$ for marine craft) while the linear and angular velocities of the craft should be expressed in the body-fixed coordinate system. The origin $O_b$ is usually chosen to coincide with a point midships in the water line. This point will be referred to as $CO$ (see Figure). For marine craft, the body axes $x_b$, $y_b$ and $z_b$ are chosen to coincide with the principal axes of inertia.
![[Pasted image 20240829114827.png]]
### Body-Fixed Reference Points
The following reference points are defined with respect to CO:
* **CG** - center of gravity
* **CB** - center of buoyancy
* **CF** - center of flotation (located a distance **LCF** from **CO** in the $x$-direction)