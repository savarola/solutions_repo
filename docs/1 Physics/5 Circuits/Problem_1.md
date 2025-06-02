# Problem 1
# ⚡ Circuits Problem 1: Equivalent Resistance Using Graph Theory

## 🎯 Problem Statement

We are given a complex electrical circuit represented as a graph, where multiple resistors span between two designated nodes: **START** and **END**.

This circuit may contain arbitrarily nested series and parallel resistor configurations.

**Goal**: Simplify the circuit step by step and compute the **total equivalent resistance** $R_{\text{eq}}$ between the START and END nodes.

---

## 🧠 Conceptual Overview

### Graph Representation of a Circuit:

- **Nodes**: represent electrical junctions.
- **Edges**: represent resistors.
- **Weights on Edges**: resistance values in ohms ($\Omega$).

By reducing the graph iteratively, we aim to collapse all intermediate connections and leave a single resistor between START and END with resistance $R_{\text{eq}}$.

---

## 🔄 Algorithm Description

The circuit is simplified using an iterative algorithm based on identifying **series** and **parallel** resistor combinations.

### 🔹 Step 1: Detect Series Connections

- A node with **degree 2** (connected to exactly two other nodes) and **not** being START or END is a candidate for a series reduction.
- The two resistors connected to this node are in series:
  $$R_{\text{eq}} = R_1 + R_2$$
- The node is removed, and the two edges are replaced by a single edge with the equivalent resistance.

### 🔹 Step 2: Detect Parallel Connections

- If there are **multiple edges between the same pair of nodes**, these edges represent resistors in parallel.
- The equivalent resistance is calculated as:
  $$R_{\text{eq}} = \left( \sum_{i=1}^{n} \frac{1}{R_i} \right)^{-1}$$
- These parallel edges are removed and replaced by a single edge with the equivalent resistance.

### 🔁 Step 3: Repeat Until Simplified

- The process is repeated:
  - Detect and reduce series connections.
  - Detect and reduce parallel connections.
- Continue until only a single edge remains between START and END.

---

## 🔄 Handling Nested Combinations

This algorithm is recursive or iterative in nature:
- Each iteration simplifies the current layer of the graph.
- As the graph is reduced, deeper layers (nested series/parallel combinations) become exposed and simplified in subsequent steps.
- This approach handles **arbitrary complexity** through repeated simplification passes.

---

## 🧪 Example Cases

### Example 1: Simple Series

START --[ $R_1 = 2\Omega$ ]-- A --[ $R_2 = 3\Omega$ ]-- END

- Series reduction:
  $$R_{\text{eq}} = R_1 + R_2 = 5\Omega$$

---

### Example 2: Simple Parallel

START --[ $R_1 = 6\Omega$ ]-- END  
START --[ $R_2 = 3\Omega$ ]-- END

- Parallel reduction:
  $$R_{\text{eq}} = \left( \frac{1}{6} + \frac{1}{3} \right)^{-1} = 2\Omega$$

---

### Example 3: Nested Series and Parallel

START --[ $R_1 = 2\Omega$ ]-- A --[ $R_2 = 4\Omega$ ]-- B --[ $R_3 = 2\Omega$ ]-- END  
Also, A and B are connected via $R_4 = 4\Omega$ (in parallel with $R_2$)

1. First reduce the parallel connection between A and B:
   $$R_{AB} = \left( \frac{1}{4} + \frac{1}{4} \right)^{-1} = 2\Omega$$

2. Now, combine in series:
   $$R_{\text{eq}} = R_1 + R_{AB} + R_3 = 2 + 2 + 2 = 6\Omega$$

---

## 🖼️ Visualization as a GIF or Sequence

To create an animated or step-by-step visualization:

1. **Frame 1**: Full resistor network as a graph.
2. **Frame 2**: Highlight and collapse a series connection.
3. **Frame 3**: Highlight and collapse a parallel connection.
4. **Repeat**: Continue until only a single resistor remains between START and END.
5. **Final Frame**: Display $R_{\text{eq}}$

This sequence can be turned into a visual animation using a graph visualization library or diagramming tool.

---

## 📈 Efficiency and Extensions

### Time Complexity (Conceptual):
- **Best case**: $O(n)$ (linear chain)
- **Average/Worst case**: $O(n^2)$ or more, depending on connectivity and cycles

### Possible Improvements:
- Detecting patterns using depth-first search (DFS)
- Using union-find data structures to track connected components
- Implementing advanced transformations (e.g., Y-Δ transforms)

---

## ✅ Conclusion

By modeling a circuit as a graph and applying a reduction algorithm that detects series and parallel resistors, we can efficiently compute equivalent resistance—even in highly complex networks.

This approach demonstrates the powerful synergy between electrical engineering and graph theory, enabling automation, scalability, and deeper insights into circuit behavior.

