# Kepler's Third Law: The Relationship Between Orbital Period and Orbital Radius

## 1. Introduction and Motivation

Kepler’s Third Law is a cornerstone of celestial mechanics, describing a precise mathematical relationship between the square of a celestial body's orbital period and the cube of its orbital radius. This relationship is not only key to understanding planetary motion in our Solar System but also plays a fundamental role in astrophysics, satellite dynamics, and the study of exoplanetary systems.

In its Newtonian form, this law connects orbital motion with gravitational force, enabling calculations of mass, orbital distance, and period for various celestial objects.

---

## 2. Deriving Kepler's Third Law for Circular Orbits

Consider a small object of mass $m$ orbiting a much larger central mass $M$ in a circular path. The gravitational force provides the required centripetal force:

$$
F_{\text{gravity}} = F_{\text{centripetal}}
$$

Using Newton's law of gravitation and the centripetal force formula:

$$
\frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Canceling $m$ from both sides:

$$
v^2 = \frac{G M}{r}
$$

The orbital period $T$ is the time to complete one full orbit:

$$
T = \frac{2\pi r}{v}
$$

Substitute $v$:

$$
T = \frac{2\pi r}{\sqrt{\frac{G M}{r}}} = 2\pi \sqrt{\frac{r^3}{G M}}
$$

Squaring both sides:

$$
T^2 = \frac{4\pi^2 r^3}{G M}
$$

Thus, Kepler’s Third Law shows that for a fixed central mass $M$:

$$
T^2 \propto r^3
$$

---

## 3. Astronomical Implications

Kepler’s Third Law is instrumental in modern astronomy for several reasons:

- **Mass Estimation**: We can estimate the mass of a star or planet using the orbital radius and period of an orbiting body:

  $$
  M = \frac{4\pi^2 r^3}{G T^2}
  $$

- **Predicting Orbits**: If we know the radius of orbit, we can predict the period (or vice versa).
- **Exploring Other Systems**: The law is widely used to analyze exoplanets, binary stars, and artificial satellites.

---

## 4. Real-World Examples

### 4.1 The Moon's Orbit Around the Earth

- Radius: $r = 3.84 \times 10^8$ m  
- Period: $T = 27.3$ days $\approx 2.36 \times 10^6$ s

Estimate Earth's mass:

$$
M = \frac{4\pi^2 r^3}{G T^2}
$$

Python code:

```python
import numpy as np

G = 6.67430e-11  # gravitational constant
r = 3.84e8       # meters
T = 2.36e6       # seconds

M = 4 * np.pi**2 * r**3 / (G * T**2)
print(f"Estimated mass of Earth: {M:.2e} kg")
```
### 4.2 Planets in the Solar System
Plotting $T^2$ vs. $r^3$ for all planets in the Solar System shows a linear relationship, confirming Kepler's Law. On a log-log plot, the slope should be approximately 1.
## 5. Computational Simulation
We can simulate the relationship between orbital period and radius using Python:
```python
import numpy as np
import matplotlib.pyplot as plt

G = 6.67430e-11
M = 1.989e30  # Sun's mass (kg)

# Orbital radii from 0.1 AU to 30 AU
radii = np.linspace(0.1, 30, 100) * 1.496e11
T_squared = (4 * np.pi**2 * radii**3) / (G * M)

plt.figure(figsize=(8, 6))
plt.plot(radii**3, T_squared, label="$T^2$ vs $r^3$")
plt.xlabel("Orbital Radius Cubed ($r^3$) [m³]")
plt.ylabel("Orbital Period Squared ($T^2$) [s²]")
plt.title("Kepler's Third Law Verification")
plt.grid(True)
plt.legend()
plt.savefig("kepler_relation.png")
plt.show()
```
## 6. Extension to Elliptical Orbits

Kepler’s Third Law is not limited to circular orbits. It can be generalized to **elliptical orbits** by replacing the orbital radius $r$ with the **semi-major axis** $a$ of the ellipse. The semi-major axis is the average distance between the orbiting body and the central mass over one complete orbit.

The generalized form of Kepler's Third Law becomes:

$$
T^2 = \frac{4\pi^2 a^3}{G M}
$$

Where:

- $T$ is the orbital period,
- $a$ is the semi-major axis of the ellipse,
- $G$ is the gravitational constant,
- $M$ is the mass of the central object.

This version of the law applies to:

- **Planets** in the Solar System (whose orbits are elliptical, not perfectly circular),
- **Moons** orbiting planets,
- **Binary star systems**,
- **Exoplanets** orbiting distant stars.

The law still shows the same proportionality:

$$
T^2 \propto a^3
$$

This means that even in non-circular orbits, the square of the period is still proportional to the cube of the orbit’s size — a powerful result that applies to virtually all orbital systems in the universe.
