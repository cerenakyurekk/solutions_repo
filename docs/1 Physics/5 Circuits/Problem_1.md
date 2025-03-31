# Problem 1
# Equivalent Resistance Using Graph Theory

## Motivation:
Calculating equivalent resistance is a fundamental problem in electrical circuits, essential for understanding and designing efficient systems. While traditional methods involve iteratively applying series and parallel resistor rules, these approaches can become cumbersome for complex circuits with many components. Graph theory offers a powerful alternative, providing a structured and algorithmic way to analyze circuits.

By representing a circuit as a graph—where nodes correspond to junctions and edges represent resistors with weights equal to their resistance values—we can systematically simplify even the most intricate networks. This method not only streamlines calculations but also opens the door to automated analysis, making it particularly useful in modern applications like circuit simulation software, optimization problems, and network design.

Studying equivalent resistance through graph theory is valuable not only for its practical applications but also for the deeper insights it provides into the interplay between electrical and mathematical concepts. This approach highlights the versatility of graph theory, demonstrating its relevance across physics, engineering, and computer science.

## Task Options:
### Option 1: Simplified Task – Algorithm Description
Describe the algorithm for calculating the equivalent resistance using graph theory.

Provide the pseudocode that:
- Identifies series and parallel connections.
- Iteratively reduces the graph until a single equivalent resistance is obtained.
- Includes a clear explanation of how the algorithm handles nested combinations.

### Option 2: Advanced Task – Full Implementation
Implement the algorithm in a programming language of your choice.

Ensure the implementation:
- Accepts a circuit graph as input.
- Handles arbitrary resistor configurations, including nested series and parallel connections.
- Outputs the final equivalent resistance.
- Test your implementation with examples, such as:
  - Simple series and parallel combinations.
  - Nested configurations.
  - Complex graphs with multiple cycles.

#### Deliverables:
- A detailed pseudocode (but preferably a full implementation) and explanation of the algorithm.
- Description of how it handles complex circuit configurations on three input examples.
- A brief analysis of the algorithm's efficiency and potential improvements.

#### Hints and Resources:
- Focus on iterative graph simplification:
  - Detect linear chains for series reduction.
  - Identify cycles for parallel reduction.
- Use tools like networkx (Python) or similar for graph manipulation if you choose implementation.
- Depth-first search (DFS) or other traversal methods can help identify patterns in the graph.

---

## Algorithm Description

The basic idea is to represent the circuit as a graph, where:
- **Nodes (vertices)** represent the junctions or connection points.
- **Edges** represent resistors, with weights corresponding to their resistance values.

The algorithm will simplify the circuit graph step-by-step, reducing series and parallel resistor combinations to a single equivalent resistance. The reduction follows these rules:
- **Series combination**: If two resistors are in series (i.e., connected directly without any branching in between), the equivalent resistance is simply the sum of the two resistances.
  \[
  R_{\text{eq}} = R_1 + R_2
  \]
- **Parallel combination**: If two resistors are in parallel (i.e., both connected between the same two nodes), the equivalent resistance is given by:
  \[
  \frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2}
  \]

---

## Algorithm Steps:
1. **Input Representation**:
   - The circuit is represented as a graph \( G(V, E) \), where each edge \( (u, v) \) has a weight \( w(u, v) \) corresponding to the resistor’s resistance.
   
2. **Identify Series and Parallel Connections**:
   - **Series connection**: Two resistors are in series if they are connected end-to-end, with no other connections between them. This can be identified by checking nodes with only two connections (except for the start and end).
   - **Parallel connection**: Two resistors are in parallel if both resistors are connected between the same pair of nodes. This can be identified by checking pairs of resistors that share the same start and end nodes.
   
3. **Graph Simplification**:
   - **Series reduction**: If resistors are in series, replace them with a single resistor whose value is the sum of the two resistances. The corresponding graph edge between the two nodes will be updated with the new resistance.
   - **Parallel reduction**: If resistors are in parallel, replace them with a single resistor whose value is calculated by the parallel formula. The corresponding graph edge will be updated with the new equivalent resistance.

4. **Iterate**:
   - Continue reducing the graph by finding series and parallel combinations and replacing them with their equivalent resistances until only one edge (the equivalent resistance) remains in the graph.

5. **Handle Nested Combinations**:
   - As the graph simplifies, new series and parallel combinations may emerge. The algorithm should recursively or iteratively re-check the graph after each reduction.

---

## Pseudocode:

```python
def equivalent_resistance(circuit_graph):
    # Step 1: Initialize a graph G
    G = circuit_graph
    
    # Step 2: Detect series connections
    def reduce_series():
        for node in G:
            if G[node] has exactly two neighbors:
                # These two resistors are in series
                # Sum the resistances and replace the edge
                equivalent_resistance = sum_of_resistances
                G[node] = equivalent_resistance  # Update the edge
    
    # Step 3: Detect parallel connections
    def reduce_parallel():
        for edge in G.edges:
            u, v = edge
            if G[u] and G[v] are connected with multiple resistors:
                # These resistors are in parallel
                # Calculate the equivalent resistance using the parallel formula
                parallel_resistance = 1 / (1 / R1 + 1 / R2)
                G[u][v] = parallel_resistance  # Update the edge
    
    # Step 4: Simplify graph
    while len(G.edges) > 1:
        reduce_series()  # Reduce series connections
        reduce_parallel()  # Reduce parallel connections
    
    # Step 5: Return the final equivalent resistance
    return G[remaining_edge]  # The final resistance is in the last remaining edge

## Explanation of the Algorithm:

### Graph Representation:
We use an adjacency list or matrix to represent the graph. The nodes (junctions) are connected by edges, which have resistance values as weights.

### Series Reduction:
We look for pairs of resistors connected in series by checking if two resistors are connected directly with no branching in between.

### Parallel Reduction:
We check for pairs of resistors connected in parallel by checking if they are both connected between the same pair of nodes.

### Iterative Process:
After each reduction, the graph is updated, and the algorithm rechecks the graph for possible new reductions. This process continues until we are left with a single equivalent resistance.

---

## Handling Complex Circuits:
The algorithm simplifies the circuit step-by-step. In complex circuits, you will need to detect combinations that might not be immediately obvious. This requires a combination of **depth-first search (DFS)** or **breadth-first search (BFS)** to explore and detect these patterns.

---

## Efficiency and Improvements:

### Time Complexity:
The complexity mainly depends on the size of the graph and the number of iterations needed to reduce the circuit. For each iteration, we are checking all edges, leading to a time complexity of \( O(E) \), where \( E \) is the number of edges.

### Optimization:
We can optimize the algorithm by maintaining auxiliary data structures to track the current state of the graph and avoid redundant calculations.

### Cycle Detection:
For more advanced circuits with cycles, we can use graph traversal techniques to detect and reduce these cycles effectively.


### Graph Representation:

#### Nodes:
- 1, 2, 3, 4, 5, 6

#### Edges:
- (1, 2, \( R_1 = 6 \, \Omega \))
- (2, 3, \( R_2 = 3 \, \Omega \))
- (3, 4, \( R_3 = 4 \, \Omega \))
- (2, 5, \( R_4 = 5 \, \Omega \))
- (4, 6, \( R_5 = 2 \, \Omega \))


import networkx as nx
import matplotlib.pyplot as plt

# Function to plot the graph for visualization
def plot_graph(G, title="Circuit Graph"):
    pos = nx.spring_layout(G)  # Layout for better visualization
    plt.figure(figsize=(10, 8))
    node_size = [500 + 100 * G.degree(node) for node in G.nodes]
    node_color = ['lightgreen' if G.degree(node) == 1 else 'lightblue' for node in G.nodes]
    nx.draw(G, pos, with_labels=True, node_color=node_color, node_size=node_size, font_size=15, font_weight="bold", edge_color="gray")

    edge_labels = nx.get_edge_attributes(G, 'weight')
    nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels, font_size=12)

    plt.title(title)
    plt.axis('off')  # Hide axes for a cleaner presentation
    plt.show()

# Function to find series resistors
def find_series_resistors(G):
    series_pairs = []
    for node in G.nodes:
        neighbors = list(G.neighbors(node))

        if len(neighbors) == 2:  # Exactly two neighbors for series connection
            R1 = G[node][neighbors[0]]['weight']
            R2 = G[node][neighbors[1]]['weight']
            if R1 is not None and R2 is not None:
                series_pairs.append((node, neighbors[0], neighbors[1]))  # (center_node, neighbor1, neighbor2)
    return series_pairs

# Function to find parallel resistors
def find_parallel_resistors(G):
    parallel_pairs = []
    for node in G.nodes:
        neighbors = list(G.neighbors(node))

        if len(neighbors) == 2:  # Exactly two neighbors for parallel connection
            R1 = G[node][neighbors[0]]['weight']
            R2 = G[node][neighbors[1]]['weight']
            if R1 is not None and R2 is not None:
                parallel_pairs.append((neighbors[0], node, neighbors[1]))  # (node1, center_node, node2)
    return parallel_pairs

# Function to simplify a series resistor
def simplify_series(G, series_pair):
    node1, node2, node3 = series_pair
    R1 = G[node2][node1]['weight']
    R2 = G[node3][node2]['weight']
    R_eq = R1 + R2  # Series combination

    # Remove the two resistors and add the equivalent one
    G.remove_edge(node2, node1)
    G.remove_edge(node3, node2)
    G.add_edge(node1, node3, weight=R_eq)
    return G

# Function to simplify a parallel resistor
def simplify_parallel(G, parallel_pair):
    node1, node2, node3 = parallel_pair
    R1 = G[node1][node2]['weight']
    R2 = G[node2][node3]['weight']
    R_eq = 1 / (1 / R1 + 1 / R2)  # Parallel combination

    # Remove the two resistors and add the equivalent one
    G.remove_edge(node1, node2)
    G.remove_edge(node2, node3)
    G.add_edge(node1, node3, weight=R_eq)
    return G

# Main function to calculate equivalent resistance
def calculate_equivalent_resistance(G):
    # Initial graph plot
    plot_graph(G, title="Initial Circuit Graph")

    step = 1
    # Keep simplifying the graph until only one edge remains
    while len(G.edges) > 1:
        # Simplify series connections
        series_pairs = find_series_resistors(G)
        if series_pairs:
            print(f"Step {step}: Simplifying series pairs: {series_pairs}")
        for series_pair in series_pairs:
            G = simplify_series(G, series_pair)

        # Plot after simplifying series resistors
        plot_graph(G, title=f"After Step {step}: Simplified Series Resistors")

        # Simplify parallel connections
        parallel_pairs = find_parallel_resistors(G)
        if parallel_pairs:
            print(f"Step {step}: Simplifying parallel pairs: {parallel_pairs}")
        for parallel_pair in parallel_pairs:
            G = simplify_parallel(G, parallel_pair)

        # Plot after simplifying parallel resistors
        plot_graph(G, title=f"After Step {step}: Simplified Parallel Resistors")

        step += 1

    # The final equivalent resistance is the only edge left in the graph
    final_resistance = None
    for edge in G.edges(data=True):
        final_resistance = edge[2]['weight']

    return final_resistance

# Example usage: Create a circuit graph
G = nx.Graph()

# Adding resistors (edges) to the circuit
# Resistor values: R1 = 6 ohms, R2 = 3 ohms, R3 = 4 ohms, R4 = 5 ohms, R5 = 2 ohms
G.add_edge(1, 2, weight=6)  # R1
G.add_edge(2, 3, weight=3)  # R2
G.add_edge(3, 4, weight=4)  # R3
G.add_edge(2, 5, weight=5)  # R4
G.add_edge(4, 6, weight=2)  # R5

# Call the function to calculate the equivalent resistance
equivalent_resistance = calculate_equivalent_resistance(G)
print(f"The equivalent resistance of the circuit is: {equivalent_resistance:.2f} ohms")



```
![alt text](image7.png)
