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

## 4. Discussion on Orbital Insertion, Reentry, and Escape

- **Orbital Insertion:** If the payload's initial velocity is below escape velocity but high enough to prevent it from falling back to Earth, it will enter an elliptical orbit.
- **Reentry:** If the velocity is too low, the payload will follow a parabolic trajectory and eventually reenter Earth's atmosphere.
- **Escape Velocity:** If the initial velocity is equal to or greater than the escape velocity, the payload will follow a hyperbolic trajectory and escape Earth's gravitational influence.

## 5. Conclusion

This analysis and simulation provide a clear understanding of how a payload's initial velocity affects its trajectory when released near Earth. By adjusting the initial conditions, we can model different space missions, such as satellite deployment or payload return.
