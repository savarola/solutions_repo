# Problem 1: Orbital Period and Orbital Radius

## Motivation

The relationship between the square of the orbital period and the cube of the orbital radius, known as **Kepler's Third Law**, is a cornerstone of celestial mechanics. This law reveals a fundamental connection between time and space in planetary systems and provides the theoretical foundation for understanding orbital motion in gravitational systems.

---

## 1. Derivation of Kepler’s Third Law for Circular Orbits

Consider an object of mass $m$ orbiting a much more massive body (e.g., a planet around the Sun) in a circular orbit of radius $r$.

The gravitational force provides the necessary centripetal force:

$$
F_{\text{gravity}} = F_{\text{centripetal}} \Rightarrow \frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Where:

- $G$ is the gravitational constant,  
- $M$ is the mass of the central body,  
- $v$ is the orbital velocity,  
- $r$ is the orbital radius.

Canceling $m$ and solving for $v$:

$$
v^2 = \frac{G M}{r}
$$

The orbital period $T$ is:

$$
T = \frac{2 \pi r}{v} \Rightarrow T^2 = \left(\frac{2 \pi r}{v}\right)^2 = \frac{4 \pi^2 r^2}{v^2}
$$

Substitute $v^2 = \frac{G M}{r}$:

$$
T^2 = \frac{4 \pi^2 r^2}{\frac{G M}{r}} = \frac{4 \pi^2 r^3}{G M}
$$

**Therefore,**

$$
T^2 \propto r^3
$$

This is **Kepler’s Third Law** for circular orbits.

---

## 2. Implications for Astronomy

- **Determining Planetary Masses**:  
  If T and r of a satellite are known, we can solve for the mass M of the central body:

  M = (4 * π² * r³) / (G * T²)

- **Calculating Orbital Distances**:  
  Given the period T (e.g., from observations), we can calculate the average orbital radius r.

- **Satellite Engineering**:  
  The altitude and speed of satellites in Earth orbit can be precisely determined using this law.

---

## 3. Real-World Examples

### a) The Moon Orbiting Earth

- $T \approx 27.3$ days $= 2.36 \times 10^6$ s  
- $r \approx 3.84 \times 10^8$ m

Plug into:

$$
M_{\text{Earth}} = \frac{4 \pi^2 r^3}{G T^2}
$$

We obtain:  
$M_{\text{Earth}} \approx 5.97 \times 10^{24}$ kg

### b) Planets in the Solar System

The table below shows the empirical validation of $T^2 \propto r^3$ using Solar System data:

| Planet  | $r$ (AU) | $T$ (yr) | $T^2$  | $r^3$  |
|---------|----------|----------|--------|--------|
| Earth   | 1.00     | 1.00     | 1.00   | 1.00   |
| Mars    | 1.52     | 1.88     | 3.53   | 3.51   |
| Jupiter | 5.20     | 11.86    | 140.7  | 140.6  |
| Saturn  | 9.58     | 29.46    | 867.8  | 878.4  |

The close match confirms the law.

![image](https://github.com/user-attachments/assets/798b8c36-005e-4c25-9908-7bcc4bb9a890)

``` python
import numpy as np
import matplotlib.pyplot as plt

# Planet data
planets = ['Mercury', 'Venus', 'Earth', 'Mars']
T_years = [0.2408, 0.6152, 1.000, 1.8808]  # Orbital periods in Earth years
a_AU = [0.387, 0.723, 1.000, 1.524]        # Semi-major axes in astronomical units (AU)

# Calculate T^2 and a^3
T_squared = [T**2 for T in T_years]
a_cubed = [a**3 for a in a_AU]

# Plotting the graph
plt.figure(figsize=(8, 6))
plt.plot(a_cubed, T_squared, 'o-', color='dodgerblue', label='Planets')

# Annotate each planet
for i, name in enumerate(planets):
    plt.text(a_cubed[i] * 1.02, T_squared[i] * 0.98, name)

# Add labels, title, grid, and reference line
plt.title("Kepler's 3rd Law: $T^2$ vs $a^3$", fontsize=14)
plt.xlabel("$a^3$ (AU³)", fontsize=12)
plt.ylabel("$T^2$ (Years²)", fontsize=12)
plt.grid(True)

# Expected reference line with slope = 1 (perfect linear relation)
plt.axline((0, 0), slope=1, color='gray', linestyle='--', label='Expected line (slope = 1)')

plt.legend()
plt.tight_layout()
plt.show()
```
[Visit My Collab](https://colab.research.google.com/drive/129tNF5rjIBYXwBCIZvJQ8oBn96b2wOs6#scrollTo=G8UDWIgkcKoD&line=33&uniqifier=1)
---
## 4. Extension to Elliptical Orbits

Kepler's Third Law also applies to **elliptical orbits**, not just circular ones. In this generalized case, the orbital radius $r$ is replaced by the **semi-major axis** $a$ of the ellipse.

$$
T^2 = \frac{4\pi^2 a^3}{G M}
$$

Where:

- $T$ is the orbital period,
- $a$ is the semi-major axis of the ellipse,
- $G$ is the gravitational constant,
- $M$ is the mass of the central body.

### Implications

- This form of Kepler’s law is valid for **all bound two-body systems**, including:
  - Planets with slightly elliptical orbits,
  - Comets with highly eccentric orbits,
  - Binary star systems,
  - Exoplanets around distant stars.

- Astronomers use it to:
  - **Calculate stellar masses** in binary systems,
  - **Estimate orbital distances** from observed periods,
  - **Model elliptical orbits** in simulations and ephemerides.

### Visualization Suggestion

To visualize an elliptical orbit and highlight the semi-major axis:

- Plot an ellipse using the equation:

  (x² / a²) + (y² / b²) = 1

  where:
  - `a` is the semi-major axis,
  - `b` is the semi-minor axis,
  - The central mass is located at one of the foci.


### Final Remark

Kepler’s Third Law for elliptical orbits can also be written as:

$$
\frac{T^2}{a^3} = \text{constant}
$$

This constant depends only on the gravitational parameter $GM$ of the central body and is **independent of orbital eccentricity** for bound systems.

