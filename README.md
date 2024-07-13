# Forward-Inverse-Kinematics-For-3DOF-Robot-Arm
# Forward Kinematics (FK)
Forward kinematics involves calculating the position and orientation of the robot's end-effector given the joint parameters (angles for revolute joints, positions for prismatic joints).

## Example: 3-DoF Robot Arm
Assume we have a 3-DoF robot arm with the following configuration:

- Joint 1: Revolute (rotational around the z-axis)
- Joint 2: Revolute (rotational around the y-axis)
- Joint 3: Revolute (rotational around the y-axis)
## Denavit-Hartenberg (DH) Parameters
We use the DH convention to describe the robot's configuration.  
#### 
#### The DH parameters are:

- 𝜃𝑖: Joint angle  
- 𝑑𝑖: Link offset  
- 𝑎𝑖: Link length  
- 𝛼𝑖: Link twist  
#### 
### Denavit-Hartenberg (DH) Parameters

We use the DH convention to describe the robot's configuration. The DH parameters are:
- \( \theta_i \): Joint angle
- \( d_i \): Link offset
- \( a_i \): Link length
- \( \alpha_i \): Link twist

Let's define the DH parameters for our 3-DoF robot as follows:

\[
\begin{array}{|c|c|c|c|c|}
\hline
\text{Joint } i & \theta_i \text{ (variable)} & d_i \text{ (constant)} & a_i \text{ (constant)} & \alpha_i \text{ (constant)} \\
\hline
1 & \theta_1 & d_1 & a_1 & 0 \\
\hline
2 & \theta_2 & 0 & a_2 & 0 \\
\hline
3 & \theta_3 & 0 & a_3 & 0 \\
\hline
\end{array}
\]

### Transformation Matrices

The transformation matrix for each joint can be represented as:

\[
\begin{bmatrix}
\cos\theta_i & -\sin\theta_i \cos\alpha_i & \sin\theta_i \sin\alpha_i & a_i \cos\theta_i \\
\sin\theta_i & \cos\theta_i \cos\alpha_i & -\cos\theta_i \sin\alpha_i & a_i \sin\theta_i \\
0 & \sin\alpha_i & \cos\alpha_i & d_i \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

For our 3-DoF robot, the transformation matrices are:

1. \( T_1 \):
\[
T_1 =
\begin{bmatrix}
\cos\theta_1 & -\sin\theta_1 & 0 & a_1 \cos\theta_1 \\
\sin\theta_1 & \cos\theta_1 & 0 & a_1 \sin\theta_1 \\
0 & 0 & 1 & d_1 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

2. \( T_2 \):
\[
T_2 =
\begin{bmatrix}
\cos\theta_2 & -\sin\theta_2 & 0 & a_2 \cos\theta_2 \\
\sin\theta_2 & \cos\theta_2 & 0 & a_2 \sin\theta_2 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

3. \( T_3 \):
\[
T_3 =
\begin{bmatrix}
\cos\theta_3 & -\sin\theta_3 & 0 & a_3 \cos\theta_3 \\
\sin\theta_3 & \cos\theta_3 & 0 & a_3 \sin\theta_3 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\]

The overall transformation matrix from the base to the end-effector is the product of these matrices:
\[
T_{0\_3} = T_1 \cdot T_2 \cdot T_3
\]

Multiply the matrices to get the final transformation matrix \( T_{0\_3} \), which gives the position and orientation of the end-effector.

### Inverse Kinematics (IK)

Inverse kinematics involves calculating the joint parameters given the desired position and orientation of the end-effector.

For a 3-DoF robot, we aim to find \( \theta_1 \), \( \theta_2 \), and \( \theta_3 \).

#### Steps for Inverse Kinematics

1. **Calculate Position of the End-Effector**: Use the desired position \((x, y, z)\).

2. **Solve for \( \theta_1 \)**:
   - Use the projection of the end-effector position on the \(xy\)-plane:
   \[
   \theta_1 = \tan^{-1}\left(\frac{y}{x}\right)
   \]
