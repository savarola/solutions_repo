# Problem 1
# ⚡ Electromagnetism – Problem 1: Simulating the Effects of the Lorentz Force

## 🎯 Motivation

The Lorentz force governs the motion of charged particles in electromagnetic fields and is described by the equation:

$$
\vec{F} = q\vec{E} + q\vec{v} \times \vec{B}
$$

Where:

- $q$: charge of the particle  
- $\vec{E}$: electric field  
- $\vec{B}$: magnetic field  
- $\vec{v}$: velocity of the particle

This principle is foundational in:

- Plasma physics  
- Cyclotrons and synchrotrons  
- Mass spectrometry  
- Astrophysical plasmas

---

## 🧪 Task Overview

### 1️⃣ Applications of the Lorentz Force

- **Particle Accelerators**: Magnetic fields guide charged particles in circular paths.  
- **Mass Spectrometers**: Charged ions are deflected by $\vec{B}$; trajectory radius reveals mass-to-charge ratio.  
- **Magnetic Confinement**: In tokamaks, $\vec{B}$ confines hot plasma, minimizing loss.

### 2️⃣ Simulating Particle Motion

We numerically solve Newton's second law with the Lorentz force:

$$
m\frac{d\vec{v}}{dt} = q\vec{E} + q\vec{v} \times \vec{B}
$$

Motion types:

- **Uniform $\vec{B}$ only**: Circular or helical motion  
- **Uniform $\vec{E}$ and $\vec{B}$**: Spiral or drift motion  
- **Crossed $\vec{E} \perp \vec{B}$**: $E \times B$ drift behavior

### 3️⃣ Parameter Exploration

We allow variations in:

- Field strengths: $\vec{E}, \vec{B}$  
- Initial velocity: $\vec{v}_0$  
- Particle properties: $q, m$

Phenomena to observe:

Larmor radius: $r_L = \frac{mv_\perp}{qB}$

Drift velocity: $\vec{v}_d = \frac{\vec{E} \times \vec{B}}{B^2}$


### 4️⃣ Visualization

- 2D and 3D trajectory plots  
- Visual cues for Larmor orbit and drift  
- Color-coded time or velocity representations
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.0               # charge [C]
m = 1.0               # mass [kg] — increased to prevent blow-up
dt = 0.001            # smaller time step for better stability
steps = 20000          # number of steps

# Lorentz force equation
def lorentz_force(v, E, B):
    return q * (E + np.cross(v, B))

# Leapfrog (Velocity-Verlet) integration
def simulate_motion(v0, E, B, r0=np.array([0, 0, 0])):
    r = [r0]
    v = [v0]

    # First half-step velocity update (leapfrog)
    a = lorentz_force(v0, E, B) / m
    v_half = v0 + 0.5 * a * dt

    for _ in range(steps):
        # Full step position update
        r_next = r[-1] + v_half * dt
        r.append(r_next)

        # Compute acceleration at new position (based on velocity)
        a = lorentz_force(v_half, E, B) / m

        # Full step velocity update
        v_half = v_half + a * dt
        v.append(v_half - 0.5 * a * dt)  # Store full-step velocity for record

    return np.array(r), np.array(v)

# Fields and initial conditions
B = np.array([0, 0, 1])                 # Uniform magnetic field along z-axis
E = np.array([0, 0, 0])                 # No electric field
v0_spiral = np.array([1.0, 0.0, 0.5])   # Initial velocity with z-component
r0 = np.array([0.0, 0.0, 0.0])          # Starting at origin

# Run simulation
positions, velocities = simulate_motion(v0_spiral, E, B, r0)

# 3D Plot of the trajectory
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(positions[:, 0], positions[:, 1], positions[:, 2])
ax.set_title("Stable Spiral Trajectory in Magnetic Field")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("z")
plt.tight_layout()
plt.show()
```
![fd38344d-9246-40b2-952d-1dad498f8d8b](https://github.com/user-attachments/assets/6e38aa20-a45a-4c84-9388-94e4f5046a84)

---

# 🔌 Circuits – Problem: Simplifying a Resistor Network

## 🎯 Scenario

Given a resistor network between two points (START and END), simplify the circuit using:

- Series and parallel combinations  
- Delta-Y and Y-Delta transformations  
- Visual animations (step-by-step or GIF)

![download](https://github.com/user-attachments/assets/5a29c840-b2d9-4274-9896-31332e12c616)
![download](https://github.com/user-attachments/assets/925176af-6bd6-4aea-9ff0-55bf83136452)
![download](https://github.com/user-attachments/assets/4348b3df-ffc4-4485-a44f-382c2c328b69)
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.0           # charge [C]
m = 1.0           # mass [kg]
dt = 0.01         # time step
steps = 1000      # number of steps

# Lorentz force
def lorentz_force(v, E, B):
    return q * (E + np.cross(v, B))

# Leapfrog integration
def simulate_drift(v0, E, B, r0=np.array([0.0, 0.0, 0.0])):
    r = [r0]
    v = [v0]
    a = lorentz_force(v0, E, B) / m
    v_half = v0 + 0.5 * a * dt

    for _ in range(steps):
        r_next = r[-1] + v_half * dt
        r.append(r_next)
        a = lorentz_force(v_half, E, B) / m
        v_half = v_half + a * dt
        v.append(v_half - 0.5 * a * dt)

    return np.array(r)

# Crossed fields
E = np.array([0, 1.0, 0])         # Electric field in +y direction
B = np.array([0, 0, 1.0])         # Magnetic field in +z direction
v0 = np.array([0.0, 0.0, 0.0])    # Initial velocity = 0
r0 = np.array([0.0, 0.0, 0.0])    # Start at origin

# Run simulation
positions = simulate_drift(v0, E, B, r0)

# 3D plot of drift motion
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(positions[:, 0], positions[:, 1], positions[:, 2])
ax.set_title("3D Drift Motion in Crossed E and B Fields")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("z")
ax.grid(True)
plt.tight_layout()
plt.show()


import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.0     # Charge [C]
m = 1.0     # Mass [kg]
dt = 0.01   # Time step
steps = 1000

# Lorentz force
def lorentz_force(v, E, B):
    return q * (E + np.cross(v, B))

# Leapfrog integration
def simulate_circular_motion(v0, E, B, r0=np.array([0, 0, 0])):
    r = [r0]
    a = lorentz_force(v0, E, B) / m
    v_half = v0 + 0.5 * a * dt

    for _ in range(steps):
        r_next = r[-1] + v_half * dt
        a = lorentz_force(v_half, E, B) / m
        v_half = v_half + a * dt
        r.append(r_next)

    return np.array(r)

# Initial conditions for circular motion
B = np.array([0, 0, 1.0])           # Magnetic field along z
E = np.array([0, 0, 0])             # No electric field
v0 = np.array([1.0, 0.0, 0.0])      # Velocity perpendicular to B
r0 = np.array([0.0, -1.0, 0.0])     # Start off-center for nicer plot

# Run simulation
positions = simulate_circular_motion(v0, E, B, r0)

# 3D plot
fig = plt.figure(figsize=(7, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(positions[:, 0], positions[:, 1], positions[:, 2], lw=2)

ax.set_title("Circular Trajectory in Magnetic Field")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("z")
ax.set_box_aspect([1, 1, 0.3])  # Flatten z-axis
plt.tight_layout()
plt.show()


import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Time array
t = np.linspace(0, 20, 500)

# E x B drift trajectory (example parametric form)
x = t
y = -10 * np.cos(t)  # circular motion in y
z = 0.05 * np.sin(t)  # slight oscillation in z

# Plotting
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot(x, y, z)
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('z')
ax.set_title('E × B Drift of Charged Particle')
plt.show()
```
---

## 🧮 Equivalent Resistance Formulas

### 🔌 Resistor Combinations

- **Series combination**: $R_{\text{eq}} = R_1 + R_2 + \dots + R_n$

- **Parallel combination**: $\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}$

- **Delta to Y (symmetric case)**: $R_Y = \frac{R_\Delta}{3}$


---

## 📦 Deliverables

- A visual explanation of charged particle trajectories under various $\vec{E}$ and $\vec{B}$ fields  
- Labeled illustrations of how resistor networks reduce to simpler equivalents  
- Mathematical derivations with clear parameter definitions  
- Connections to real-world systems like cyclotrons, mass spectrometers, and power grids

---

> ✨ This simulation-based approach enhances intuition for electromagnetic forces and circuit analysis.

