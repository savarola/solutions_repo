# Problem 2: Investigating the Dynamics of a Forced Damped Pendulum

## Motivation

The forced damped pendulum represents a fascinating example of nonlinear dynamics. When both damping and external forcing are introduced, the pendulum displays a wide array of behaviors—from simple periodic motion to resonance and chaos. These dynamics mirror those found in systems such as climate models, mechanical resonators, and electrical circuits.

## 1. Theoretical Foundation

The motion of a forced damped pendulum is governed by the second-order nonlinear differential equation:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \sin\theta = A \cos(\omega t)
$$

Where:

- $\theta$ is the angular displacement,
- $b$ is the damping coefficient,
- $g$ is the acceleration due to gravity,
- $L$ is the length of the pendulum,
- $A$ is the amplitude of the driving force,
- $\omega$ is the driving frequency.

### Small-Angle Approximation

For small $\theta$, we can use the approximation $\sin\theta \approx \theta$, reducing the equation to:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(\omega t)
$$

This is a linear non-homogeneous differential equation with a general solution composed of a transient (homogeneous) and a steady-state (particular) solution.

### Resonance

Resonance occurs when the driving frequency $\omega$ is close to the natural frequency of the system:

$$
\omega_0 = \sqrt{\frac{g}{L}}
$$

At resonance, the system can exhibit large amplitude oscillations, especially when damping is low ($b \ll 1$). The amplitude of steady-state oscillations is maximized near resonance.

## 2. Analysis of Dynamics

To study the system numerically, we convert the second-order equation into two first-order ODEs:

Let:
- $\theta_1 = \theta$
- $\theta_2 = \frac{d\theta}{dt}$

Then:

$$
\frac{d\theta_1}{dt} = \theta_2
$$

$$
\frac{d\theta_2}{dt} = -b \theta_2 - \frac{g}{L} \sin\theta_1 + A \cos(\omega t)
$$

### Parameter Effects

- **Damping ($b$)**: Reduces amplitude and can suppress chaotic behavior.
- **Driving Amplitude ($A$)**: Higher values can induce chaotic behavior.
- **Driving Frequency ($\omega$)**: Determines resonance conditions and the potential for complex behavior.

### Transition to Chaos

As parameters (e.g., $A$, $\omega$) are varied, the system transitions from periodic to quasiperiodic, and eventually to chaotic motion. Indicators include:

- Sensitivity to initial conditions,
- Strange attractors in phase space,
- Irregular time series.

## 3. Practical Applications

- **Energy Harvesting Devices**: Use resonant mechanical systems to convert vibrational energy.
- **Suspension Bridges**: Modeled using driven oscillators under periodic loading.
- **Oscillating Electrical Circuits**: Analogous to forced damped pendulums (e.g., RLC circuits).
- **Biomechanics**: Human gait and limb motion can be approximated by driven pendulums.

## 4. Implementation

### Python Simulation Outline

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Parameters
g = 9.81
L = 1.0
b = 0.5
A = 1.2
omega = 2/3

# ODE System
def pendulum(t, y):
    theta, omega_dot = y
    dtheta_dt = omega_dot
    domega_dt = -b * omega_dot - (g / L) * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# Initial conditions
y0 = [0.2, 0.0]

# Time span
t_span = (0, 100)
t_eval = np.linspace(*t_span, 5000)

# Solve ODE
sol = solve_ivp(pendulum, t_span, y0, t_eval=t_eval)

# Plot theta vs time
plt.plot(sol.t, sol.y[0])
plt.xlabel("Time (s)")
plt.ylabel("Theta (rad)")
plt.title("Forced Damped Pendulum")
plt.grid()
plt.show()

import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Parameters
g, L, b, A, omega = 9.81, 1.0, 0.5, 1.2, 2/3
t_span = (0, 100)
t_eval = np.linspace(*t_span, 5000)
y0 = [0.2, 0.0]

def pendulum(t, y):
    theta, omega_dot = y
    return [omega_dot, -b * omega_dot - (g / L) * np.sin(theta) + A * np.cos(omega * t)]

sol = solve_ivp(pendulum, t_span, y0, t_eval=t_eval)

plt.figure(figsize=(10, 4))
plt.plot(sol.t, sol.y[0])
plt.xlabel('Time $t$')
plt.ylabel('Angle $\\theta(t)$')
plt.title('Forced Damped Pendulum - Time Series')
plt.grid()
plt.savefig("theta_time_series.png")
