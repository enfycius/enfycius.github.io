---
title: "Linear Algebra: Matrices and Linear Equations - Multiplication of Matrices - Question #1"

classes: wide

categories:
  - Linear Algebra
tags:
  - Mathematics
  - Linear Algebra

toc: true
---

# Question

[Reference - Question2](https://enfycius.github.io/linear%20algebra/Studying_Linear-3/)

Because it is just rotation, the negative rotation is described by positive rotation.

Therefore, if $$y^2 = x^2$$ is shown to be established, regardless of whether its root is positive or negative, is the proof completed?

<br/>

# Answer

Below is a reply from Jaemin Shin, PhD.

You need know the definition of $$\left\|\cdot\right\|$$, called the norm, first. There are several ways to define the norm but in general in $$R^{2}$$ it is defines as follows (called 2-norm); for $$X = \mathbf{(x_{1}, x_{2})}^\top \in R^2$$

$$\left\|X\right\| = \sqrt{\left\|x_{1}\right\|^2 + \left\|x_{2}\right\|^2}$$

or it is equivalent to

$$\left\|X\right\| = (\mathbf{X}^{\top}X)^{\frac{1}{2}}$$

Here $$\mathbf{X}^\top$$ is the transpose of the vector. $$$$ Note that

$$\mathbf{(AB)}^\top = \mathbf{B}^\top\mathbf{A}^\top$$

and

$$\mathbf{R(\theta)}^\top = R(\theta)^{-1} = R(-\theta)$$

Thus,

$$\left\|Y\right\|^{2} = \left\|RX\right\|^{2} = \mathbf{(RX)}^{\top}(RX)=(\mathbf{X}^{\top}\mathbf{R}^{\top})(RX)$$

Using the associative law

$$(\mathbf{X}^{\top}\mathbf{R}^{\top})(RX) = \mathbf{X}^{\top}(\mathbf{R}^{\top}R)X = \mathbf{X}^{\top}(R^{-1}R)X = \mathbf{X}^{\top}X = \left\|X\right\|^2$$

Since the norm is non-negative, it follows that

$$\left\|Y\right\| = \left\|X\right\|.$$

