---
title: "Linear Algebra: Solving Linear Equations - Vectors and Linear Equations #1"

classes: wide

categories:
  - Linear Algebra
tags:
  - Mathematics
  - Linear Algebra

toc: true
---

# Concepts

## Multiplication by rows

$$Ax$$ comes from **dot products**, each row times the column $$x$$:

$$Ax = \begin{pmatrix}(row 1) \cdot x \\
(row 2) \cdot x \\
(row 3) \cdot x
 \end{pmatrix}$$

## Multiplication by columns

$$Ax$$ is a **combination of column vectors**:

$$Ax = x(\text{column 1}) + y(\text{column 2}) + z(\text{column 3})$$


# Questions

## Question 1

Write $$2x+3y+z+5t=8$$ as a matrix $$A$$ (how many rows?) multiplying the column vector $$x = (x, y, z, t)$$ to produce $$b$$. The solutions $$x$$ fill a plane or "hyperplane" in 4-dimensional space. The plane is 3-dimensional with no 4D volume.

## Question 2

Find the matrix $$P$$ that multiplies $$(x, y, z)$$ to give $$(y, z, x)$$. Find the Matrix $$Q$$ that multiplies $$(y, z, x)$$ to bring back $$(x, y, z)$$.

## Question 3

(a) What 2 by 2 matrix $$R$$ rotates every vector by $$90\,^{\circ}$$? $$R$$ times $$\begin{pmatrix}x \\
y\end{pmatrix}$$ is $$\begin{pmatrix}y \\
-x\end{pmatrix}$$
(b) What 2 by 2 matrix $$R^{2}$$ rotates every vector by $$180\,^{\circ}$$?

# Answers

## Answer 1

$$Ax = \begin{pmatrix}2 & 3 & 1 & 5\end{pmatrix}\begin{pmatrix}x \\
y \\
z \\
t \\
\end{pmatrix}$$

> how many rows?

one row.

## Answer 2

> Find the matrix $$P$$ that multiplies $$(x, y, z)$$ to give $$(y, z, x)$$.

$$\begin{pmatrix}0 & 1 & 0 \\
0 & 0 & 1 \\
1 & 0 & 0
\end{pmatrix}\begin{pmatrix}x \\
y \\
z\end{pmatrix} = \begin{pmatrix}y \\
z \\
x\end{pmatrix}$$

$$\therefore P = \begin{pmatrix}0 & 1 & 0 \\
0 & 0 & 1 \\
1 & 0 & 0\end{pmatrix}$$

> Find the Matrix $$Q$$ that multiplies $$(y, z, x)$$ to bring back $$(x, y, z)$$.

$$\begin{pmatrix}0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{pmatrix}\begin{pmatrix}y \\
z \\
x\end{pmatrix}$$

$$\therefore Q = \begin{pmatrix}0 & 0 & 1 \\
1 & 0 & 0 \\
0 & 1 & 0
\end{pmatrix}$$

## Answer 3

(a)

$$\begin{pmatrix}0 & 1 \\
-1 & 0\end{pmatrix}\begin{pmatrix}x \\
y\end{pmatrix} = \begin{pmatrix}y \\
-x\end{pmatrix}$$

$$\therefore R = \begin{pmatrix}0 & 1 \\
-1 & 0\end{pmatrix}$$

(b)

Intuitively, if a $$90\,^{\circ}$$ rotation occurs when R is applied once, wouldn't a $$180\,^{\circ}$$ rotation occur when R is applied twice?

$$\therefore \text{ Let's apply R to the answer obtained from (a) again.}$$

$$\begin{pmatrix}y \\
-x\end{pmatrix}\begin{pmatrix}0 & 1 \\
-1 & 0\end{pmatrix} = \begin{pmatrix}-x \\
-y\end{pmatrix}$$

<br />

$$\text{By the way, It is the same as:}$$

$$\begin{pmatrix}-1 & 0 \\
0 & -1\end{pmatrix}\begin{pmatrix}x \\
y\end{pmatrix} = \begin{pmatrix}-x \\
-y\end{pmatrix}$$

<br />

$$\text{Here, }\begin{pmatrix}-1 & 0 \\
0 & -1\end{pmatrix} = -I$$

$$\therefore R^{2} = -I$$





