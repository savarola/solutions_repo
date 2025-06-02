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

- **Larmor radius**:  
  $$
  r_L = \frac{mv_\perp}{qB}
  $$

- **Drift velocity**:  
  $$
  \vec{v}_d = \frac{\vec{E} \times \vec{B}}{B^2}
  $$

### 4️⃣ Visualization

- 2D and 3D trajectory plots  
- Visual cues for Larmor orbit and drift  
- Color-coded time or velocity representations

---

# 🔌 Circuits – Problem: Simplifying a Resistor Network

## 🎯 Scenario

Given a resistor network between two points (START and END), simplify the circuit using:

- Series and parallel combinations  
- Delta-Y and Y-Delta transformations  
- Visual animations (step-by-step or GIF)

---

## 🧮 Equivalent Resistance Formulas

- **Series combination**:  
  $$
  R_{\text{eq}} = R_1 + R_2 + \dots + R_n
  $$

- **Parallel combination**:  
  $$
  \frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}
  $$

- **Delta to Y (symmetric case)**:  
  $$
  R_Y = \frac{R_\Delta}{3}
  $$

---

## 📦 Deliverables

- A visual explanation of charged particle trajectories under various $\vec{E}$ and $\vec{B}$ fields  
- Labeled illustrations of how resistor networks reduce to simpler equivalents  
- Mathematical derivations with clear parameter definitions  
- Connections to real-world systems like cyclotrons, mass spectrometers, and power grids

---

> ✨ This simulation-based approach enhances intuition for electromagnetic forces and circuit analysis.

