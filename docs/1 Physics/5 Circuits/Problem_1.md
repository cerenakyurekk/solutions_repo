# What is an Electric Circuit?

An **electric circuit** is a closed path that enables **electric current** to flow. It generally consists of:

- A **power source** (e.g., battery or generator)
- **Conductive wires** for carrying the current
- One or more **electrical components** (e.g., resistors, switches, bulbs)

> ✅ A circuit must be **complete** and **unbroken** to function — allowing charges to circulate continuously.

![Simple Circuit Diagram](./Pictures/simple_circuit_diagram.png)

---

# Calculating Equivalent Resistance Using Graph Theory

In **graph theory**, a resistor network can be represented as a graph where:

- **Nodes (vertices)** = circuit junctions
- **Edges** = resistors (edge weight = resistance)

## Method Overview

1. **Model** the circuit as an undirected weighted graph.
2. **Construct the conductance matrix** (1/R for each resistor).
3. **Build the Laplacian matrix** `L`:
   - `L = D - A`
   - `D`: Degree matrix (sum of conductances at each node)
   - `A`: Adjacency matrix (using conductance values)
4. Use the **Moore-Penrose pseudoinverse** of `L` (denoted `L⁺`) to compute:
   ```math
   R_eq(a, b) = L⁺[a,a] + L⁺[b,b] - 2 * L⁺[a,b]
