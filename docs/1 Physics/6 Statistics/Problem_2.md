# Problem 2: Estimating $\pi$ Using Monte Carlo Methods

## 🎯 Motivation

Monte Carlo simulations harness randomness to approximate values or solve complex problems numerically. A classic example is the estimation of $\pi$ using geometric probability. These simulations demonstrate fundamental connections between probability, geometry, and numerical computation.

We explore two Monte Carlo approaches:

1. Estimating $\pi$ using random points in a square and a unit circle.
2. Estimating $\pi$ using Buffon's Needle experiment.

---

## Part 1: Estimating $\pi$ Using a Circle

### 📐 1. Theoretical Foundation

Consider a unit circle inscribed in a square of side length 2 (from $[-1, 1]$ on both axes). The area of the circle is:

$$
A_{\text{circle}} = \pi r^2 = \pi (1)^2 = \pi
$$

The area of the square is:

$$
A_{\text{square}} = (2)^2 = 4
$$

If we randomly distribute points inside the square, the proportion of points that fall inside the circle should be approximately equal to the ratio of the circle's area to the square's area:

$$
\frac{\text{Points inside circle}}{\text{Total points}} \approx \frac{\pi}{4}
$$

Solving for $\pi$:

$$
\pi \approx 4 \cdot \left( \frac{\text{Points inside circle}}{\text{Total points}} \right)
$$

![1 5](https://github.com/user-attachments/assets/5769c175-baa4-4e20-bf84-15a59dbf311c)

 ```python
import numpy as np
import matplotlib.pyplot as plt

# Nokta sayısı
n = 10000

# Rastgele (x, y) noktaları üret
x = np.random.uniform(-1, 1, n)
y = np.random.uniform(-1, 1, n)

# Dairenin içinde olup olmadığını kontrol et
inside = x**2 + y**2 <= 1

# Pi tahmini
pi_estimate = 4 * np.sum(inside) / n

# Görselleştirme
plt.figure(figsize=(6, 6))
plt.scatter(x[inside], y[inside], s=1, color='darkgreen', label='Inside Circle')
plt.scatter(x[~inside], y[~inside], s=1, color='crimson', label='Outside Circle')
plt.gca().set_aspect('equal')
plt.title(f"Monte Carlo π Estimate ({n} points)\nπ ≈ {pi_estimate:.6f}")
plt.legend()
plt.grid(True)
plt.show()
 ```
---

### 🧪 2. Simulation

Steps:
- Generate $N$ random $(x, y)$ points in $[-1, 1] \times [-1, 1]$.
- Count how many satisfy $x^2 + y^2 \leq 1$ (inside the circle).
- Estimate $\pi$ using the formula above.

---

### 📊 3. Visualization

- Plot all generated points.
- Highlight points inside the circle in one color (e.g., green).
- Points outside in another color (e.g., red).
- Optionally, draw the boundary of the unit circle.

---

### 📈 4. Analysis

- Run simulations for increasing $N$ (e.g., $100, 1000, 10^4, 10^5$).
- Record the estimate of $\pi$ at each $N$.
- Plot $\pi$ estimates vs. $N$ to observe convergence.
- Discuss computational time and accuracy.

---
## Part 2: Estimating $\pi$ Using Buffon's Needle

### 📐 1. Theoretical Foundation

Buffon's Needle experiment involves dropping a needle of length $l$ on a plane with parallel lines spaced $d$ units apart. If $l \leq d$, the probability $P$ that the needle crosses a line is:

$$
P = \frac{2l}{\pi d}
$$

Rearranged to estimate $\pi$:

$$
\pi \approx \frac{2l \cdot N}{d \cdot C}
$$

Where:
- $N$ = number of needle drops
- $C$ = number of crosses (intersections with a line)

---

### 🧪 2. Simulation

Steps:
- Set needle length $l$ and line spacing $d$ (commonly $l = d = 1$).
- Drop the needle $N$ times:
  - Randomly place its center $y \in [0, d/2]$
  - Randomly select angle $\theta \in [0, \pi/2]$
- If $y \leq \frac{l}{2} \sin(\theta)$, it's a hit (crossing).
- Use above formula to estimate $\pi$.

---

### 📊 3. Visualization

- Show parallel lines spaced $d$ units apart.
- Draw needles as lines across drops.
- Use different colors for crossing vs non-crossing needles.

---

### 📈 4. Analysis

- Vary number of drops $N$: $100, 1000, 10000, \ldots$
- Record number of crossings $C$ and $\pi$ estimate.
- Compare with the circle-based method:
  - Which one converges faster?
  - Which one is more stable?
  - Discuss runtime and sensitivity to randomness.

---

## 🧾 Definitions and Key Concepts

- **Monte Carlo Method**: A computational algorithm relying on repeated random sampling to obtain numerical results.
- **Unit Circle**: Circle with radius $r = 1$ centered at origin.
- **Buffon's Needle**: Classical probability problem estimating $\pi$ from geometric probabilities.
- **Convergence Rate**: How fast an estimate approaches the true value as the number of samples increases.

---

## 📈 Deliverables

### 1. Markdown Document:
- Includes all theory, explanations, and observations.

### 2. Python Simulations:
- One script for the unit circle method.
- One script for Buffon’s Needle method.

### 3. Visual Outputs:
- Scatter plots of circle simulation.
- Needle-drop visualizations.
- $\pi$ vs number of samples graphs.

### 4. Comparative Analysis:
- Table of $\pi$ estimates vs sample size.
- Commentary on computational efficiency and accuracy.

---

## 🔗 References

- Grinstead, C. M., & Snell, J. L. (1997). *Introduction to Probability*.
- Wikipedia: [Monte Carlo method](https://en.wikipedia.org/wiki/Monte_Carlo_method)
- Wikipedia: [Buffon's needle](https://en.wikipedia.org/wiki/Buffon%27s_needle)

