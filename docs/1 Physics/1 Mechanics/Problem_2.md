# Problem 2
# Investigating the Dynamics of a Forced Damped Pendulum

## Motivation

The forced damped pendulum is a captivating example of a physical system with intricate behavior resulting from the interplay of damping, restoring forces, and external driving forces. By introducing both damping and external periodic forcing, the system demonstrates a transition from simple harmonic motion to a rich spectrum of dynamics, including resonance, chaos, and quasiperiodic behavior. These phenomena serve as a foundation for understanding complex real-world systems, such as driven oscillators, climate systems, and mechanical structures under periodic stress.

Adding forcing introduces new parameters, such as the amplitude and frequency of the external force, which significantly affect the pendulum's behavior. By systematically varying these parameters, a diverse class of solutions can be observed, including synchronized oscillations, chaotic motion, and resonance phenomena. These behaviors not only highlight fundamental physics principles but also provide insights into engineering applications such as energy harvesting, vibration isolation, and mechanical resonance.

## Task

### 1. Theoretical Foundation
- Start with the differential equation governing the motion of a forced damped pendulum:
  
  \[
  \frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \sin\theta = A \cos(\omega t)
  \]
  
- Derive the approximate solutions for small-angle oscillations.
- Explore resonance conditions and their implications for the system's energy.

### 2. Analysis of Dynamics
- Investigate how the damping coefficient, driving amplitude, and driving frequency influence the motion of the pendulum.
- Examine the transition between regular and chaotic motion and their physical interpretations.

### 3. Practical Applications
- Discuss real-world scenarios where the forced damped pendulum model applies, such as in energy harvesting devices, suspension bridges, and oscillating circuits.

### 4. Implementation
- Create a computational model to simulate the motion of a forced damped pendulum.
- Visualize the behavior under various damping, driving force, and initial conditions.
- Plot phase diagrams and Poincaré sections to illustrate transitions to chaos.

## Solution Approach

### 1. Small-Angle Approximation
For small angles (\( \theta \approx 0 \)), we approximate \( \sin\theta \approx \theta \), simplifying the equation to:

\[
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(\omega t)
\]

This is a linear second-order differential equation with a known analytical solution in the form:

\[
\theta(t) = C_1 e^{\lambda_1 t} + C_2 e^{\lambda_2 t} + \theta_p(t)
\]

where:
- \( \lambda_1, \lambda_2 \) are roots of the characteristic equation.
- \( \theta_p(t) \) is the particular solution due to external forcing.
- The behavior depends on whether the system is underdamped, critically damped, or overdamped.

### 2. Numerical Solution for Arbitrary Angles
For larger angles where \( \sin\theta \) cannot be approximated by \( \theta \), we solve the equation numerically using the Runge-Kutta method.

### 3. Python Implementation
We'll integrate the system using the **Runge-Kutta** method for arbitrary angles.

#### Python Code:
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Parameters
g = 9.81  # Gravity (m/s^2)
L = 1.0   # Length of the pendulum (m)
b = 0.5   # Damping coefficient
A = 1.2   # Driving force amplitude
omega = 2.0  # Driving force frequency

# Differential equations
def pendulum(t, y):
    theta, omega_dot = y
    dtheta_dt = omega_dot
    domega_dt = -b * omega_dot - (g / L) * np.sin(theta) + A * np.cos(omega * t)
    return [dtheta_dt, domega_dt]

# Time span and initial conditions
t_span = (0, 50)
t_eval = np.linspace(*t_span, 1000)
y0 = [0.1, 0]  # Initial angle and velocity

# Solve the system
sol = solve_ivp(pendulum, t_span, y0, t_eval=t_eval, method='RK45')

# Plot results
plt.figure(figsize=(10, 5))
plt.plot(sol.t, sol.y[0], label='Theta (rad)')
plt.xlabel('Time (s)')
plt.ylabel('Angle (rad)')
plt.title('Forced Damped Pendulum')
plt.legend()
plt.grid()
plt.show()
```
![alt text](image2.png)


## Deliverables
- A Markdown document with a Python script or notebook implementing the simulations.
- A detailed explanation of the general solutions for the forced damped pendulum.
- Graphical representations of the motion for different damping coefficients, driving amplitudes, and driving frequencies, including resonance and chaotic behavior.
- A discussion on the limitations of the model and potential extensions, such as introducing nonlinear damping or non-periodic driving forces.
- Phase portraits, Poincaré sections, and bifurcation diagrams to analyze transitions to complex dynamics.

## Hints and Resources
- For small angles, approximate \( \sin \theta \approx \theta \) to simplify the differential equation.
- Employ numerical techniques (e.g., Runge-Kutta methods) for exploring the dynamics beyond the small-angle approximation.
- Relate the forced damped pendulum to analogous systems in other fields, such as electrical circuits (driven RLC circuits) or biomechanics (human gait).
- Utilize software tools like Python for simulations and visualizations.

This task bridges theoretical analysis with computational exploration, fostering a deeper understanding of forced and damped oscillatory phenomena and their implications in both physics and engineering.

