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

![1](https://github.com/user-attachments/assets/095641be-3a61-4f93-a552-4db3664c0961)
![2](https://github.com/user-attachments/assets/0703578e-f61d-41db-8d19-1e1f6ddbf887)
![3](https://github.com/user-attachments/assets/ad5a9ea3-770f-4cb6-880d-d73620ba3c36)
![4](https://github.com/user-attachments/assets/883d098b-1591-4de2-82ea-fd0c0ce20e0a)
![5](https://github.com/user-attachments/assets/ab6b242e-ff2d-4a41-ae87-6688695b4297)

```python
import networkx as nx
import matplotlib.pyplot as plt

def draw_graph(G, step_title):
    pos = nx.spring_layout(G, seed=42)
    plt.figure(figsize=(6, 4))
    edge_labels = {}
    for u, v, data in G.edges(data=True):
        label = f"{data['resistance']}Ω"
        if G.number_of_edges(u, v) > 1:
            label = ', '.join(f"{d['resistance']}Ω" for d in G.get_edge_data(u, v).values())
        edge_labels[(u, v)] = label

    nx.draw(
        G, pos,
        with_labels=True,
        node_color='tomato',
        node_size=800,
        edge_color='darkgreen',
        width=2,
        font_weight='bold',
        font_color='black'
    )

    nx.draw_networkx_edge_labels(
        G, pos,
        edge_labels=edge_labels,
        font_color='navy',
        font_size=9
    )

    plt.title(step_title)
    plt.axis('off')
    plt.show()

def combine_series(G):
    changed = True
    while changed:
        changed = False
        for node in list(G.nodes):
            if G.degree(node) == 2 and node not in ("B+", "B-"):
                neighbors = list(G.neighbors(node))
                if len(neighbors) == 2:
                    u, v = neighbors
                    edge1 = next(iter(G.get_edge_data(u, node).values()))
                    edge2 = next(iter(G.get_edge_data(node, v).values()))
                    R_new = edge1['resistance'] + edge2['resistance']
                    G.remove_node(node)
                    G.add_edge(u, v, resistance=R_new)
                    changed = True
                    draw_graph(G, f"{u} - {v} (series): {R_new}Ω")
                    break

def combine_parallel(G):
    to_process = list(G.edges(keys=True))
    seen = set()
    for u, v, k in to_process:
        if (u, v) in seen or (v, u) in seen:
            continue
        if G.number_of_edges(u, v) > 1:
            resistances = [d['resistance'] for d in G.get_edge_data(u, v).values()]
            R_parallel = 1 / sum(1/r for r in resistances)
            G.remove_edges_from([(u, v, key) for key in G.get_edge_data(u, v).keys()])
            G.add_edge(u, v, resistance=R_parallel)
            draw_graph(G, f"{u} - {v} (parallel): {R_parallel:.2f}Ω")
        seen.add((u, v))

def reduce_graph(G):
    draw_graph(G, "Initial Graph")
    while True:
        nodes_before = len(G.nodes)
        combine_series(G)
        combine_parallel(G)
        if len(G.nodes) == nodes_before:
            break
    return G

def get_equivalent_resistance(G, source, target):
    if G.has_edge(source, target):
        return next(iter(G.get_edge_data(source, target).values()))['resistance']
    else:
        return None

def example_case_1():
    G = nx.MultiGraph()
    G.add_nodes_from(["B+", "B-", "A", "B", "C"])
    G.add_edge("B+", "A", resistance=2)  # R2
    G.add_edge("A", "B", resistance=3)   # R3
    G.add_edge("B+", "B", resistance=5)  # R1
    G.add_edge("B", "C", resistance=4)   # R4
    G.add_edge("C", "B-", resistance=6)  # R5

    reduce_graph(G)
    Req = get_equivalent_resistance(G, "B+", "B-")
    print(f"Equivalent Resistance (Case 1): {Req:.2f} Ohms")

example_case_1()
```

Equivalent Resistance (Case 1): 12.50 Ohms

![1](https://github.com/user-attachments/assets/dcbfe595-81c4-4230-99e6-12b4b3307deb)
![2](https://github.com/user-attachments/assets/eb207813-05e4-4f45-82fc-a1971017d9e2)
![3](https://github.com/user-attachments/assets/78b6d09b-5ac8-45e6-83ed-02bb1e2d2aef)
![4](https://github.com/user-attachments/assets/4974d1f1-61fc-4aff-acab-af38297768b3)
![5](https://github.com/user-attachments/assets/53fcde8d-25ee-40c5-b855-a2bb75a73348)
![6](https://github.com/user-attachments/assets/dccd0e81-76e3-45a8-a068-a1198cd6ee75)
![7](https://github.com/user-attachments/assets/56324e2d-b844-4978-bdc8-3ec7da70c18a)
![8](https://github.com/user-attachments/assets/3059a2d7-bfd9-453e-8787-e951f962a07e)

```python
import networkx as nx
import matplotlib.pyplot as plt

# Koordinatlar
pos_case2 = {
    "B+": (0, 1),
    "A": (1, 1),
    "X1": (2, 2),
    "X2": (3, 2),
    "Y1": (2, 0),
    "Y2": (3, 0),
    "B": (4, 1),
    "B-": (5, 1)
}

def draw_case2(G, title):
    plt.figure(figsize=(8, 4))
    edge_labels = nx.get_edge_attributes(G, 'resistance')

    nx.draw(
        G, pos=pos_case2,
        with_labels=True,
        node_size=800,
        node_color='orange',
        edge_color='teal',
        font_weight='bold',
        font_color='black',
        width=2
    )

    nx.draw_networkx_edge_labels(
        G, pos=pos_case2,
        edge_labels=edge_labels,
        font_color='darkred'
    )

    plt.title(title, color='navy')
    plt.axis('off')
    plt.show()

def combine_series_case2(G):
    changed = True
    while changed:
        changed = False
        for node in list(G.nodes):
            if node not in ("B+", "B-") and G.degree(node) == 2:
                u, v = list(G.neighbors(node))
                r1 = G.get_edge_data(u, node)[0]['resistance']
                r2 = G.get_edge_data(node, v)[0]['resistance']
                G.remove_node(node)
                G.add_edge(u, v, resistance=r1 + r2)
                draw_case2(G, f"Series combined: {u}-{v} = {r1}+{r2} Ω")
                changed = True
                break

def combine_parallel_case2(G):
    for u, v in list(G.edges()):
        if G.number_of_edges(u, v) > 1:
            resistances = [edata['resistance'] for k, edata in G[u][v].items()]
            R_parallel = 1 / sum(1/r for r in resistances)
            G.remove_edges_from([(u, v, k) for k in G[u][v]])
            G.add_edge(u, v, resistance=R_parallel)
            draw_case2(G, f"Parallel combined: {u}-{v} = {R_parallel:.2f} Ω")

def reduce_graph_case2(G):
    draw_case2(G, "Initial Circuit (Case 2)")
    while True:
        before = len(G.edges)
        combine_series_case2(G)
        combine_parallel_case2(G)
        if len(G.edges) == before:
            break

def get_equivalent_resistance(G, source, target):
    return list(G.get_edge_data(source, target).values())[0]['resistance']

def example_case_2():
    G = nx.MultiGraph()

    G.add_nodes_from(["B+", "A", "X1", "X2", "Y1", "Y2", "B", "B-"])

    G.add_edge("A", "X1", resistance=2)   # R2
    G.add_edge("X1", "X2", resistance=4)  # R4
    G.add_edge("X2", "B", resistance=0)   # bağ

    G.add_edge("A", "Y1", resistance=3)   # R3
    G.add_edge("Y1", "Y2", resistance=6)  # R5
    G.add_edge("Y2", "B", resistance=0)   # bağ

    G.add_edge("B+", "A", resistance=1)   # R1
    G.add_edge("B", "B-", resistance=2)   # R6

    reduce_graph_case2(G)
    Req = get_equivalent_resistance(G, "B+", "B-")
    print(f"Equivalent Resistance (Case 2): {Req:.2f} Ω")

example_case_2()
```

Equivalent Resistance (Case 2): 6.60 Ω

![download](https://github.com/user-attachments/assets/80058279-0536-4db8-a69c-6080b4032e91)

```python
import matplotlib.pyplot as plt
import networkx as nx

def draw_parallel_and_series():
    fig, axs = plt.subplots(2, 2, figsize=(14, 10))
    fig.suptitle("Building Blocks: Parallel and Series Configuration", fontsize=16)

    # --- PARALLEL CONFIGURATION ---
    # Before
    G1 = nx.DiGraph()
    G1.add_edges_from([("I1", "o1"), ("In", "o1"),
                       ("o1", "p1"), ("o1", "p2"),
                       ("p1", "o3"), ("p2", "o3"),
                       ("o3", "D1"), ("o3", "D4")])
    pos1 = {
        "I1": (0, 2), "In": (0, 0), "o1": (1, 1),
        "p1": (2, 2), "p2": (2, 0), "o3": (3, 1),
        "D1": (4, 2), "D4": (4, 0)
    }
    nx.draw(G1, pos1, ax=axs[0, 0], with_labels=True,
            node_color='skyblue', edge_color='dimgray', node_size=800)
    nx.draw_networkx_edge_labels(G1, pos1, ax=axs[0, 0], edge_labels={
        ("o1", "p1"): "R1", ("o1", "p2"): "R2"
    }, font_color='navy')
    axs[0, 0].set_title("Before (Parallel)")
    axs[0, 0].axis('off')

    # After
    G2 = nx.DiGraph()
    G2.add_edges_from([("I1", "o1"), ("In", "o1"),
                       ("o1", "o3"), ("o3", "D1"), ("o3", "Dm")])
    pos2 = {
        "I1": (0, 2), "In": (0, 0), "o1": (1, 1),
        "o3": (2, 1), "D1": (3, 2), "Dm": (3, 0)
    }
    nx.draw(G2, pos2, ax=axs[0, 1], with_labels=True,
            node_color='mediumorchid', edge_color='dimgray', node_size=800)
    nx.draw_networkx_edge_labels(G2, pos2, ax=axs[0, 1], edge_labels={
        ("o1", "o3"): "R12"
    }, font_color='navy')
    axs[0, 1].set_title("After (1/R1 + 1/R2 = 1/R12)")
    axs[0, 1].axis('off')

    # --- SERIES CONFIGURATION ---
    # Before
    G3 = nx.DiGraph()
    G3.add_edges_from([("I1", "o1"), ("In", "o1"),
                       ("o1", "o2"), ("o2", "o3"),
                       ("o3", "D1"), ("o3", "D4")])
    pos3 = {
        "I1": (0, 2), "In": (0, 0), "o1": (1, 1),
        "o2": (2, 1), "o3": (3, 1), "D1": (4, 2), "D4": (4, 0)
    }
    node_colors_series = ['skyblue'] * 7
    node_colors_series[3] = 'orchid'  # o2
    nx.draw(G3, pos3, ax=axs[1, 0], with_labels=True,
            node_color=node_colors_series, edge_color='dimgray', node_size=800)
    nx.draw_networkx_edge_labels(G3, pos3, ax=axs[1, 0], edge_labels={
        ("o1", "o2"): "R1", ("o2", "o3"): "R2"
    }, font_color='navy')
    axs[1, 0].set_title("Before (Series)")
    axs[1, 0].axis('off')

    # After
    G4 = nx.DiGraph()
    G4.add_edges_from([("I1", "o1"), ("In", "o1"),
                       ("o1", "o3"), ("o3", "D1"), ("o3", "Dm")])
    pos4 = {
        "I1": (0, 2), "In": (0, 0), "o1": (1, 1),
        "o3": (2, 1), "D1": (3, 2), "Dm": (3, 0)
    }
    nx.draw(G4, pos4, ax=axs[1, 1], with_labels=True,
            node_color='skyblue', edge_color='dimgray', node_size=800)
    nx.draw_networkx_edge_labels(G4, pos4, ax=axs[1, 1], edge_labels={
        ("o1", "o3"): "R12"
    }, font_color='navy')
    axs[1, 1].set_title("After (R12 = R1 + R2)")
    axs[1, 1].axis('off')

    plt.tight_layout(rect=[0, 0.03, 1, 0.95])
    plt.show()

draw_parallel_and_series()
```

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

