# Problem 2
# Escape Velocities and Cosmic Velocities

## Motivation

Understanding escape and cosmic velocities is fundamental in space exploration, as these velocities determine the conditions required for objects to overcome gravitational influences, achieve stable orbits, or depart from celestial systems.&#8203;:contentReference[oaicite:0]{index=0}

## Definitions and Physical Meanings

1. **First Cosmic Velocity (Orbital Velocity):**
   - **Definition:** :contentReference[oaicite:1]{index=1}&#8203;:contentReference[oaicite:2]{index=2}
   - **Physical Meaning:** :contentReference[oaicite:3]{index=3}&#8203;:contentReference[oaicite:4]{index=4}
   - **Formula:** 
     $$
     v_1 = \sqrt{\frac{G M}{r}}
     $$
     Where:
     - *G* is the gravitational constant (6.67430 × 10⁻¹¹ m³ kg⁻¹ s⁻²)
     - *M* is the mass of the celestial body
     - *r* is the distance from the center of the celestial body to the object

2. **Second Cosmic Velocity (Escape Velocity):**
   - **Definition:** :contentReference[oaicite:5]{index=5}&#8203;:contentReference[oaicite:6]{index=6}
   - **Physical Meaning:** :contentReference[oaicite:7]{index=7}&#8203;:contentReference[oaicite:8]{index=8}
   - **Formula:** 
     $$
     v_2 = \sqrt{\frac{2 G M}{r}}
     $$
     Where:
     - *G* is the gravitational constant
     - *M* is the mass of the celestial body
     - *r* is the distance from the center of the celestial body to the object

3. **Third Cosmic Velocity:**
   - **Definition:** :contentReference[oaicite:9]{index=9}&#8203;:contentReference[oaicite:10]{index=10}
   - **Physical Meaning:** :contentReference[oaicite:11]{index=11}&#8203;:contentReference[oaicite:12]{index=12}
   - **Formula:** 
     $$
     v_3 = \sqrt{\frac{2 G M_{\text{star}}}{r_{\text{star}}} + \frac{2 G M_{\text{planet}}}{r_{\text{planet}}}}
     $$
     Where:
     - *M_star* and *M_planet* are the masses of the star and planet, respectively
     - *r_star* and *r_planet* are the distances from the object to the star and planet, respectively

## Derivations and Parameters Affecting These Velocities

:contentReference[oaicite:13]{index=13}&#8203;:contentReference[oaicite:14]{index=14}

:contentReference[oaicite:15]{index=15}&#8203;:contentReference[oaicite:16]{index=16}

:contentReference[oaicite:17]{index=17}&#8203;:contentReference[oaicite:18]{index=18}

**Key Parameters Influencing These Velocities:**

- **Mass of the Celestial Body (M):** :contentReference[oaicite:19]{index=19}&#8203;:contentReference[oaicite:20]{index=20}
- **Radius or Distance (r):** :contentReference[oaicite:21]{index=21}&#8203;:contentReference[oaicite:22]{index=22}
- **Gravitational Constant (G):** :contentReference[oaicite:23]{index=23}&#8203;:contentReference[oaicite:24]{index=24}

## Calculations and Visualizations for Earth, Mars, and Jupiter

Using the provided formulas, we can calculate these velocities for Earth, Mars, and Jupiter.

**Earth:**

- **First Cosmic Velocity (Orbital Velocity):**
  :contentReference[oaicite:25]{index=25}&#8203;:contentReference[oaicite:26]{index=26}
- **Second Cosmic Velocity (Escape Velocity):**
  :contentReference[oaicite:27]{index=27}&#8203;:contentReference[oaicite:28]{index=28}

**Mars:**

- **First Cosmic Velocity (Orbital Velocity):**
  :contentReference[oaicite:29]{index=29}&#8203;:contentReference[oaicite:30]{index=30}
- **Second Cosmic Velocity (Escape Velocity):**
  :contentReference[oaicite:31]{index=31}&#8203;:contentReference[oaicite:32]{index=32}

**Jupiter:**

- **First Cosmic Velocity (Orbital Velocity):**
  :contentReference[oaicite:33]{index=33}&#8203;:contentReference[oaicite:34]{index=34}
- **Second Cosmic Velocity (Escape Velocity):**
  :contentReference[oaicite:35]{index=35}&#8203;:contentReference[oaicite:36]{index=36}

*Note: The third cosmic velocity calculations are complex, involving interactions between multiple celestial bodies and are typically calculated using numerical methods and simulations.*

## Importance in Space Exploration

- **Launching Satellites:** :contentReference[oaicite:37]{index=37}&#8203;:contentReference[oaicite:38]{index=38}
- **Missions to Other Planets:** :contentReference[oaicite:39]{index=39}&#8203;:contentReference[oaicite:40]{index=40}
- **Interstellar Travel:** 
::contentReference[oaicite:41]{index=41}
 
```python
import numpy as np
import matplotlib.pyplot as plt

# Gravitational constant in m^3 kg^-1 s^-2
G = 6.67430e-11

# Define a function to calculate escape velocity
def escape_velocity(mass, radius):
    return np.sqrt((2 * G * mass) / radius)

# Define a function to calculate first cosmic velocity (orbital velocity)
def orbital_velocity(mass, radius):
    return np.sqrt((G * mass) / radius)

# Data for celestial bodies: mass in kg, radius in meters
celestial_bodies = {
    'Earth': {'mass': 5.972e24, 'radius': 6.371e6},
    'Mars': {'mass': 6.4171e23, 'radius': 3.3895e6},
    'Jupiter': {'mass': 1.8982e27, 'radius': 6.9911e7}
}

# Initialize lists to store velocities
escape_velocities = []
orbital_velocities = []
labels = []

# Calculate velocities for each celestial body
for body, data in celestial_bodies.items():
    escape_vel = escape_velocity(data['mass'], data['radius'])
    orbit_vel = orbital_velocity(data['mass'], data['radius'])
    escape_velocities.append(escape_vel)
    orbital_velocities.append(orbit_vel)
    labels.append(body)

# Set up the bar width and positions
bar_width = 0.35
index = np.arange(len(labels))

# Create the plot
fig, ax = plt.subplots(figsize=(10, 6))

# Plot escape velocities
bar1 = ax.bar(index, escape_velocities, bar_width, label='Escape Velocity (m/s)', color='b')

# Plot orbital velocities
bar2 = ax.bar(index + bar_width, orbital_velocities, bar_width, label='Orbital Velocity (m/s)', color='g')

# Add labels and title
ax.set_xlabel('Celestial Body')
ax.set_ylabel('Velocity (m/s)')
ax.set_title('Escape and Orbital Velocities of Earth, Mars, and Jupiter')
ax.set_xticks(index + bar_width / 2)
ax.set_xticklabels(labels)
ax.legend()

# Display the plot
plt.tight_layout()
plt.show()




![alt text](image6.png)
