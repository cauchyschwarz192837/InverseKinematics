# Human Arm Inverse Kinematics in C++ and OpenGL for Virtual Reality App in Oculus Quest 2 (Test Reference)

This is an implemention of inverse kinematics (IK) on 3 joints with 9 degrees of freedom using the numerical Jacobian Transpose method using C++ and OpenGL for rendering visualizations. 

This was later used for intern work at Creativex Consulting Pte Ltd in 2022. Final code cannot be shared, but a short video demo can be found here (click the image):

[![Watch the video](https://img.youtube.com/vi/jOmvSfiN6L8/hqdefault.jpg)](https://www.youtube.com/embed/jOmvSfiN6L8)

---

## What is Inverse Kinematics?

In computer graphics and robotics, inverse kinematics (IK) solves the problem:

> Given a desired end-effector position (e.g., the hand in 3D space), determine the joint angles required to reach that position.

This is the inverse of forward kinematics, where joint angles are known and the hand position is computed.

Mathematically:

- Let joint angles be  
  \[
  \theta \in \mathbb{R}^n
  \]
- Let the hand position be  
  \[
  \mathbf{x} = f(\theta)
  \]

Inverse kinematics solves for:

\[
\theta \quad \text{such that} \quad f(\theta) = \mathbf{x}_{target}
\]

Because this mapping is nonlinear and often over-parameterized, a closed-form solution is not always feasible. Instead, numerical methods are used.

---

## Jacobian Transpose Method

The implementation uses the Jacobian Transpose approach:

1. Compute the positional error:
   \[
   \mathbf{e} = \mathbf{x}_{target} - \mathbf{x}_{current}
   \]

2. Compute the Jacobian matrix:
   \[
   J = \frac{\partial f}{\partial \theta}
   \]

3. Update joint angles using:
   \[
   \Delta \theta = \alpha J^T \mathbf{e}
   \]

Where:
- \( J \) maps joint velocity to end-effector velocity.
- \( J^T \) provides a stable gradient-like direction.
- \( \alpha \) is a step size parameter.

The system iteratively updates joint angles until the positional error falls below a tolerance threshold.

---

## System Features

- 3 joints (shoulder, elbow, wrist)
- 9 degrees of freedom
- Real-time OpenGL visualization
- Quaternion-based rotation handling (avoids gimbal lock)
- Joint limit constraints for anatomical realism
- Iterative numerical solver
- VR controller input driving target hand position

---

## Application in Virtual Reality

In the VR system:

- Hand position is tracked via motion controllers.
- The IK solver computes arm joint angles in real time.
- Joint velocities are derived using Jacobian-based mapping.
- Constraints ensure physically plausible arm motion.

This allows the avatar’s arm to move naturally and stably, even during rapid motion.

---
