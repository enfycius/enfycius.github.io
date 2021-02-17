---
title: "Linear Algebra: Matrices and Linear Equations - Multiplication of Matrices #1"

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

Let $$A$$, $$B$$ be square matrices of the same size, and assume that $$AB = BA$$.

Show that

$$(A+B)^{2} = A^{2} + 2AB + B^{2}$$, and $$(A+B)(A-B) = A^{2} - B^{2}$$,

using the distributive law.

## Question 2

Let $$A, B$$ be two square matrices of the same size. We say that $$A$$ is **similar** to $$B$$ if there exists an invertible matrix $$T$$ such that $$B = TAT^{-1}$$. Suppose this is the case. Prove:

(a) $$B$$ is similar to $$A$$.

(b) $$A$$ is invertible if and only if $$B$$ is invertible.

(c) $$\mathbf{A}^\top$$ is similar to $$\mathbf{B}^\top$$.

(d) Suppose $$A^{n} = O$$ and $$B$$ is an invertible matrix of the same size as $$A$$. Show that $$(BAB^{-1})^{n} = O$$.


## Question 3

(a) Find a $$2 \times 2$$ matrix $$A$$ such that $$A^{2} = -I = \begin{pmatrix}-1&0\\
0&-1\end{pmatrix}$$.

<br/>

# Answer

## Answer 1

$$(A+B)^{2} = (A+B)(A+B) = A^{2} + AB + BA + B^{2}$$

$$(\text{By the way, } AB = BA)$$

$$\therefore A^{2} + AB + BA + B^{2} = A^{2} + AB + AB + B^{2} = A^{2} + 2AB + B^{2}$$

<br/>

$$(A+B)(A-B) = A^{2} - AB + BA -B^{2}$$

$$(\text{By the way, } AB = BA)$$

$$\therefore A^{2} - AB + BA -B^{2} =  A^{2} - AB + AB -B^{2} = A^{2}-B^{2}$$ 

## Answer 2

(a)

$$B = TAT^{-1}$$

$$T^{-1}BT = T^{-1}TAT^{-1}T$$

$$T^{-1}BT = IAI$$

$$(\because T^{-1}T = TT^{-1} = I)$$

$$T^{-1}BT = A$$

$$(\because AI = IA = A)$$

$$\therefore A = T^{-1}BT$$

(b)

$$Proof.$$

$$B \text{ is invertible.}$$

$$\therefore BB^{-1} = B^{-1}B = I$$

$$\text{(1) } BB^{-1} = TAT^{-1}B^{-1} = I$$

$$(\because B = TAT^{-1})$$

$$T^{-1}BB^{-1}T = T^{-1}TAT^{-1}B^{-1}T = I$$

$$T^{-1}TAT^{-1}B^{-1}T = IAT^{-1}B^{-1}T = I$$

$$(\because T \text { is invertible, } T^{-1}T = TT^{-1} = I)$$

$$IAT^{-1}B^{-1}T = AT^{-1}B^{-1}T = I$$

$$(\because AI = IA = A)$$

<br/>

$$\text{(2) } B^{-1}B = B^{-1}TAT^{-1} = I$$

$$(\because B = TAT^{-1})$$

$$T^{-1}B^{-1}BT = T^{-1}B^{-1}TAT^{-1}T = I$$

$$T^{-1}B^{-1}TAT^{-1}T = T^{-1}B^{-1}TAI = I$$

$$(\because T \text { is invertible, } T^{-1}T = TT^{-1} = I)$$

$$T^{-1}B^{-1}TAI = T^{-1}B^{-1}TA = I$$

$$(\because AI = IA = A)$$

<br/>

$$AT^{-1}B^{-1}T = T^{-1}B^{-1}TA = I$$

$$\therefore A \text{ is invertible}$$

(c)

$$B = TAT^{-1}$$

$$\mathbf{B}^\top = \mathbf{(TAT^{-1})}^\top$$

$$\mathbf{(TAT^{-1})}^\top = \mathbf{(T^{-1})}^\top \mathbf{A}^\top \mathbf{T}^\top$$

$$(\because \text{By the rule for the traspose of a product.})$$

$$\text{Let's replace } \mathbf{(T^{-1})}^\top \text{with } C.$$

$$\mathbf{B}^\top = \mathbf{(T^{-1})}^\top \mathbf{A}^\top \mathbf{T}^\top = C \mathbf{A}^\top C^{-1}$$

$$\therefore \mathbf{A}^\top \text{ is similar to } \mathbf{B}^\top$$

(d)

$$(BAB^{-1})^{n} = O$$

$$(B^{-1}BAB^{-1}B)^{n} = O$$

$$(B^{-1}BAB^{-1}B)^{n} = (IAI)^{n}$$

$$(\because \text{B is invertible, } BB^{-1} = B^{-1}B = I)$$

$$(IAI)^{n} = (A)^{n}$$

$$(\because AI = IA = A)$$

$$(\text{By the way, } (A)^{n} = O)$$

$$\therefore (BAB^{-1})^{n} = O$$

## Answer 3

The answer to the question is $$\begin{pmatrix}0&1\\
-1&0\end{pmatrix}$$.

My answer to the question is $$\begin{pmatrix}i&0\\
0&i\end{pmatrix}$$.

> According to the Jaemin Shin, PhD, my answer is correct. However, he also said my answer is still incorrect. Since the range of value is not specified in the question, it seems to be limited to a real number.

So the answer to the question is $$\begin{pmatrix}0&1\\
-1&0\end{pmatrix}$$.