---
title: "Linear Algebra: Matrices and Linear Equations - Multiplication of Matrices #2"

classes: wide

categories:
  - Linear Algebra
tags:
  - Mathematics
  - Linear Algebra

toc: true
---

# Questions

## Question 1

**Rotations.** Let $$R(\theta)$$ be the matrix given by

$$R(\theta) = \begin{pmatrix}\cos{\theta}&-\sin{\theta}\\
\sin{\theta}&\cos{\theta}\end{pmatrix}.$$

(a) Show that for any two numbers $$\theta_{1}$$, $$\theta_{2}$$ we have


$$R(\theta_{1})R(\theta_{2}) = R(\theta_{1} + \theta_{2}).$$

[You will have to use the addition formulas for sine and cosine.]

(b) Show that the matrix $$R(\theta)$$ has an inverse, and write down this inverse.

(c) Let $$A = R(\theta)$$. Show that


$$A^{2} = \begin{pmatrix}\cos{2\theta}&-\sin{2\theta}\\
\sin{2\theta}&\cos{2\theta}
\end{pmatrix}.$$

(d) Determine $$A^{n}$$ for any positive integer $$n$$. Use induction.

## Question 2

For any vector $$X$$ in $$R^{2}$$ let $$Y = R(\theta)X$$ be its rotation by an angle $$\theta$$. Show that $$\left\|Y\right\| = \left\|X\right\|.$$

## Question 3

Let $$A$$ be a square matrix which is of the form

$$\begin{pmatrix}a_{11}&*&\cdots\cdots&&*\\
0&a_{22}&*&\cdots&*\\
\vdots&&\ddots&&\vdots\\
&&&&*\\
0&\cdots\cdots&0&&a_{nn}\end{pmatrix}$$

The notation means that all elements below the diagonal are equal to 0, and the elements above the diagonal are arbitrary. One may express this property by saying that

$$a_{ij}=0 \text{ if } i>j.$$

Such a matrix is called **upper triangular**. If $$A$$, $$B$$ are upper triangular matrices(of the same size) what can you say about the diagonal elements of $$AB$$?

<br/>

# Answers

## Answer 1

(a)

$$R(\theta_{1})R(\theta_{2}) = \begin{pmatrix}\cos{\theta_{1}}&-\sin{\theta_{1}}\\
\sin{\theta_{1}}&\cos{\theta_{1}}\end{pmatrix}\begin{pmatrix}\cos{\theta_{2}}&-\sin{\theta_{2}}\\
\sin{\theta_{2}}&\cos{\theta_{2}}\end{pmatrix}$$

$$=\begin{pmatrix}\cos{\theta_{1}}\cos{\theta_{2}}-\sin{\theta_{1}}\sin{\theta_{2}}&-\cos{\theta_{1}}\sin{\theta_{2}}-\sin{\theta_{1}}\cos{\theta_{2}}\\
\sin{\theta_{1}}\cos{\theta_{2}}+\cos{\theta_{1}}\sin{\theta_{2}}&-\sin{\theta_{1}}\sin{\theta_{2}}+\cos{\theta_{1}}\cos{\theta_{2}}
\end{pmatrix}$$

$$=\begin{pmatrix}\cos{(\theta_{1}+\theta_{2})}&-\sin{(\theta_{1}+\theta_{2})}\\
\sin{(\theta_{1}+\theta_{2})}&\cos{(\theta_{1}+\theta_{2})}
\end{pmatrix}=R(\theta_{1}+\theta_{2})$$


(b)

The answer to the question is $$R(-\theta)$$

My answer to the question is $$\begin{pmatrix}\cos{\theta}&\sin{\theta}\\
-\sin{\theta}&\cos{\theta} \end{pmatrix}$$

Both answers are correct.

$$\because \begin{pmatrix}\cos{(-\theta)}&-\sin{(-\theta)}\\
\sin{(-\theta)}&\cos{(-\theta)}\end{pmatrix} = \begin{pmatrix}\cos{\theta}&\sin{\theta}\\
-\sin{\theta}&\cos{\theta} \end{pmatrix}$$

$$(\because \sin(-\theta) = -\sin(\theta),\text{ } \cos(-\theta) = \cos(\theta))$$


(c)

$$A = R(\theta)$$

$$A^2 = \begin{pmatrix}\cos{\theta}&-\sin{\theta}\\
\sin{\theta}&\cos{\theta}
\end{pmatrix}\begin{pmatrix}\cos{\theta}&-\sin{\theta}\\
\sin{\theta}&\cos{\theta}
\end{pmatrix}$$

$$=\begin{pmatrix}\cos^2{\theta}-\sin^2{\theta}&-2\sin{\theta}\cos{\theta}\\
2\sin{\theta}\cos{\theta}&\cos^2{\theta}-\sin^2{\theta}
\end{pmatrix} = \begin{pmatrix}\cos{2\theta}&-\sin{2\theta}\\
\sin{2\theta}&\cos{2\theta}
\end{pmatrix}$$

$$(\because \sin{2\theta} = \sin{(\theta+\theta)} = \sin{\theta}\cos{\theta}+\cos{\theta}
sin{\theta} = 2\sin{\theta}\cos{\theta})$$

$$(\because \cos{2\theta} = \cos{(\theta+\theta)} = \cos^2{\theta}-\sin^2{\theta})$$


(d)

$$A=\begin{pmatrix}\cos{\theta}&-\sin{\theta}\\
\sin{\theta}&\cos{\theta}
\end{pmatrix}$$

$$A^{2}=\begin{pmatrix}\cos{2\theta}&-\sin{2\theta}\\
\sin{2\theta}&\cos{2\theta}
\end{pmatrix}$$

$$\vdots$$

$$A^{k} = \begin{pmatrix}\cos{k\theta}&-\sin{k\theta}
\\
\sin{k\theta}&\cos{k\theta}
\end{pmatrix}?$$

Assume True:

$$A^{k} = \begin{pmatrix}\cos{k\theta}&-\sin{k\theta}
\\
\sin{k\theta}&\cos{k\theta}
\end{pmatrix}$$

Show True:

$$A^{k+1} = \begin{pmatrix}\cos{(k+1)\theta}&-\sin{(k+1)\theta}
\\
\sin{(k+1)\theta}&\cos{(k+1)\theta}
\end{pmatrix}$$

<br/>

$$Proof.$$

$$A^{k+1} = A^{k}A = AA^{k} = \begin{pmatrix}\cos{\theta}&-\sin{\theta}\\
\sin{\theta}&\cos{\theta}
\end{pmatrix}\begin{pmatrix}\cos{k\theta}&-\sin{k\theta}\\
\sin{k\theta}&\cos{k\theta}
\end{pmatrix}$$

$$=\begin{pmatrix}\cos{\theta}\cos{k\theta}-\sin{\theta}\sin{k\theta}&-\cos{\theta}\sin{k\theta}-\sin{\theta}\cos{k\theta}\\
\sin{\theta}\cos{k\theta}+\cos{\theta}\sin{k\theta}&-\sin{\theta}\sin{k\theta}+\cos{\theta}\cos{k\theta}
\end{pmatrix}$$

$$=\begin{pmatrix}\cos{(k+1)\theta}&-\sin{(k+1)\theta}
\\
\sin{(k+1)\theta}&\cos{(k+1)\theta}
\end{pmatrix}$$

<br/>

$$\because \begin{pmatrix}\cos{(k+1)\theta}&-\sin{(k+1)\theta}
\\
\sin{(k+1)\theta}&\cos{(k+1)\theta}
\end{pmatrix} = \begin{pmatrix}\cos{k\theta}\cos{\theta}-\sin{k\theta}\sin{\theta}&-(\sin{k\theta}\cos{\theta}+\cos{k\theta}\sin{\theta})\\
\sin{k\theta}\cos{\theta}+\cos{k\theta}\sin{\theta}&\cos{k\theta}\cos{\theta}-\sin{k\theta}\sin{\theta}
\end{pmatrix}$$

<br/>

So $$A^{k+1}$$ is true.

$$\therefore \text{The given statement is true for all k.}$$


## Answer 2

$$Y = R(\theta)X = \begin{pmatrix}\cos{\theta}&-\sin{\theta}\\
\sin{\theta}&\cos{\theta}
\end{pmatrix}\begin{pmatrix}x_{1}\\
x_{2}\end{pmatrix}$$

$$(\because \text{for any vector } X \text{ in } R^2.)$$

$$=\begin{pmatrix}\cos{\theta}&-\sin{\theta}\\
\sin{\theta}&\cos{\theta}
\end{pmatrix}\begin{pmatrix}x1\\
x2\end{pmatrix}=\begin{pmatrix}{x_{1}}\cos{\theta}-{x_{2}}\sin{\theta}\\
{x_{1}}\sin{\theta}+{x_{2}}\cos{\theta}
\end{pmatrix}$$

$$\therefore y_{1} = {x_{1}}\cos{\theta}-{x_{2}}\sin{\theta}, y_{2} = {x_{1}}\sin{\theta}+{x_{2}}\cos{\theta}$$

<br/>

$$Y^{2} = {y_{1}}^2+{y_{2}}^2$$

$$={x_{1}}^2\cos^2{\theta}-2{x_{1}}{x_{2}}\cos{\theta}\sin{\theta}+{x_{2}}^2\sin^2{\theta}+{x_{1}}^2\sin^2{\theta}+2{x_{1}}{x_{2}}\sin{\theta}\cos{\theta}+{x_{2}}^2\cos^2{\theta}$$

$$={x_{1}}^2(\cos^2{\theta}+\sin^2{\theta})-2{x_{1}}{x_{2}}\cos{\theta}\sin{\theta}+2{x_{1}}{x_{2}}\sin{\theta}\cos{\theta}+{x_{2}}^2(\sin^2{\theta}+\cos^2{\theta})$$

$$={x_{1}}^2+{x_{2}}^2$$

$$(\because \sin^2{\theta}+\cos^2{\theta} = 1)$$

$$=X^{2}$$

<br/>

$$\therefore \left\|Y\right\| = \left\|X\right\|.$$

## Answer 3

Let $$B$$ be the matrix given by

$$B = \begin{pmatrix}b_{11}&*&\cdots\cdots&&*\\
0&b_{22}&*&\cdots&*\\
\vdots&&\ddots&&\vdots\\
&&&&*\\
0&\cdots\cdots&0&&b_{nn}\end{pmatrix}$$

Also, The above-mentioned A was:

$$\begin{pmatrix}a_{11}&*&\cdots\cdots&&*\\
0&a_{22}&*&\cdots&*\\
\vdots&&\ddots&&\vdots\\
&&&&*\\
0&\cdots\cdots&0&&a_{nn}\end{pmatrix}$$

Thus,

$$AB = \begin{pmatrix}a_{11}b_{11}&*&\cdots\cdots&&*\\
0&a_{22}b_{22}&*&\cdots&*\\
\vdots&&\ddots&&\vdots\\
&&&&*\\
0&\cdots\cdots&0&&a_{nn}b_{nn}\end{pmatrix}$$

<br/>

$$\therefore \text{The diagonal elements of AB are } a_{11}b_{11}, \cdots, a_{nn}b_{nn}$$