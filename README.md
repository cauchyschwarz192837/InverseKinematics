# Inverse Kinematics in C++ and OpenGL for Virtual Reality App

Implemention of inverse kinematics (IK) on 3 joints with 9 degrees of freedom using the numerical Jacobian Transpose method using C++ and OpenGL for rendering visualizations. 

Final code cannot be shared, but a short video demo can be found here (click the image):

[![Watch the video](https://img.youtube.com/vi/jOmvSfiN6L8/hqdefault.jpg)](https://www.youtube.com/embed/jOmvSfiN6L8)

---

Inverse kinematics (IK) solves the problem: Given a desired end-effector position (e.g., the hand in 3D space), determine the joint angles required to reach that position.

Let joint angles be  
  $$\theta \in \mathbb{R}^n$$
Let the hand position be  
  $$\mathbf{x} = f(\theta) $$

We also solve for:

$$
\theta \quad \text{such that} \quad f(\theta) = \mathbf{x}_{target}
$$

Because this mapping is nonlinear and often over-parameterised, we use numerical methods are used.

---

## Jacobian Transpose Method

The implementation uses the Jacobian Transpose approach:

1. Compute the positional error:
   $$e = x_{target} - x_{current}$$

2. Compute the Jacobian matrix:
   $$J = \frac{\partial f}{\partial \theta}$$

3. Update joint angles using:
   $$\Delta \theta = \alpha J^T \mathbf{e}$$

where $J$ maps joint velocity to end-effector velocity, $J^T$ provides a stable gradient-like direction, $\alpha$ is a step size parameter.

The system iteratively updates joint angles until the positional error falls below a tolerance threshold. Hand position is tracked via motion controllers and the IK solver computes arm joint angles in real time. Constraints ensure physically plausible arm motion.
