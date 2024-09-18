---
{"dg-publish":true,"permalink":"/work/preimage/tdd/implementation-of-transformations-for-projects-and-scans/","noteIcon":""}
---

## Why?
We will store transformations to correctly position and align 3D models in space.

To align two 3D models correctly using their transformation matrices, you need to understand how to manipulate these matrices mathematically. Here’s a step-by-step explanation of the process:

## Understanding Transformation Matrices

A **transformation matrix** in 3D space is typically represented as a 4x4 matrix in homogeneous coordinates. This matrix can encapsulate various transformations such as translation, rotation, and scaling. The general form of a transformation matrix MM is:
![Pasted image 20240918165958.png](/img/user/work/preimage/tdd/Pasted%20image%2020240918165958.png)
Where:
- R is a 3x3 rotation matrix.
- t is a 3x1 translation vector.
- The last row is always (0,0,0,1)(0,0,0,1) to maintain the homogeneous coordinate system.

## Steps to Align Two Models

1. **Extract Transformation Matrices**: Assume you have two models with their respective transformation matrices M1​ and M2​.
2. **Compute the Inverse of the First Model's Matrix**: To align model 2 with model 1, you need to compute the inverse of M1​:
	![Pasted image 20240918170051.png](/img/user/work/preimage/tdd/Pasted%20image%2020240918170051.png)
	Where $R_1^t$​ is the transpose of the rotation matrix (which serves as its inverse for orthogonal matrices), and $-R_1^Tt_1$ translates the origin back to the first model's position.
3. **Transform the Second Model**: Multiply the inverse of the first model's transformation matrix by the second model's transformation matrix:
	![Pasted image 20240918170523.png](/img/user/work/preimage/tdd/Pasted%20image%2020240918170523.png)
	This operation aligns model 2 with respect to model 1’s coordinate system.
4. **Apply the Aligned Transformation**: The resulting matrix $M_{aligned}$​ can now be used to transform the vertices of model 2 into the coordinate space of model 1.

## Example Calculation

If you have specific matrices, for example:
![Pasted image 20240918170652.png](/img/user/work/preimage/tdd/Pasted%20image%2020240918170652.png)
You would compute M1−1M1−1​ and then perform the multiplication to find $M_{aligned}$.