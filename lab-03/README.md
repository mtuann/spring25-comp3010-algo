
# Lab 03: Graph Traversals

## Overview
In **Lab 03: Graph Traversals**, you will explore how to navigate graphs using fundamental traversal techniques: **Breadth-First Search (BFS)** and **Depth-First Search (DFS)**. You will implement these algorithms, analyze their behavior, and apply them to solve practical problems.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the structure of graphs (directed, undirected, weighted, unweighted).
2. Learn and implement **Breadth-First Search (BFS)**.
3. Learn and implement **Depth-First Search (DFS)** (recursive and iterative).
4. Compare BFS and DFS in terms of functionality and performance.
5. Apply graph traversals to solve real-world problems (e.g., shortest path, connected components).

---

## Lab Outline

### 1. **Introduction to Graphs**
   - Types of graphs: Directed, undirected, weighted, unweighted.
   - Representations of graphs:
     - Adjacency List.
     - Adjacency Matrix.
   - Key terminology: Vertices, edges, paths, cycles, connected components.

### 2. **Breadth-First Search (BFS)**
   - Algorithm overview:
     - Traverses level by level.
     - Utilizes a **queue** for exploration.
   - Common applications:
     - Finding the shortest path in an unweighted graph.
     - Checking bipartite graphs.

### 3. **Depth-First Search (DFS)**
   - Algorithm overview:
     - Explores as far as possible along each branch before backtracking.
     - Can be implemented recursively or using a **stack**.
   - Common applications:
     - Detecting cycles.
     - Finding connected components.

---

## Getting Started

### Prerequisites
- Ensure Python (>= 3.8) is installed.
- Install `matplotlib` and `networkx` for graph visualization:
  ```bash
  pip install matplotlib networkx
  ```

### Files Provided
1. `graph_traversals.py` - A template file for implementing graph traversal algorithms.
2. `sample_graph.json` - Example input graph in JSON format.
3. `README.md` - This instruction file.

---

## Tasks

### Task 1: Graph Representation
1. Open `graph_traversals.py`.
2. Implement a `Graph` class with:
   - `add_vertex(vertex)`: Adds a vertex to the graph.
   - `add_edge(v1, v2, weight=1)`: Adds an edge between `v1` and `v2`. If the graph is undirected, ensure symmetry.
   - `display()`: Prints or visualizes the graph using `networkx`.

   Example:
   ```python
   g = Graph()
   g.add_vertex('A')
   g.add_vertex('B')
   g.add_edge('A', 'B')
   g.display()
   ```

---

### Task 2: Implement BFS
1. Implement the `bfs(start_vertex)` method in the `Graph` class:
   - Input: Starting vertex.
   - Output: List of vertices in the order they are visited.

   Example:
   ```python
   g.bfs('A')
   ```

2. Analyze its time complexity for adjacency list and adjacency matrix representations.

---

### Task 3: Implement DFS
1. Implement the `dfs_recursive(start_vertex, visited=None)` method:
   - Input: Starting vertex.
   - Output: List of vertices in the order they are visited.
   
2. Implement the `dfs_iterative(start_vertex)` method:
   - Input: Starting vertex.
   - Output: List of vertices in the order they are visited.

3. Compare the recursive and iterative approaches.

---

### Task 4: Application of Graph Traversals
#### 4.1: Connected Components
1. Write a function `find_connected_components()` to identify all connected components in an undirected graph.
2. Test with a graph containing multiple disconnected subgraphs.

#### 4.2: Shortest Path (Unweighted)
1. Use BFS to implement `shortest_path(start_vertex, end_vertex)` to find the shortest path between two vertices.
2. Output:
   - The shortest path as a list of vertices.
   - The path length.

#### 4.3: Cycle Detection
1. Use DFS to implement `has_cycle()` to detect cycles in a graph.

---

## Bonus Task: Graph Visualization
1. Use `networkx` and `matplotlib` to visualize graphs.
   - Highlight BFS and DFS traversals on the graph.
2. Example visualization:
   - Nodes visited during BFS/DFS in a different color.

   Example code:
   ```python
   import networkx as nx
   import matplotlib.pyplot as plt

   def visualize_graph(graph, traversal=None):
       G = nx.Graph()
       for vertex, neighbors in graph.items():
           for neighbor in neighbors:
               G.add_edge(vertex, neighbor)

       pos = nx.spring_layout(G)
       nx.draw(G, pos, with_labels=True, node_color='lightblue')
       if traversal:
           nx.draw_networkx_nodes(G, pos, nodelist=traversal, node_color='orange')
       plt.show()
   ```

---

## Sample Input Graph
`sample_graph.json`:
```json
{
  "A": ["B", "C"],
  "B": ["A", "D", "E"],
  "C": ["A", "F"],
  "D": ["B"],
  "E": ["B", "F"],
  "F": ["C", "E"]
}
```

---

## Submission Instructions
1. Save your implementation in `graph_traversals.py`.
2. Include results (e.g., connected components, shortest paths) in a file named `results.txt`.
3. Attach visualizations (if any) as a PDF or image files.
4. Submit all files on Canvas by the deadline.

---

## Additional Resources
- [Graph Basics](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics))
- Python `networkx` library: [https://networkx.org/](https://networkx.org/)
- Graph traversal algorithms: [https://www.geeksforgeeks.org/](https://www.geeksforgeeks.org/)

---

## Notes
- Test all functions with different types of graphs (directed, undirected, cyclic, acyclic).
- Add comments in your code explaining the logic and complexity.
- Contact the TA or instructor if you need assistance.