# Trajectories of a Freely Released Payload Near Earth

## Motivation

When an object is released from a moving rocket near Earth, its trajectory depends on initial conditions and gravitational forces. This scenario presents a rich problem, blending principles of orbital mechanics and numerical methods. Understanding the potential trajectories is vital for space missions, such as deploying payloads or returning objects to Earth.

## 1. Possible Trajectories of a Payload

### 1.1 Types of Trajectories

When a payload is released from a moving object near Earth, its trajectory depends on the initial velocity and position. The main types of trajectories are:
- **Parabolic Trajectory:** The object follows a parabolic path when its velocity is less than the escape velocity but enough to travel away from the Earth.
- **Hyperbolic Trajectory:** The object follows a hyperbolic trajectory when its velocity is greater than the escape velocity.
- **Elliptical Trajectory:** The object follows an elliptical path when the velocity is not enough to escape Earth's gravity, resulting in an orbit.

### 1.2 Deriving the Equation of Motion

The motion of the payload can be described by Newton’s Law of Gravitation and the equations of motion. The gravitational force between two objects (Earth and the payload) is given by:

$$
F = \frac{GMm}{r^2}
$$

where:
- $G$ is the gravitational constant ($6.67430 \times 10^{-11} \, \text{m}^3 \, \text{kg}^{-1} \, \text{s}^{-2}$),
- $M$ is the mass of Earth ($5.972 \times 10^{24} \, \text{kg}$),
- $m$ is the mass of the payload,
- $r$ is the distance between the payload and the center of Earth.

The equations of motion can then be derived from this gravitational force, and numerical methods are used to simulate the motion over time.
![image-4](https://github.com/user-attachments/assets/d895314c-2f6c-46c5-a682-de817a66f48d)
``` python
import numpy as np
import matplotlib.pyplot as plt

# Гравитационные константы
G = 6.67430e-11  # м^3 кг^-1 с^-2
M = 5.972e24     # масса Земли, кг
R_earth = 6.371e6  # радиус Земли, м

# Начальные условия
altitude = 800e3  # 800 км над поверхностью
r0 = np.array([R_earth + altitude, 0])  # начальная позиция справа от Земли
velocities = np.arange(5e3, 13.5e3, 0.5e3)  # скорости от 5 до 13 км/с

# Временные параметры
dt = 1  # шаг по времени (с)
T = 10000  # общее время моделирования (с)
steps = int(T / dt)

# Создание графика
fig, ax = plt.subplots(figsize=(8, 8))
theta = np.linspace(0, 2 * np.pi, 500)
earth_x = R_earth * np.cos(theta)
earth_y = R_earth * np.sin(theta)
ax.fill(earth_x, earth_y, 'b', label='Земля', alpha=0.5)

# Симуляция для каждой скорости
colors = plt.cm.viridis(np.linspace(0, 1, len(velocities)))

for v0, color in zip(velocities, colors):
    r = r0.copy()
    v = np.array([0, v0])
    traj_x, traj_y = [], []

    for _ in range(steps):
        r_mag = np.linalg.norm(r)
        if r_mag < R_earth:  # если груз врезался в Землю
            break
        a = -G * M * r / r_mag**3
        v += a * dt
        r += v * dt
        traj_x.append(r[0])
        traj_y.append(r[1])

    ax.plot(traj_x, traj_y, label=f'{v0/1000:.1f} км/с', color=color)

# Оформление графика
ax.set_aspect('equal')
ax.set_xlim(-2e7, 2e7)
ax.set_ylim(-2e7, 2e7)
ax.set_xlabel('x (м)')
ax.set_ylabel('y (м)')
ax.set_title('Траектории груза при сбросе с высоты 800 км')
ax.legend(loc='upper right', fontsize='small')
plt.grid(True)
plt.tight_layout()
plt.show()
```
[Visit My Collab](https://colab.research.google.com/drive/129tNF5rjIBYXwBCIZvJQ8oBn96b2wOs6#scrollTo=AxILuY4Zhebe&line=56&uniqifier=1)
## 2. Numerical Analysis of the Payload's Path

### 2.1 Initial Conditions and Setup

For the simulation, we set the initial position of the payload at an altitude of 800 km above Earth's surface. The Earth's radius is approximately 6371 km, so the initial distance from the center of Earth is:

$$
r_{\text{initial}} = 6371 \, \text{km} + 800 \, \text{km} = 7171 \, \text{km}
$$

We also release the payload with different initial velocities (5 km/s, 5.5 km/s, ..., up to 13 km/s). Each velocity results in a different trajectory, and we will simulate and visualize these paths.

### 2.2 Equations of Motion

The equations of motion are based on Newton's second law:

$$
m \ddot{r} = -\frac{GMm}{r^2}
$$

where $\ddot{r}$ is the acceleration, and the negative sign indicates that the force is attractive (towards the Earth). The simulation involves solving this differential equation numerically using methods like Euler's method or the Runge-Kutta method.

## 3. Computational Tool and Visualization

A computational tool can be used to simulate and visualize the trajectory of the payload under Earth's gravity. This involves solving the equations of motion numerically for different initial velocities. The results will be plotted as the distance from Earth's center over time.

### 3.1 Explanation of the Python Code

The simulation involves updating the position and velocity of the payload at each time step using the gravitational force equation. The payload is released at 800 km above Earth's surface with varying initial velocities (from 5 km/s to 13 km/s). The Earth is represented as a reference point at the surface level, and the trajectory is computed numerically.

### 3.2 Visualizing the Trajectories

The plot generated from the simulation shows the trajectories of the payload for different initial velocities. The trajectories are plotted as a function of time, with the Earth's surface marked as a reference.
![download](https://github.com/user-attachments/assets/544c1912-62d5-4e31-8a84-068eb95da5ed) ![download](https://github.com/user-attachments/assets/872cb650-335b-4c5a-bbb9-6fb3bfdae46f)
``` python
# --- Imports ---
import numpy as np
import matplotlib.pyplot as plt

# --- Physical Constants ---
G = 6.67430e-11  # gravitational constant, m^3 kg^-1 s^-2
AU = 1.496e11    # 1 astronomical unit (average Earth-Sun distance), m
day = 24 * 3600  # seconds in one day
year = 365.25 * day  # seconds in one year

# --- Kepler's Third Law Formula ---
# T^2 = (4π²/GM) * R³
# => M = (4π² R³) / (G T²)

def mass_from_orbit(R, T):
    return (4 * np.pi**2 * R**3) / (G * T**2)

# --- 1. Finding the Mass of the Sun from Earth's Orbit ---
R_earth_orbit = AU        # Earth's orbit radius (m)
T_earth_orbit = year      # Earth's orbital period (s)

M_sun = mass_from_orbit(R_earth_orbit, T_earth_orbit)
print(f"☀️ Mass of the Sun ≈ {M_sun:.2e} kg")

# --- 2. Finding the Mass of the Earth from the Moon's Orbit ---
# Parameters of the Moon's orbit:
R_moon_orbit = 384400e3   # average distance to the Moon (m)
T_moon_orbit = 27.32 * day  # Moon's orbital period (s)

M_earth = mass_from_orbit(R_moon_orbit, T_moon_orbit)
print(f"🌍 Mass of the Earth ≈ {M_earth:.2e} kg")

# --- 3. Plotting T² vs R³ ---

# Example planetary data (Solar System planets)
radii = np.array([
    57.9e9,   # Mercury
    108.2e9,  # Venus
    149.6e9,  # Earth
    227.9e9,  # Mars
    778.5e9,  # Jupiter
    1433e9,   # Saturn
    2877e9,   # Uranus
    4503e9    # Neptune
])

periods_days = np.array([
    88,        # Mercury
    224.7,     # Venus
    365.25,    # Earth
    687,       # Mars
    4331,      # Jupiter
    10747,     # Saturn
    30589,     # Uranus
    59800      # Neptune
])

# Convert to seconds
periods_seconds = periods_days * day

# Calculate T² and R³
T_squared = periods_seconds**2
R_cubed = radii**3

# --- Plot T² vs R³ ---
plt.figure(figsize=(8,6))
plt.plot(R_cubed, T_squared, 'o-', label="Planets")
plt.xlabel('$R^3$ (m³)', fontsize=12)
plt.ylabel('$T^2$ (s²)', fontsize=12)
plt.title('Dependence of $T^2$ on $R^3$ (Kepler\'s Third Law)', fontsize=14)
plt.grid(True)
plt.legend()
plt.show()

# --- 4. Checking the linear relation (log-log plot) ---
plt.figure(figsize=(8,6))
plt.plot(np.log10(R_cubed), np.log10(T_squared), 'o-', label="Planets")
plt.xlabel('log($R^3$)', fontsize=12)
plt.ylabel('log($T^2$)', fontsize=12)
plt.title('Log-Log Plot: $T^2$ vs $R^3$', fontsize=14)
plt.grid(True)
plt.legend()
plt.show()
```
[Visit My Collab](https://colab.research.google.com/drive/129tNF5rjIBYXwBCIZvJQ8oBn96b2wOs6#scrollTo=HVu3rMDNhEtx&line=83&uniqifier=1)
## 4. Discussion on Orbital Insertion, Reentry, and Escape

- **Orbital Insertion:** If the payload's initial velocity is below escape velocity but high enough to prevent it from falling back to Earth, it will enter an elliptical orbit.
- **Reentry:** If the velocity is too low, the payload will follow a parabolic trajectory and eventually reenter Earth's atmosphere.
- **Escape Velocity:** If the initial velocity is equal to or greater than the escape velocity, the payload will follow a hyperbolic trajectory and escape Earth's gravitational influence.

## 5. Conclusion

This analysis and simulation provide a clear understanding of how a payload's initial velocity affects its trajectory when released near Earth. By adjusting the initial conditions, we can model different space missions, such as satellite deployment or payload return.
