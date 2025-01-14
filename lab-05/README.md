# Lab 05: Minimum Spanning Tree (MST)

## Overview
In this lab, you will explore **Minimum Spanning Trees (MST)**, an essential concept in graph theory. A spanning tree connects all the vertices in a graph with the minimum total edge weight. You will learn two classical algorithms for finding MSTs: **Kruskal's Algorithm** and **Prim's Algorithm**.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the concept of a **Minimum Spanning Tree**.
2. Implement **Kruskal's Algorithm** using a Disjoint Set (Union-Find) data structure.
3. Implement **Prim's Algorithm** using a priority queue (min-heap).
4. Compare and analyze the performance of these algorithms.

---

## Lab Outline

### 1. **Introduction to MST**
- A **spanning tree** is a subset of the edges in a graph that forms a tree, connecting all vertices with no cycles.
- A **minimum spanning tree** is a spanning tree with the smallest total edge weight.

**Applications of MST**:
- Network design (telecommunications, roads, electrical grids).
- Approximation algorithms for NP-hard problems (e.g., Traveling Salesman Problem).
- Cluster analysis.

### 2. **Algorithms for MST**
- **Kruskal's Algorithm**:
  - Greedily adds edges to the MST in increasing order of weight while avoiding cycles.
  - Uses the **Disjoint Set Union-Find** structure for cycle detection.
- **Prim's Algorithm**:
  - Starts from a vertex and grows the MST by adding the smallest edge connecting the MST to a new vertex.
  - Efficiently implemented using a **priority queue** (min-heap).

---

## Getting Started

### Prerequisites
- Familiarity with graphs (vertices, edges, weights, adjacency representation).
- Knowledge of sorting, priority queues, and basic data structures (e.g., lists, sets).

### Files Provided
1. `mst_algorithms.py` - A template for implementing MST algorithms.
2. `graph_input.txt` - A sample input file representing a graph.
3. `README.md` - This instruction file.

---

## Tasks

### Task 1: Implement Kruskal's Algorithm
1. Open `mst_algorithms.py`.
2. Define the function `kruskal_mst(graph)`.
3. Steps:
   - Sort all edges in ascending order by weight.
   - Use a **Disjoint Set Union-Find** structure to check for cycles.
   - Add edges to the MST until all vertices are connected.

4. Example Implementation:
   ```python
   def kruskal_mst(graph):
       # Initialize Union-Find structure
       # Sort edges by weight
       # Iteratively add edges, checking for cycles
       return mst, total_weight
   ```

5. Test with:
   ```python
   graph = {
       'vertices': ['A', 'B', 'C', 'D'],
       'edges': [
           ('A', 'B', 1), ('B', 'C', 2), ('C', 'D', 3), ('A', 'D', 4)
       ]
   }
   mst, weight = kruskal_mst(graph)
   print("MST:", mst, "Total Weight:", weight)
   ```

---

### Task 2: Implement Prim's Algorithm
1. Define the function `prim_mst(graph)`.
2. Steps:
   - Initialize a min-heap to select edges with the smallest weight.
   - Use a set to track visited vertices.
   - Expand the MST by adding the smallest edge from the heap.

3. Example Implementation:
   ```python
   def prim_mst(graph):
       # Initialize a priority queue
       # Add edges of the starting vertex to the queue
       # Iteratively add the smallest edge that connects to a new vertex
       return mst, total_weight
   ```

4. Test with:
   ```python
   graph = {
       'vertices': ['A', 'B', 'C', 'D'],
       'edges': [
           ('A', 'B', 1), ('B', 'C', 2), ('C', 'D', 3), ('A', 'D', 4)
       ]
   }
   mst, weight = prim_mst(graph)
   print("MST:", mst, "Total Weight:", weight)
   ```

---

### Task 3: Analyze and Compare Algorithms
1. Compare the time complexity:
   - **Kruskal's Algorithm**: $O(E \log E + E \cdot \alpha(V))$, where $\alpha(V)$ is the inverse Ackermann function (from Union-Find).
   - **Prim's Algorithm**: $O(E + V \log V)$ with an adjacency list and a min-heap.
2. Discuss practical use cases for each algorithm:
   - Kruskal's is efficient for sparse graphs.
   - Prim's is efficient for dense graphs.

---

### Task 4: Bonus Task - Visualize the MST
1. Use the `networkx` library to visualize the MST.
2. Example:
   ```python
   import networkx as nx
   import matplotlib.pyplot as plt

   def visualize_mst(graph, mst):
       G = nx.Graph()
       for edge in graph['edges']:
           G.add_edge(edge[0], edge[1], weight=edge[2])
       mst_edges = [(u, v) for u, v, _ in mst]
       pos = nx.spring_layout(G)
       nx.draw(G, pos, with_labels=True)
       nx.draw_networkx_edges(G, pos, edgelist=mst_edges, edge_color='r', width=2)
       plt.show()
   ```

3. Call `visualize_mst(graph, mst)` after finding the MST.

---

## Submission Instructions
1. Save your implementation in `mst_algorithms.py`.
2. Include your analysis in `analysis.txt`.
3. Attach screenshots or plots of the MST visualization.
4. Submit all files on Canvas by the deadline.

---

## Additional Resources
- [Kruskal's Algorithm on GeeksforGeeks](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm/)
- [Prim's Algorithm on GeeksforGeeks](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/)
- [NetworkX Documentation](https://networkx.org/documentation/stable/index.html)

---

## Notes
- Test your code with both connected and disconnected graphs.
- Handle edge cases (e.g., graphs with multiple edges of the same weight).
- Include comments explaining your implementation logic and time complexity.