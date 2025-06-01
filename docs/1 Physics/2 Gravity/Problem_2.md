# Escape Velocities and Cosmic Velocities

## Motivation

The concept of escape velocity is crucial for understanding the conditions required to leave a celestial body's gravitational influence. The first, second, and third cosmic velocities define the thresholds for orbiting, escaping, and leaving a star system. These principles underpin modern space exploration, from launching satellites to interplanetary missions.

## 1. Cosmic Velocities: Definitions and Derivations

### 1.1 First Cosmic Velocity (Orbital Velocity)

The first cosmic velocity is the velocity required for an object to enter a stable orbit around a celestial body without any additional propulsion. It is derived from balancing the centrifugal force (due to circular motion) with the gravitational force acting on the object.

The formula for the orbital velocity is:

$$
v_1 = \sqrt{\frac{GM}{R}}
$$

where:
- $G$ is the gravitational constant ($6.67430 \times 10^{-11} \, \text{m}^3 \, \text{kg}^{-1} \, \text{s}^{-2}$),
- $M$ is the mass of the celestial body,
- $R$ is the radius of the celestial body.

### 1.2 Second Cosmic Velocity (Escape Velocity)

The second cosmic velocity is the velocity required for an object to break free from a celestial body's gravitational influence, assuming no other forces (like atmospheric drag) are acting on it. It is derived from the energy required to escape the gravitational field.

The escape velocity is given by:

$$
v_2 = \sqrt{\frac{2GM}{R}}
$$

where:
- $G$ is the gravitational constant,
- $M$ is the mass of the celestial body,
- $R$ is the radius of the celestial body.

### 1.3 Third Cosmic Velocity (Heliocentric Escape Velocity)

The third cosmic velocity is the velocity required for an object to escape the gravitational influence of the Sun (i.e., to leave the Solar System). It is derived from the combination of the escape velocity from Earth and the velocity required to overcome the Sun's gravity.

The third cosmic velocity is given by:

$$
v_3 = \sqrt{v_2^2 + v_{\text{Sun}}^2}
$$

where:
- $v_2$ is the second cosmic velocity (escape velocity from the Earth),
- $v_{\text{Sun}}$ is the orbital velocity of the Earth around the Sun, which is approximately $29.78 \, \text{km/s}$.

### 1.4 Mathematical Parameters Affecting Cosmic Velocities

The velocities depend on:
- The mass ($M$) of the celestial body,
- The radius ($R$) of the celestial body,
- The gravitational constant ($G$),
- The orbital velocity of Earth around the Sun for the third cosmic velocity.

## 2. Calculation and Values for Earth

### 2.1 First Cosmic Velocity for Earth

For Earth, we use the following values:
- $M_{\text{Earth}} = 5.972 \times 10^{24} \, \text{kg}$,
- $R_{\text{Earth}} = 6.378 \times 10^{6} \, \text{m}$.

Substituting into the formula for $v_1$:

$$
v_1 = \sqrt{\frac{(6.67430 \times 10^{-11}) (5.972 \times 10^{24})}{6.378 \times 10^{6}}}
$$

This yields:

$$
v_1 \approx 7.12 \, \text{km/s}
$$

### 2.2 Second Cosmic Velocity for Earth

Using the same values for Earth, the second cosmic velocity is:

$$
v_2 = \sqrt{\frac{2(6.67430 \times 10^{-11}) (5.972 \times 10^{24})}{6.378 \times 10^{6}}}
$$

This gives:

$$
v_2 \approx 11.2 \, \text{km/s}
$$

### 2.3 Third Cosmic Velocity for Earth

To calculate the third cosmic velocity, we use the value of the second cosmic velocity for Earth and the orbital velocity of the Earth around the Sun ($v_{\text{Sun}} = 29.78 \, \text{km/s}$):

$$
v_3 = \sqrt{(11.2)^2 + (29.78)^2}
$$

This yields:

$$
v_3 \approx 32.2 \, \text{km/s}
$$
## 3. 🚀 Derivation of the First and Second Cosmic Velocities

### 1️⃣ First Cosmic Velocity (Orbital Velocity)

The first cosmic velocity is the minimum speed an object needs to stay in a stable circular orbit near the Earth's surface without propulsion.

Using Newton’s law of gravitation and centripetal force:

$$
F_{\text{gravity}} = F_{\text{centripetal}} \Rightarrow \frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Cancel $m$ and solve for $v$:

$$
v = \sqrt{\frac{G M}{r}}
$$

Where:

- $G$: Gravitational constant  
- $M$: Mass of the planet (e.g., Earth)  
- $r$: Radius from center of the planet  
- $v$: First cosmic (orbital) velocity

---

### 2️⃣ Second Cosmic Velocity (Escape Velocity)

Escape velocity is the minimum speed needed for an object to escape a planet's gravitational field without further propulsion.

Using conservation of energy:

$$
\frac{1}{2} m v^2 - \frac{G M m}{r} = 0
$$

Solving for $v$:

$$
v = \sqrt{\frac{2 G M}{r}}
$$

This is **higher** than the first cosmic velocity by a factor of $\sqrt{2}$:

$$
v_{\text{escape}} = \sqrt{2} \cdot v_{\text{orbital}}
$$

---

### 📘 Summary

- First Cosmic Velocity: $v_1 = \sqrt{\frac{G M}{r}}$
- Second Cosmic Velocity: $v_2 = \sqrt{\frac{2 G M}{r}}$
- Relationship: $v_2 = \sqrt{2} \cdot v_1$

## 4. Comparison with Other Celestial Bodies

### 4.1 Moon

For the Moon, the mass and radius are as follows:
- $M_{\text{Moon}} = 7.347 \times 10^{22} \, \text{kg}$,
- $R_{\text{Moon}} = 1.737 \times 10^{6} \, \text{m}$.

Using the formulas for $v_1$ and $v_2$, we can calculate the first and second cosmic velocities for the Moon. The third cosmic velocity would be the same as for Earth, since the Moon is orbiting the Earth, and the third cosmic velocity is primarily influenced by the Earth's position relative to the Sun.

### 4.2 Mars

For Mars:
- $M_{\text{Mars}} = 6.4171 \times 10^{23} \, \text{kg}$,
- $R_{\text{Mars}} = 3.396 \times 10^{6} \, \text{m}$.

Again, using the formulas for $v_1$ and $v_2$, we can compute these values for Mars.

### 4.3 Jupiter

For Jupiter:
- $M_{\text{Jupiter}} = 1.898 \times 10^{27} \, \text{kg}$,
- $R_{\text{Jupiter}} = 6.991 \times 10^{7} \, \text{m}$.

Similarly, the first and second cosmic velocities for Jupiter can be calculated, and the third cosmic velocity will again be affected by the position of Jupiter relative to the Sun.

![image-2](https://github.com/user-attachments/assets/e2204abe-da06-4cf6-bfab-0bbde7d859f8)
``` python
import matplotlib.pyplot as plt

bodies = ["Moon", "Earth", "Mars", "Jupiter"]
v1 = [1.68, 7.9, 3.6, 42.1]
v2 = [2.38, 11.2, 5.0, 59.5]

x = range(len(bodies))

plt.bar(x, v1, width=0.4, label="1st Cosmic Velocity", align='center')
plt.bar([i + 0.4 for i in x], v2, width=0.4, label="2nd Cosmic Velocity", align='center')

plt.xticks([i + 0.2 for i in x], bodies)
plt.ylabel("Velocity (km/s)")
plt.title("Comparison of Cosmic Velocities")
plt.legend()
plt.grid(axis='y')
plt.show()
```
[Visit My Collab](https://colab.research.google.com/drive/129tNF5rjIBYXwBCIZvJQ8oBn96b2wOs6#scrollTo=qUl9FuiNcsPC&line=17&uniqifier=1)
## 5. Importance in Space Exploration

### 5.1 Launching Satellites

The first cosmic velocity is important for placing satellites into stable orbits around Earth. Achieving this velocity ensures that the satellite remains in orbit without falling back to the surface.

### 5.2 Missions to Other Planets

The second cosmic velocity is crucial for missions aiming to escape Earth's gravitational influence, such as interplanetary missions. This velocity allows spacecraft to escape Earth’s gravity and travel to other planets.

### 5.3 Potential for Interstellar Travel

The third cosmic velocity is important when considering missions that aim to leave the Solar System entirely. While this velocity is beyond current technological capabilities, it is theoretically important for interstellar travel.

## 6. Conclusion

Understanding the first, second, and third cosmic velocities is essential for modern space exploration, as these velocities determine the thresholds for orbital dynamics, escape, and interstellar missions.
