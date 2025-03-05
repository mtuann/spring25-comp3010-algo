# Graph Theory: Basic Definitions, Connectivity, and Traversal

## Overview
This module explores **Graph Theory** concepts and their applications in **Algorithm Design**. You will learn how to represent graphs, traverse them efficiently, test for bipartiteness, and compute topological ordering in Directed Acyclic Graphs (DAGs).

## Topics Covered

### 1. **Basic Definitions and Applications**
- **Graph Representation**:
  - **Adjacency List** (Efficient for sparse graphs).
  - **Adjacency Matrix** (Fast edge lookup for dense graphs).
  
- **Types of Graphs**:
  - **Undirected vs. Directed Graphs**.
  - **Weighted vs. Unweighted Graphs**.
  - **DAGs (Directed Acyclic Graphs)**.

- **Applications**:
  - **Social networks** (Facebook friends graph).
  - **Road navigation** (Google Maps shortest path).
  - **Scheduling tasks** (DAGs with dependencies).

---

### 2. **Graph Connectivity and Traversal**
Graph traversal helps in exploring all nodes of a graph. Two key techniques are **Depth-First Search (DFS)** and **Breadth-First Search (BFS)**.

#### **Depth-First Search (DFS)**
- Explores as deep as possible before backtracking.
- Uses **recursion** (or an explicit **stack** for iterative implementation).

**Pseudocode for DFS (Recursive)**:
```
DFS(graph, node, visited):
    visited[node] = True
    for neighbor in graph[node]:
        if not visited[neighbor]:
            DFS(graph, neighbor, visited)
```

**Pseudocode for DFS (Iterative using Stack)**:
```
DFS(graph, start):
    stack = [start]
    visited = set()
    
    while stack is not empty:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            for neighbor in graph[node]:
                stack.push(neighbor)
```

📌 **Use cases**: Cycle detection, connectivity check, topological sorting.

---

#### **Breadth-First Search (BFS)**
- Explores all neighbors first before moving deeper.
- Uses a **queue** (FIFO order).

**Pseudocode for BFS**:
```
BFS(graph, start):
    queue = [start]
    visited = set([start])

    while queue is not empty:
        node = queue.pop(0)
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

📌 **Use cases**: Finding the shortest path in **unweighted** graphs.

---

### 3. **Testing Bipartiteness**
A graph is **bipartite** if it can be colored using **two colors** such that no two adjacent nodes have the same color.

#### **Algorithm (BFS-based Two-Coloring)**
1. Assign one node **color 1**.
2. Assign its neighbors **color 2**.
3. Continue BFS. If a node encounters a neighbor of the same color, the graph is **not bipartite**.

**Pseudocode**:
```
CheckBipartite(graph, n):
    colors = [-1] * n  # -1: Unvisited, 0: First color, 1: Second color
    
    for node in range(n):  # Ensure all components are checked
        if colors[node] == -1:
            queue = [node]
            colors[node] = 0
            
            while queue:
                u = queue.pop(0)
                for v in graph[u]:
                    if colors[v] == -1:  # If unvisited, assign opposite color
                        colors[v] = 1 - colors[u]
                        queue.append(v)
                    elif colors[v] == colors[u]:  # Conflict found
                        return False
    return True
```
📌 **Use case**: **Matching problems** (e.g., job assignments, team formation).

---

### 4. **DAGs and Topological Ordering**
A **DAG** is a **Directed Acyclic Graph**. It allows **topological sorting**, where nodes appear **before** their dependencies.

#### **Algorithm 1: Kahn’s Algorithm (BFS-based)**
1. Compute **in-degrees** of all nodes.
2. Start with **zero in-degree nodes**.
3. Remove nodes one by one, updating in-degrees.

**Pseudocode**:
```
TopologicalSort(graph, n):
    in_degree = [0] * n
    for u in graph:
        for v in graph[u]:
            in_degree[v] += 1

    queue = [node for node in range(n) if in_degree[node] == 0]
    topo_order = []

    while queue:
        node = queue.pop(0)
        topo_order.append(node)
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
                
    if len(topo_order) == n:
        return topo_order  # Valid order
    else:
        return "Cycle detected, no valid topological ordering"
```

📌 **Use cases**: **Task Scheduling**, **Compiling Dependencies**.

---

## **Learning Outcomes**
By the end of this module, you should be able to:
✔ Implement **DFS and BFS** for **graph traversal**.  
✔ Check whether a graph is **bipartite** using **two-coloring**.  
✔ Construct a **topological order** for a **DAG** and apply it to real-world problems.  

---

## **Resources**
- 📖 **CLRS - Introduction to Algorithms** (Graph Algorithms).
- 📖 **Competitive Programming Handbook** (Graph Traversal).
- 🔗 **LeetCode Graph Problems**: [LeetCode](https://leetcode.com/tag/graph/)
- 🔗 **Codeforces Graph Section**: [Codeforces](https://codeforces.com/blog/entry/55219)

---

## **Exercises**
1. **Implement DFS and BFS** for a given **undirected graph**.
2. **Check if a given graph is bipartite**.
3. **Find the topological order** of a DAG using **both DFS and Kahn’s algorithm**.
4. **Solve a scheduling problem** using **topological sorting**.

🚀 **Happy Coding!**


