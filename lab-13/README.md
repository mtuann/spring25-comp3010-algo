# Lab 13: Approximation and Local Search

## Overview
In this lab, we explore **approximation algorithms** and **local search techniques** for tackling computationally hard problems (NP-hard problems). These methods provide near-optimal solutions in reasonable time, even when finding exact solutions is computationally infeasible.

You will:
1. Learn the fundamentals of approximation algorithms.
2. Understand how local search works for optimization problems.
3. Implement practical algorithms to solve common NP-hard problems using approximation and local search techniques.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the principles of approximation algorithms and their use in solving NP-hard problems.
2. Learn about approximation ratios and analyze the performance of approximation algorithms.
3. Implement local search techniques for solving optimization problems.
4. Compare and analyze the trade-offs between approximation, local search, and exact algorithms.

---

## Lab Outline

### 1. **Introduction to Approximation Algorithms**
- **What are approximation algorithms?**
  - Algorithms that find solutions close to the optimal with a guaranteed performance bound.
- **Key Concepts:**
  - Approximation ratio.
  - Polynomial-time solvability.

### 2. **Local Search Techniques**
- **What is local search?**
  - An iterative optimization technique that explores neighboring solutions.
- **Applications:**
  - Suitable for combinatorial optimization problems like TSP, Vertex Cover, and Max-Cut.
- **Key Features:**
  - Starting from an initial solution.
  - Exploring neighborhoods and improving iteratively.

---

## Tasks

### Task 1: Approximation for Vertex Cover
#### Objective
Implement a **2-approximation algorithm** for the Vertex Cover problem.

#### Problem
Input: A graph $G(V, E)$.  
Output: A vertex cover $C$ such that $|C| \leq 2 \times |C^*|$, where $C^*$ is the optimal solution.

#### Algorithm
1. Initialize the vertex cover $C$ as an empty set.
2. While there are uncovered edges:
   - Pick an edge $(u, v)$ from $E$.
   - Add both $u$ and $v$ to $C$.
   - Remove all edges incident to $u$ and $v$.

#### Implementation
```python
def vertex_cover_approximation(graph):
    """
    2-Approximation algorithm for Vertex Cover.
    Args:
        graph: Adjacency list representation of the graph.
    Returns:
        A set representing the vertex cover.
    """
    cover = set()
    edges = set((u, v) for u in graph for v in graph[u])
    
    while edges:
        u, v = edges.pop()
        cover.update([u, v])
        edges = {e for e in edges if u not in e and v not in e}
    
    return cover

# Example usage
graph = {
    0: [1, 2],
    1: [0, 2],
    2: [0, 1, 3],
    3: [2]
}
print(vertex_cover_approximation(graph))
```

---

### Task 2: Traveling Salesperson Problem (TSP) - Nearest Neighbor Heuristic
#### Objective
Solve TSP using the **Nearest Neighbor Heuristic**.

#### Problem
Input: A weighted graph representing distances between cities.  
Output: An approximate tour that visits all cities and returns to the start.

#### Algorithm
1. Start at any city.
2. Move to the nearest unvisited city.
3. Repeat until all cities are visited.
4. Return to the starting city.

#### Implementation
```python
def tsp_nearest_neighbor(graph, start):
    """
    Nearest Neighbor Heuristic for TSP.
    Args:
        graph: Dictionary representing the weighted graph.
        start: Starting node.
    Returns:
        The tour and its cost.
    """
    n = len(graph)
    visited = {start}
    tour = [start]
    current = start
    total_cost = 0
    
    while len(visited) < n:
        next_city = min(
            (city for city in graph[current] if city not in visited),
            key=lambda city: graph[current][city]
        )
        total_cost += graph[current][next_city]
        visited.add(next_city)
        tour.append(next_city)
        current = next_city
    
    # Return to the start
    total_cost += graph[current][start]
    tour.append(start)
    return tour, total_cost

# Example usage
graph = {
    0: {1: 10, 2: 15, 3: 20},
    1: {0: 10, 2: 35, 3: 25},
    2: {0: 15, 1: 35, 3: 30},
    3: {0: 20, 1: 25, 2: 30}
}
print(tsp_nearest_neighbor(graph, 0))
```

---

### Task 3: Local Search for Max-Cut Problem
#### Objective
Optimize the Max-Cut problem using a local search algorithm.

#### Problem
Input: A graph $G(V, E)$.  
Output: A partition of $V$ into two sets $S$ and $T$ such that the number of edges between $S$ and $T$ is maximized.

#### Algorithm
1. Start with a random partition of vertices.
2. Iteratively move vertices between sets $S$ and $T$ to improve the cut value.
3. Stop when no single move improves the cut.

#### Implementation
```python
import random

def max_cut_local_search(graph):
    """
    Local Search for Max-Cut Problem.
    Args:
        graph: Adjacency list of the graph.
    Returns:
        The sets S and T and the cut size.
    """
    vertices = list(graph.keys())
    random.shuffle(vertices)
    S, T = set(vertices[:len(vertices)//2]), set(vertices[len(vertices)//2:])
    
    def cut_size():
        return sum(1 for u in S for v in T if v in graph[u])
    
    improved = True
    while improved:
        improved = False
        for v in list(S) + list(T):
            if v in S:
                new_S, new_T = S - {v}, T | {v}
            else:
                new_S, new_T = S | {v}, T - {v}
            
            new_cut_size = sum(1 for u in new_S for v in new_T if v in graph[u])
            if new_cut_size > cut_size():
                S, T = new_S, new_T
                improved = True
    
    return S, T, cut_size()

# Example usage
graph = {
    0: [1, 2],
    1: [0, 2, 3],
    2: [0, 1],
    3: [1]
}
print(max_cut_local_search(graph))
```

---

## Additional Exercises
1. Implement a 3-approximation algorithm for the Set Cover problem.
2. Use simulated annealing to solve TSP.
3. Explore the trade-offs between brute force and approximation techniques for Knapsack.

---

## Submission Instructions
1. Submit the following files:
   - `vertex_cover.py`: Implementation of the Vertex Cover approximation.
   - `tsp_heuristic.py`: Nearest Neighbor Heuristic for TSP.
   - `max_cut_local_search.py`: Local search for Max-Cut.
2. Include a report (`report.pdf`) discussing:
   - Approximation ratios achieved.
   - Performance analysis of local search vs. exact algorithms.
3. Submit via Canvas by the due date.

---

## Additional Resources
- [Approximation Algorithms (GeeksforGeeks)](https://www.geeksforgeeks.org/approximation-algorithms/)
- [Local Search Methods](https://en.wikipedia.org/wiki/Local_search_(optimization))
- [TSP Approximation](https://www.math.uwaterloo.ca/~bico/papers/tsp.pdf)