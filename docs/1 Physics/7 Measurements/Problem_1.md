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
import math

# Function to simulate measuring the time for 10 oscillations
def measure_time_for_10_oscillations(num_measurements=10):
    times = np.random.normal(loc=20.0, scale=0.5, size=num_measurements)  # Simulate 10 measurements with mean and std deviation
    return times

# Constants
L = 1.0  # Length of pendulum in meters
ruler_resolution = 0.01  # Resolution of measuring tool in meters
n = 10  # Number of measurements
true_gravity = 9.81  # True value of gravity in m/s^2

# Uncertainty in Length
delta_L = ruler_resolution / 2

# Simulating the data collection
times_10_oscillations = measure_time_for_10_oscillations(num_measurements=n)

# Calculate the mean time and standard deviation for 10 oscillations
mean_time_10 = np.mean(times_10_oscillations)
std_time_10 = np.std(times_10_oscillations)

# Calculate the uncertainty in the mean time
delta_T_10 = std_time_10 / np.sqrt(n)

# Calculate the period of a single oscillation
T = mean_time_10 / 10
delta_T = delta_T_10 / 10

# Calculate gravitational acceleration using the formula
g = (4 * np.pi**2 * L) / T**2

# Propagate uncertainties to calculate uncertainty in g
delta_g = g * np.sqrt((delta_L / L)**2 + (2 * delta_T / T)**2)

# Tabulated data
data = {
    'Measurement #': np.arange(1, n+1),
    'Time for 10 Oscillations (s)': times_10_oscillations,
    'Mean Time for 10 Oscillations (s)': mean_time_10,
    'Standard Deviation of Time (s)': std_time_10,
    'Uncertainty in Time for 10 Oscillations (s)': delta_T_10
}

df = pd.DataFrame(data)

# Display the table
print("Tabulated Data for Pendulum Measurements:")
print(df)

# Display the calculated values for g and uncertainty
print("\nCalculated Values:")
print(f"Mean Time for 10 Oscillations: {mean_time_10:.4f} s")
print(f"Period of One Oscillation: {T:.4f} s")
print(f"Calculated g: {g:.4f} m/s^2")
print(f"Uncertainty in g: {delta_g:.4f} m/s^2")

# Compare with true value of g
print(f"\nDifference from true value of g ({true_gravity} m/s^2): {abs(g - true_gravity):.4f} m/s^2")

