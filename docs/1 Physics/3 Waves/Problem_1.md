# Problem 1 
# 🌊 Wave Interference Patterns on a Water Surface

## 📌 Motivation

Interference occurs when waves from different sources overlap, creating new patterns. On a water surface, this is easily observed as ripples from different points meet and form distinctive patterns.

Understanding these patterns helps us grasp the principle of **superposition**, the influence of **phase differences**, and the effects of **multiple wave sources**. We explore this visually using wave simulations for:

- One wave source  
- Two coherent sources  
- Multiple sources placed on a regular polygon (e.g., triangle, square, pentagon)

---

## 📐 Wave Equation for a Circular Disturbance

A circular wave on a water surface from a single point source at $(x_0, y_0)$ is modeled as:

$$
\eta(x, y, t) = \frac{A}{r} \cdot \cos(k r - \omega t + \phi)
$$

Where:

- $\eta(x, y, t)$: Displacement at position $(x, y)$ and time $t$
- $A$: Amplitude of the wave
- $r = \sqrt{(x - x_0)^2 + (y - y_0)^2}$: Distance from source
- $k = \frac{2\pi}{\lambda}$: Wave number
- $\omega = 2\pi f$: Angular frequency
- $\phi$: Initial phase

---

## 💡 Superposition of Multiple Sources

When $N$ sources emit coherent waves, the total displacement is:

$$
\eta_{\text{sum}}(x, y, t) = \sum_{i=1}^{N} \frac{A}{r_i} \cdot \cos(k r_i - \omega t + \phi_i)
$$

Where $r_i = \sqrt{(x - x_i)^2 + (y - y_i)^2}$ is the distance from the $i^{th}$ source.

---

## 🧪 Python Simulation Code (Snippet)

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation

# --- Grid Setup ---
size = 200
x = np.linspace(-10, 10, size)
y = np.linspace(-10, 10, size)
X, Y = np.meshgrid(x, y)

# --- Wave Function ---
def wave_source(X, Y, x0, y0, t, wavelength=1, speed=1):
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    k = 2 * np.pi / wavelength
    omega = k * speed
    return np.sin(k * r - omega * t) / (r + 1e-6)  # avoid division by zero

# --- Source Patterns ---
def get_sources(pattern):
    if pattern == "one":
        return [(0, 0)]
    elif pattern == "two":
        return [(-3, 0), (3, 0)]
    elif pattern == "triangle":
        R = 4
        angles = np.linspace(0, 2*np.pi, 4)[:-1]
        return [(R * np.cos(a), R * np.sin(a)) for a in angles]
    elif pattern == "pentagon":
        R = 5
        angles = np.linspace(0, 2*np.pi, 6)[:-1]
        return [(R * np.cos(a), R * np.sin(a)) for a in angles]

# --- Patterns to Animate ---
patterns = ["one", "two", "triangle", "pentagon"]

# --- Plot Setup ---
fig, ax = plt.subplots(figsize=(6, 6))
heatmap = ax.imshow(np.zeros((size, size)), cmap='coolwarm', vmin=-1, vmax=1, extent=(-10, 10, -10, 10))
title = ax.set_title("")
ax.set_xlabel("x")
ax.set_ylabel("y")

# --- Frame Update Function ---
def update(frame):
    pattern = patterns[(frame // 20) % len(patterns)]  # Change pattern every 20 frames
    t = frame % 20
    sources = get_sources(pattern)
    Z = sum(wave_source(X, Y, sx, sy, t) for sx, sy in sources)
    heatmap.set_data(Z)
    title.set_text(f"Wave Interference: {pattern.capitalize()} ({len(sources)} source{'s' if len(sources) > 1 else ''})")
    return heatmap, title

# --- Create Animation ---
ani = animation.FuncAnimation(fig, update, frames=80, interval=100, blit=False)

# --- Save GIF ---
ani.save("wave_interference_colored.gif", writer="pillow")
plt.close()

print("✅ GIF saved as wave_interference_colored.gif")
```
![wave_interference_colored](https://github.com/user-attachments/assets/63909aaf-fe77-4e8a-b76f-f5561ae9b824)

```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from mpl_toolkits.mplot3d import Axes3D

# --- Grid Setup ---
size = 100  # smaller size for faster rendering
x = np.linspace(-10, 10, size)
y = np.linspace(-10, 10, size)
X, Y = np.meshgrid(x, y)

# --- Wave Function ---
def wave_source(X, Y, x0, y0, t, wavelength=1, speed=1):
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    k = 2 * np.pi / wavelength
    omega = k * speed
    return np.sin(k * r - omega * t) / (r + 1e-6)

# --- Source Patterns ---
def get_sources(pattern):
    if pattern == "one":
        return [(0, 0)]
    elif pattern == "two":
        return [(-3, 0), (3, 0)]
    elif pattern == "triangle":
        R = 4
        angles = np.linspace(0, 2*np.pi, 4)[:-1]
        return [(R * np.cos(a), R * np.sin(a)) for a in angles]
    elif pattern == "pentagon":
        R = 5
        angles = np.linspace(0, 2*np.pi, 6)[:-1]
        return [(R * np.cos(a), R * np.sin(a)) for a in angles]

patterns = ["one", "two", "triangle", "pentagon"]

# --- Plot Setup ---
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')

Z = np.zeros_like(X)
surf = ax.plot_surface(X, Y, Z, cmap='RdBu', vmin=-1, vmax=1, linewidth=0, antialiased=True)

ax.set_zlim(-1, 1)
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Amplitude')
title = ax.set_title("")

# --- Frame Update Function ---
def update(frame):
    pattern = patterns[(frame // 20) % len(patterns)]
    t = frame % 20
    sources = get_sources(pattern)
    Z = sum(wave_source(X, Y, sx, sy, t) for sx, sy in sources)
    ax.clear()  # careful: only light clearing
    surf = ax.plot_surface(X, Y, Z, cmap='RdBu', vmin=-1, vmax=1, linewidth=0, antialiased=True)
    ax.set_zlim(-1, 1)
    ax.set_xlabel('X')
    ax.set_ylabel('Y')
    ax.set_zlabel('Amplitude')
    ax.set_title(f"Wave Interference: {pattern.capitalize()} ({len(sources)} source{'s' if len(sources) > 1 else ''})")
    return surf,

# --- Create Animation ---
ani = animation.FuncAnimation(fig, update, frames=80, interval=100, blit=False)

# --- Save Animation ---
ani.save('/content/wave_interference_3d.gif', writer='pillow')
plt.close()

print("✅ 3D GIF saved as /content/wave_interference_3d.gif")
```
![wave_interference_3d](https://github.com/user-attachments/assets/178ef5a9-ddf3-4307-937b-949065372358)

## 📊 Visualizations

### ✅ One Source — Radial Symmetry

- Circular ripples expanding outward from the center.
- No interference is observed since there is only **one wavefront**.
- The wave pattern is described by:

$$
\eta(x, y, t) = \frac{A}{r} \cdot \cos(k r - \omega t + \phi)
$$

Where:

- $r = \sqrt{(x - x_0)^2 + (y - y_0)^2}$ is the radial distance from the source.
- $k = \frac{2\pi}{\lambda}$ is the wave number.
- $\omega = 2\pi f$ is the angular frequency.

---

### ✅ Two Sources — Classic Interference

- Alternating **constructive** and **destructive** interference zones appear.
- Central regions exhibit **lines of maxima and minima**, depending on the relative phase and path difference.
- The total displacement is given by:

$$
\eta_{\text{sum}}(x, y, t) = \eta_1(x, y, t) + \eta_2(x, y, t)
$$

- Constructive interference occurs when:

$$
\Delta r = n \lambda, \quad n \in \mathbb{Z}
$$

- Destructive interference occurs when:

$$
\Delta r = \left(n + \frac{1}{2}\right)\lambda
$$

---

### ✅ Triangle or Pentagon Configuration

- Multiple coherent sources create **complex and symmetric interference patterns**.
- Patterns form an intricate lattice due to overlapping wavefronts.
- High symmetry and **periodicity** in amplification (constructive interference) and cancellation (destructive interference) regions.
- The total displacement from $N$ sources:

$$
\eta_{\text{sum}}(x, y, t) = \sum_{i=1}^{N} \frac{A}{r_i} \cdot \cos(k r_i - \omega t + \phi_i)
$$

Where each $r_i = \sqrt{(x - x_i)^2 + (y - y_i)^2}$ is the distance from the $i^{\text{th}}$ source.

---

> 📌 These visualizations help reinforce key wave phenomena including superposition, phase difference, and spatial symmetry.
