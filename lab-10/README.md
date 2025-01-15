# Lab 10: Network Flow Algorithms

## Overview
This lab introduces network flow algorithms, focusing on problems involving maximum flow, minimum cut, and their applications. You will explore the fundamentals of flow networks, residual graphs, and augmenting paths, and implement classical algorithms such as Ford-Fulkerson and Edmonds-Karp.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the concepts of flow networks, residual graphs, and augmenting paths.
2. Implement the Ford-Fulkerson and Edmonds-Karp algorithms for solving the maximum flow problem.
3. Apply network flow concepts to real-world problems such as bipartite matching and circulation.
4. Analyze the time complexity of network flow algorithms.

---

## Lab Outline

### 1. **Introduction to Network Flow**
- **Flow Network**: A directed graph where each edge has a capacity, and each flow must respect capacity constraints.
- **Residual Graph**: Tracks the remaining capacities after a flow is sent.
- **Augmenting Path**: A path from the source to the sink that can accommodate more flow.

### 2. **Key Algorithms**
- **Ford-Fulkerson Method**: Uses augmenting paths to increase flow iteratively.
- **Edmonds-Karp Algorithm**: An implementation of Ford-Fulkerson using BFS to find augmenting paths (ensures polynomial time).

---

## Tasks

### Task 1: Maximum Flow using Ford-Fulkerson
Find the maximum flow in a given flow network using the Ford-Fulkerson algorithm.

#### Problem
Input: A flow network represented as an adjacency matrix or list, with capacities for each edge.  
Output: The maximum flow from source `s` to sink `t`.

#### Implementation
```python
from collections import defaultdict

class Graph:
    def __init__(self, vertices):
        self.graph = defaultdict(list)
        self.capacity = {}
        self.V = vertices

    def add_edge(self, u, v, cap):
        self.graph[u].append(v)
        self.graph[v].append(u)
        self.capacity[(u, v)] = cap
        self.capacity[(v, u)] = 0  # Reverse edge has 0 capacity initially

    def bfs(self, s, t, parent):
        visited = [False] * self.V
        queue = [s]
        visited[s] = True

        while queue:
            u = queue.pop(0)
            for v in self.graph[u]:
                if not visited[v] and self.capacity[(u, v)] > 0:
                    queue.append(v)
                    visited[v] = True
                    parent[v] = u
                    if v == t:
                        return True
        return False

    def ford_fulkerson(self, source, sink):
        parent = [-1] * self.V
        max_flow = 0

        while self.bfs(source, sink, parent):
            path_flow = float('Inf')
            v = sink
            while v != source:
                u = parent[v]
                path_flow = min(path_flow, self.capacity[(u, v)])
                v = parent[v]

            v = sink
            while v != source:
                u = parent[v]
                self.capacity[(u, v)] -= path_flow
                self.capacity[(v, u)] += path_flow
                v = parent[v]

            max_flow += path_flow

        return max_flow
```

---

### Task 2: Maximum Flow using Edmonds-Karp
Solve the maximum flow problem using the Edmonds-Karp algorithm (BFS-based Ford-Fulkerson).

#### Implementation
Modify the BFS implementation in the Ford-Fulkerson method to use a queue-based approach. Ensure that BFS finds the shortest augmenting path.

---

### Task 3: Bipartite Graph Matching
Use network flow to find the maximum bipartite matching in a given bipartite graph.

#### Problem
Input: A bipartite graph where vertices are divided into two disjoint sets.  
Output: The maximum number of matching pairs.

#### Implementation Hint
Transform the bipartite graph into a flow network:
1. Add a source node connected to all vertices in set `A` with capacity 1.
2. Add a sink node connected to all vertices in set `B` with capacity 1.
3. Add edges between `A` and `B` as per the bipartite graph structure with capacity 1.

---

### Task 4: Minimum Cut in a Flow Network
Find the edges that form the minimum cut in a flow network after computing the maximum flow.

#### Problem
Output: The set of edges whose removal disconnects the source from the sink.

#### Implementation Hint
Use the residual graph after finding the maximum flow to identify reachable and non-reachable nodes from the source.

---

### Bonus Task: Circulation Problem
Determine whether a circulation with demands exists in a network.

#### Problem
Input: A graph with edge capacities and vertex demands.  
Output: Whether a feasible circulation exists.

#### Implementation Hint
Add a super-source and super-sink, and transform the problem into a maximum flow problem.

---

## Code Template
```python
# Create a flow network
g = Graph(6)  # Example: 6 vertices
g.add_edge(0, 1, 16)
g.add_edge(0, 2, 13)
g.add_edge(1, 2, 10)
g.add_edge(1, 3, 12)
g.add_edge(2, 4, 14)
g.add_edge(3, 2, 9)
g.add_edge(3, 5, 20)
g.add_edge(4, 3, 7)
g.add_edge(4, 5, 4)

source, sink = 0, 5
print(f"Maximum Flow: {g.ford_fulkerson(source, sink)}")
```

---

## Submission Instructions
1. Save your solutions in a file named `network_flow_algorithms.py`.
2. Ensure the file is well-commented and includes explanations for your code.
3. Submit your work via Canvas by the deadline.

---

## Additional Resources
- [Ford-Fulkerson Algorithm Explanation](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/)
- [Edmonds-Karp Algorithm](https://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm)
- [Bipartite Matching with Network Flow](https://www.topcoder.com/community/competitive-programming/tutorials/maximum-bipartite-matching/)