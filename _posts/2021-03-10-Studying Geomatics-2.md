---
title: "Geomatics Engineering: 구과량 증명"

classes: wide

categories:
  - Geomatics Engineering
tags:
  - Geomatics Engineering

toc: true
---

# Question

## Girard's Theorem

A spherical triangle on the surface of a sphere of radius $$r$$, with angles $$A, B$$ and $$C$$, has area, $$T$$, given by

$$T = r^{2}(A+B+C-\frac{1}{2}\tau)\text{,}$$

$$\text{where }\tau = 2\pi.$$

<br />

![Figure](/assets/images/geomatics/proof-1.png)

<br />

$$\text{(1) Prove Girard's Theorem.}$$

$$\text{(2) Prove that } \varepsilon^{''} = \frac{T}{r^{2}}\rho^{''}.$$

# Answer

(1)

$$Proof$$

$$\text{A sphere of radius } r \text{ has surface area } 2\tau{r^{2}}.$$

<br />

$$\text{If two great circles meet in a lunar angle }\theta, 0 < \theta \leq{\tau}, \text{then the proportion of surface area which is occupied by the lune they create is } \frac{\theta}{\tau}.$$

$$\therefore \text{ We have area of lune with lunar angle } \theta.$$

$$\frac{\theta}{\tau} \times 2\tau{r^{2}} = 2r^{2}\theta$$

<br />

$$\text{Denote by } L_{A}, L_{B} \text{ and } L_{C} \text{ the areas of the three lunes with angles } A, B \text{ and } C, \text{ respectively}.$$

$$\text{Also, Denote by } T \text{ the area of triangle } ABC;$$

<br />

$$\text{These areas}(L_{A}, L_{B}, L_{C}) \text{ each have an antipodal duplicate.}$$

$$\text{Likewise, } T \text{ also has its antipodal duplicate.}$$

$$\therefore 2L_{A} + 2L_{B} + 2L_{C} = 2r^{2}\tau + 4T$$

<br />

$$T = \frac{1}{2}(L_{A} + L_{B} + L_{C} - r^2\tau)$$

$$= \frac{1}{2}(2r^{2}A + 2r^{2}B + 2r^{2}C - r^{2}\tau)$$

$$= r^{2}(A + B + C - \frac{1}{2}\tau)$$

<br />

(2)

$$Proof$$

$$\text{Let's replace } A + B + C - \frac{1}{2}\tau \text{ with } \varepsilon.$$

$$\therefore T = r^{2}\varepsilon$$

$$\varepsilon = \frac{T}{r^{2}}$$

<br />

$$\text{Here,}$$

$$\rho^{''} = \frac{180^{\circ}}{\pi}$$

$$\therefore \varepsilon^{''} = \frac{T}{r^{2}}\rho^{''}$$












