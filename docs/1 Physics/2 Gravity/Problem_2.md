# Problem 2: Escape Velocities and Cosmic Velocities

## Motivation

The concept of escape velocity is crucial for understanding the energy required to overcome the gravitational pull of a celestial body. The first, second, and third cosmic velocities define the minimum speeds needed to:

1. Maintain a stable orbit near the surface,
2. Escape the celestial body's gravity,
3. Escape the Sun's gravitational influence from a planet's orbit.

These concepts are fundamental for satellite launches, planetary missions, and interstellar travel planning.

---

## 1. Definitions and Physical Meanings

- **First Cosmic Velocity ($v_1$)**: The minimum horizontal speed required for an object to enter a circular orbit just above the surface of a planet (low Earth orbit).  
- **Second Cosmic Velocity ($v_2$)**: The escape velocity — the minimum speed required to break free from a planet's gravitational field without further propulsion.  
- **Third Cosmic Velocity ($v_3$)**: The velocity needed to escape the solar system from a given planet's orbit (e.g., Earth), overcoming the Sun's gravity.

---

## 2. Derivation of the Three Cosmic Velocities

### a) First Cosmic Velocity ($v_1$)

Using the balance between centripetal force and gravitational force:

$$
\frac{G M m}{R^2} = \frac{m v_1^2}{R}
\Rightarrow v_1 = \sqrt{\frac{G M}{R}}
$$

Where:

- $G$: Gravitational constant ($6.674 \times 10^{-11} \ \text{m}^3 \text{kg}^{-1} \text{s}^{-2}$),
- $M$: Mass of the planet,
- $R$: Radius of the planet.

---

### b) Second Cosmic Velocity ($v_2$)

Derived from energy conservation: total mechanical energy must be zero to escape.

$$
\frac{1}{2} m v_2^2 - \frac{G M m}{R} = 0
\Rightarrow v_2 = \sqrt{\frac{2 G M}{R}} = \sqrt{2} \cdot v_1
$$

---

### c) Third Cosmic Velocity ($v_3$)

Escape velocity from the **Sun** starting from orbit around a planet (e.g. Earth):

$$
v_3 = \sqrt{v_{\text{esc,Sun}}^2 - v_{\text{orbital}}^2}
= \sqrt{\frac{2 G M_{\odot}}{r} - \frac{G M_{\odot}}{r}} = \sqrt{\frac{G M_{\odot}}{r}}
$$

Where $r$ is the orbital radius of the planet from the Sun.

---

## 3. Python Calculations and Visualization

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # m^3 kg^-1 s^-2

# Celestial body data: (name, mass [kg], radius [m], orbital radius from Sun [m])
bodies = {
    "Earth":   (5.972e24, 6.371e6, 1.496e11),
    "Moon":    (7.347e22, 1.737e6, 3.844e8 + 1.496e11),
    "Mars":    (6.417e23, 3.390e6, 2.279e11),
    "Jupiter": (1.898e27, 6.991e7, 7.785e11),
}

M_sun = 1.989e30

results = {}

for body, (M, R, r_sun) in bodies.items():
    v1 = np.sqrt(G * M / R)
    v2 = np.sqrt(2 * G * M / R)
    v3 = np.sqrt(G * M_sun / r_sun)
    results[body] = (v1, v2, v3)

# Print results
print("Cosmic Velocities (m/s):")
print(f"{'Body':<10} {'v1':>10} {'v2':>10} {'v3':>10}")
for body, (v1, v2, v3) in results.items():
    print(f"{body:<10} {v1:10.0f} {v2:10.0f} {v3:10.0f}")

# Bar plot
labels = list(results.keys())
v1_vals = [results[b][0] for b in labels]
v2_vals = [results[b][1] for b in labels]
v3_vals = [results[b][2] for b in labels]

x = np.arange(len(labels))
width = 0.25

plt.figure(figsize=(10,6))
plt.bar(x - width, v1_vals, width, label='First Cosmic Velocity')
plt.bar(x, v2_vals, width, label='Second Cosmic Velocity')
plt.bar(x + width, v3_vals, width, label='Third Cosmic Velocity')
plt.xticks(x, labels)
plt.ylabel('Velocity (m/s)')
plt.title('Comparison of Cosmic Velocities')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

