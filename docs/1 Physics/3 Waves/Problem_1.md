# Problem 1
# Interference Patterns on a Water Surface

## Motivation
Interference occurs when waves from different sources overlap, creating new patterns. On a water surface, this can be easily observed when ripples from different points meet, forming distinctive interference patterns. These patterns show how waves combine in different ways, either reinforcing each other or canceling out.

Studying these patterns helps us understand wave behavior in a simple, visual way. It also allows us to explore important concepts, like the relationship between wave phase and the effects of multiple sources. This task offers a hands-on approach to learning about wave interactions and their real-world applications, making it an interesting and engaging way to dive into wave physics.

---

## Task
A circular wave on the water surface, emanating from a point source located at \((x_0, y_0)\), can be described by the Single Disturbance equation:

\[
\eta(x, y, t) = \frac{A}{\sqrt{r}} \cos(kr - \omega t + \phi)
\]

where:

- \( \eta(x, y, t) \) is the displacement of the water surface at point \((x, y)\) and time \( t \),
- \( A \) is the amplitude of the wave,
- \( k = \frac{2\pi}{\lambda} \) is the wave number, related to the wavelength \( \lambda \),
- \( \omega = 2\pi f \) is the angular frequency, related to the frequency \( f \),
- \( r = \sqrt{(x - x_0)^2 + (y - y_0)^2} \) is the distance from the source to the point \( (x, y) \),
- \( \phi \) is the initial phase.

---

## Problem Statement
Your task is to analyze the interference patterns formed on the water surface due to the superposition of waves emitted from point sources placed at the vertices of a chosen regular polygon.

---

## Steps to Follow
1. **Select a Regular Polygon:** Choose a regular polygon (e.g., equilateral triangle, square, regular pentagon).
2. **Position the Sources:** Place point wave sources at the vertices of the selected polygon.
3. **Wave Equations:** Write the equations describing the waves emitted from each source, considering their respective positions.
4. **Superposition of Waves:** Apply the principle of superposition by summing the wave displacements at each point on the water surface:

   \[
   \eta_{\text{sum}}(x, y, t) = \sum_{i=1}^{N} \eta_i (x, y, t)
   \]

   where \( N \) is the number of sources (vertices of the polygon).

5. **Analyze Interference Patterns:** Examine the resulting displacement \( \eta_{\text{sum}}(x, y, t) \) as a function of position \( (x, y) \) and time \( t \). Identify regions of constructive interference (wave amplification) and destructive interference (wave cancellation).
6. **Visualization:** Present your findings graphically, illustrating the interference patterns for the chosen regular polygon.

---

## Considerations
- Assume all sources emit waves with the same amplitude \( A \), wavelength \( \lambda \), and frequency \( f \).
- The waves are coherent, maintaining a constant phase difference.
- You may use simulation and visualization tools such as Python (with libraries like Matplotlib) or other graphical software to aid in your analysis.

---

## Deliverables
1. A Markdown document with a Python script or notebook implementing the simulations.
2. A detailed explanation of the interference patterns observed for the chosen regular polygon with the goal of understanding wave superposition.
3. Graphical representations of the water surface showing constructive and destructive interference regions.


```python

import numpy as np
import matplotlib.pyplot as plt

# Parameters
A = 1.0    # Amplitude of waves
wavelength = 1.0  # Wavelength of waves
k = 2 * np.pi / wavelength  # Wave number
f = 1.0    # Frequency of waves
omega = 2 * np.pi * f  # Angular frequency
t = 0  # Time snapshot

# Define polygon source positions (equilateral triangle as an example)
n_sources = 3  # Number of sources (vertices of polygon)
radius = 5  # Radius of the polygon
angles = np.linspace(0, 2 * np.pi, n_sources, endpoint=False)
source_positions = [(radius * np.cos(a), radius * np.sin(a)) for a in angles]

# Define spatial grid
x = np.linspace(-10, 10, 400)
y = np.linspace(-10, 10, 400)
X, Y = np.meshgrid(x, y)

# Compute wave superposition
wave_sum = np.zeros_like(X)
for x0, y0 in source_positions:
    r = np.sqrt((X - x0)*2 + (Y - y0)*2)
    wave_sum += A * np.cos(k * r - omega * t)

# Plot interference pattern
plt.figure(figsize=(8, 6))
plt.imshow(wave_sum, extent=[-10, 10, -10, 10], cmap='RdBu', origin='lower')
plt.colorbar(label='Wave Amplitude')
plt.title('Wave Interference Pattern')
plt.xlabel('X Position')
plt.ylabel('Y Position')
plt.scatter(*zip(*source_positions), color='black', marker='o', label='Wave Sources')
plt.legend()
plt.show()


```
![alt text](wave.png)
