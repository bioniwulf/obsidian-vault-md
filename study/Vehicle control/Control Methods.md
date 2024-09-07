# Control Methods

There are plenty of different methods for vehicle motion control:
## Feedback-based Methods
* [[PID Control]]
* [[Fuzzy Logic Control]]
* [[Sliding Control]]
## Model-based Methods
* [[Model Predictive Control]]
* [[Adaptive Control]]
* [[Neural Network Control]]
* [[LQR Control]]
## Overview Sources
* [Youtube. Control Bootcamp (U. Washington)](https://www.youtube.com/playlist?list=PLMrJAkhIeNNR20Mz-VpzgfQs5zrYi085m)

## Hits and Tips
### Inner-outer loops
Inner-outer (dynamic-kinematic) loop control structures are pervasive and have shown to be effective. In particular, inner-outer loop control structures exhibit a fast-slow temporal scale separation that yields simple ”rules of thumb” for controller tuning. Stated intuitively, the inner loop dynamics should be much faster than those of the outer loop.
Conceptually, the procedure described has three key advantages:
* it decouples the design of the inner and outer control loops,
* the structure of the outer loop controller does not depend on the dynamics of the vehicle, and
* it affords practitioners a very convenient method to effectively implement path following controllers on a wide range of vehicles.