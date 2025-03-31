# Problem 1
# Measuring Earth's Gravitational Acceleration with a Pendulum

## Motivation
The acceleration \( g \) due to gravity is a fundamental constant that influences various physical phenomena. Measuring \( g \) accurately is important for understanding gravitational interactions, designing structures, and conducting experiments. A classic method for determining \( g \) involves measuring the oscillations of a simple pendulum, where the period of oscillation depends on the local gravitational field.

## Task
Measure the acceleration \( g \) due to gravity using a pendulum and analyze the uncertainties in the measurements. This exercise emphasizes precision, uncertainty analysis, and their role in experimental physics.

## Procedure

### 1. Materials
- A string (1 or 1.5 meters long).
- A small weight (e.g., a bag of coins, key chain, or sugar bag) attached to the string.
- Stopwatch (or smartphone timer).
- Ruler or measuring tape.

### 2. Setup
1. Attach the weight to the string and fix the other end to a sturdy support.
2. Measure the length of the pendulum, \( L \), from the suspension point to the center of the weight using a ruler or measuring tape. Record the resolution of the measuring tool and calculate the uncertainty as:
   \[
   \Delta L = \frac{\text{Ruler Resolution}}{2}
   \]

### 3. Data Collection
1. Displace the pendulum slightly (< 15\(^\circ\)) and release it.
2. Measure the time for 10 full oscillations (\( T_{10} \)) and repeat this process 10 times. Record all measurements.
3. Calculate the mean time for 10 oscillations (\( \overline{T}_{10} \)) and the standard deviation (\( \sigma_T \)).
4. Determine the uncertainty in the mean time using:
   \[
   \Delta T_{10} = \frac{\sigma_T}{\sqrt{n}}
   \]
   where \( n = 10 \).

## Calculations

### 1. Calculate the period
\[
T = \frac{\overline{T}_{10}}{10}, \quad \Delta T = \frac{\Delta T_{10}}{10}
\]

### 2. Determine \( g \)
\[
g = \frac{4\pi^2 L}{T^2}
\]

### 3. Propagate uncertainties
\[
\Delta g = g \sqrt{\left( \frac{\Delta L}{L} \right)^2 + \left( 2 \frac{\Delta T}{T} \right)^2}
\]

## Analysis

1. Compare your measured \( g \) with the standard value (9.81 m/s²).
2. Discuss:
   - The effect of measurement resolution on \( \Delta L \).
   - Variability in timing and its impact on \( \Delta T \).
   - Any assumptions or experimental limitations.
 
 
```python
import numpy as np
# Given values
T_10 = 20.190  # Mean time for 10 oscillations in seconds
std_T = 0.120  # Standard deviation in seconds
delta_T_10 = 0.038  # Uncertainty in mean time for 10 oscillations in seconds

# Period for one oscillation (calculated earlier)
T = 2.019  # Period of one oscillation in seconds
delta_T = 0.004  # Uncertainty in period in seconds

# Length of the pendulum (assumed for calculation purposes)
L = 1.0  # Length of the pendulum in meters (example)

# Gravitational acceleration (calculated earlier)
g_measured = 9.685  # Measured gravitational acceleration in m/s²
delta_g_measured = 0.038  # Uncertainty in g in m/s²

# Calculation of gravitational acceleration using the formula
# g = (4 * pi^2 * L) / T^2
pi = np.pi
g_calculated = (4 * pi**2 * L) / (T**2)

# Propagate the uncertainty in g
# Uncertainty in g = g * sqrt((delta_L / L)^2 + (2 * delta_T / T)^2)
delta_L = 0.001  # Uncertainty in length, assume 1 mm uncertainty in measurement
delta_g = g_calculated * np.sqrt((delta_L / L)**2 + (2 * delta_T / T)**2)

# Print the results
print(f"Measured Gravitational Acceleration (g): {g_measured:.4f} m/s²")
print(f"Uncertainty in g: ±{delta_g_measured:.4f} m/s²")
print(f"Calculated Gravitational Acceleration (g): {g_calculated:.4f} m/s²")
print(f"Uncertainty in g from calculations: ±{delta_g:.4f} m/s²")
