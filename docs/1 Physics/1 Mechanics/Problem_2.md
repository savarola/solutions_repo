# Investigating the Dynamics of a Forced Damped Pendulum

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
![image-6](https://github.com/user-attachments/assets/83529e9a-8130-4745-84b4-6857aaba3106)
![image-7](https://github.com/user-attachments/assets/e31fbf78-23e9-4d27-a9c2-f2a250f32d36)
![image-8](https://github.com/user-attachments/assets/8a65cf3d-7a63-4a31-9c2a-06f722a0e315)
![image-9](https://github.com/user-attachments/assets/1a2c80fc-0238-42e4-a624-c5f8a289cee2)
![image-10](https://github.com/user-attachments/assets/b5fd4fae-4688-4b28-b4b0-d9e33ce54901)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Уравнение маятника: d²θ/dt² + b*dθ/dt + sin(θ) = A*cos(ω*t)
def pendulum(t, y, b, A, omega):
    theta, omega_ = y
    dtheta_dt = omega_
    domega_dt = -b * omega_ - np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# Визуализация: графики θ(t) и (θ, ω)
def plot_pendulum(t, sol, title, color):
    theta = sol[0]
    omega = sol[1]

    fig, ax = plt.subplots(1, 2, figsize=(14, 4))
    fig.suptitle(title, fontsize=16)

    ax[0].plot(t, theta, color=color)
    ax[0].set_title("Time Series")
    ax[0].set_xlabel("Time (s)")
    ax[0].set_ylabel("Angle (rad)")
    ax[0].grid(True)

    ax[1].plot(theta, omega, color=color)
    ax[1].set_title("Phase Portrait")
    ax[1].set_xlabel("θ (rad)")
    ax[1].set_ylabel("ω (rad/s)")
    ax[1].grid(True)

    plt.tight_layout()
    plt.subplots_adjust(top=0.85)  # чтобы заголовок не налезал
    plt.show()

# Параметры моделирования
t_span = (0, 30)
t_eval = np.linspace(*t_span, 2000)
initial_state = [0.1, 0.0]  # начальный угол и угловая скорость

# ===== 1. Simple Pendulum =====
sol1 = solve_ivp(pendulum, t_span, initial_state, t_eval=t_eval, args=(0.0, 0.0, 0.0))
plot_pendulum(sol1.t, sol1.y, "1) Simple Pendulum (b=0, A=0)", "crimson")

# ===== 2. Damped Pendulum =====
sol2 = solve_ivp(pendulum, t_span, initial_state, t_eval=t_eval, args=(0.5, 0.0, 0.0))
plot_pendulum(sol2.t, sol2.y, "2) Damped Pendulum (b=0.5, A=0)", "darkblue")

# ===== 3. Forced Pendulum =====
sol3 = solve_ivp(pendulum, t_span, initial_state, t_eval=t_eval, args=(0.0, 1.0, 2.0))
plot_pendulum(sol3.t, sol3.y, "3) Forced Pendulum (b=0, A=1.0, ω=2.0)", "teal")

# ===== 4. Forced Damped Pendulum =====
sol4 = solve_ivp(pendulum, t_span, initial_state, t_eval=t_eval, args=(0.2, 1.2, 2.0))
plot_pendulum(sol4.t, sol4.y, "4) Forced Damped Pendulum (b=0.2, A=1.2, ω=2.0)", "orange")

# ===== 5. Chaotic / Resonant Pendulum =====
sol5 = solve_ivp(pendulum, t_span, initial_state, t_eval=t_eval, args=(0.5, 1.5, 2/3))
plot_pendulum(sol5.t, sol5.y, "5) Chaotic / Resonant Pendulum (b=0.5, A=1.5, ω=2/3)", "firebrick")
```
[Visit My Collab](https://colab.research.google.com/drive/109lrp068uFr13UuE4VJkmi05Ge6HLrbp#scrollTo=avf3de6KWdl0)
