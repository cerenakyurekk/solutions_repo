# Problem 1
markdown
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
import pandas as pd

# Constants
pi = np.pi
g_standard = 9.81  # Standard value of gravitational acceleration in m/s²

# User input or measured values
L = 1.0  # Length of the pendulum in meters (Example: 1 meter)
ruler_resolution = 0.001  # Ruler resolution in meters (Example: 1 mm)
n = 10  # Number of throws for averaging
T_10_values = np.array([19.8, 20.1, 20.0, 19.9, 20.2, 20.0, 19.7, 20.1, 19.8, 20.0])  # Measured times for 10 oscillations in seconds

# Uncertainty in length (ΔL)
delta_L = ruler_resolution / 2

# Step 1: Calculate the mean time for 10 oscillations and standard deviation
mean_T_10 = np.mean(T_10_values)
std_T = np.std(T_10_values)

# Uncertainty in time for 10 oscillations (ΔT_10)
delta_T_10 = std_T / np.sqrt(n)

# Step 2: Calculate the period (T) for one oscillation
T = mean_T_10 / 10
delta_T = delta_T_10 / 10

# Step 3: Calculate gravitational acceleration (g)
g = (4 * pi**2 * L) / (T**2)

# Step 4: Propagate uncertainties in g
delta_g = g * np.sqrt((delta_L / L)**2 + (2 * delta_T / T)**2)

# Create a simpler DataFrame to display the results
data = {
    'Measured Time for 10 Oscillations (T_10) [s]': T_10_values,
    'Mean Time (T_mean) [s]': np.repeat(mean_T_10, n),
    'Period (T) [s]': np.repeat(T, n),
    'Uncertainty in Time (ΔT) [s]': np.repeat(delta_T, n),
}

# Convert the data into a DataFrame
df = pd.DataFrame(data)

# Add final calculations for g and uncertainty in g
df.loc['Final', :] = ['-', mean_T_10, T, delta_T]

# Display the table
print(df)
print("\nCalculated Gravitational Acceleration (g): {:.4f} m/s²".format(g))
print("Uncertainty in g (Δg): {:.4f} m/s²".format(delta_g))
