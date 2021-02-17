---
title: "Linear Algebra: Matrices and Linear Equations - Matrices"

classes: wide

categories:
  - Linear Algebra
tags:
  - Mathematics
  - Linear Algebra

toc: true
---

# Question 

## Question 1

Show that for any square matrix, the matrix $$A + \mathbf{A}^\top$$ is symmetric.

## Question 2

If $$A = (a_{ij})$$ is a square matrix, then the elements $$a_{ii}$$ are called the **diagonal** elements. How do the diagonal elements of $$A$$ and $$\mathbf{A}^\top$$ differ?

## Question 3

Define a matrix $$A$$ to be **skew-symmetric** if $$\mathbf{A}^\top = -A$$. Show that for any square matrix $$A$$, the matrix $$A-\mathbf{A}^\top$$ is skew-symmetric.

## Question 4

If a matrix is skew-symmetric, what can you say about its diagonal elements?

<br/>

# Answer

## Answer 1

the matrix $$A + \mathbf{A}^\top$$ is symmetric.

$$\because (A + \mathbf{A}^\top)^\top = (\mathbf{A}^\top + A)$$

$$ = (A+\mathbf{A}^\top)$$

## Answer 2

Same

$$A_{i,j} = 
 \begin{pmatrix}
  \color{green}{a_{1,1}} & a_{1,2} & \cdots & a_{1,j} \\
  a_{2,1} & \color{green}{a_{2,2}} & \cdots & a_{2,j} \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  a_{i,1} & a_{i,2} & \cdots & \color{green}{a_{i,j}} 
 \end{pmatrix}$$

 $$\mathbf{(A)}^\top_{i,j} = 
 \begin{pmatrix}
  \color{red}{a_{1,1}} & a_{2,1} & \cdots & a_{i,1} \\
  a_{1,2} & \color{red}{a_{2,2}} & \cdots & a_{i,2} \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  a_{1,j} & a_{2,j} & \cdots & \color{red}{a_{i,j}} 
 \end{pmatrix}$$

## Answer 3

 The matrix $$A - \mathbf{A}^\top$$ is a skew-symmetric.

 $$\because \mathbf{(A - \mathbf{A}^\top)}^\top = \mathbf{A}^\top - A$$

 $$ = -(A - \mathbf{A}^\top)$$

## Answer 4

$$\text{By skew-symmetric}$$

$$a_{ii} = -a_{ii}$$

$$\therefore a_{ii} = 0$$
