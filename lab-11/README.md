# Lab 11: NP Problems

## Overview
This lab introduces the concepts of NP (nondeterministic polynomial time) problems, focusing on problem complexity, NP-completeness, and practical approaches to tackle NP problems. Students will work with problems like the Traveling Salesperson Problem (TSP), Knapsack Problem, and SAT, exploring both brute-force and heuristic methods.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the class of NP problems and their significance in computational theory.
2. Differentiate between P, NP, NP-complete, and NP-hard problems.
3. Solve NP problems using brute-force and heuristic approaches.
4. Explore approximation algorithms for intractable problems.

---

## Lab Outline

### 1. **Introduction to NP Problems**
- **Definition of P and NP**: 
  - P: Problems solvable in polynomial time.
  - NP: Problems verifiable in polynomial time.
- **NP-Complete**: Problems in NP for which every other NP problem can be reduced to it in polynomial time.
- Examples: TSP, Knapsack Problem, SAT.

### 2. **Brute-Force Solutions**
- Understand brute-force approaches and their time complexity.
- Example: Exhaustively generating all possible solutions for TSP.

### 3. **Heuristic and Approximation Methods**
- Use heuristics to find approximate solutions within reasonable timeframes.
- Explore greedy algorithms, dynamic programming, and local search methods.

---

## Tasks

### Task 1: Traveling Salesperson Problem (TSP)
Find the shortest route that visits all given cities and returns to the starting point.

#### Problem
Input: A graph where vertices represent cities and edges represent distances.  
Output: The minimum distance to complete the tour.

#### Implementation
**Brute-Force Approach**:
1. Generate all possible permutations of cities.
2. Calculate the total distance for each permutation.
3. Return the minimum distance.

```python
from itertools import permutations

def tsp_brute_force(graph, start):
    cities = list(range(len(graph)))
    cities.remove(start)
    min_distance = float('inf')
    best_route = []

    for perm in permutations(cities):
        current_distance = graph[start][perm[0]] + sum(
            graph[perm[i]][perm[i + 1]] for i in range(len(perm) - 1)
        ) + graph[perm[-1]][start]
        
        if current_distance < min_distance:
            min_distance = current_distance
            best_route = [start] + list(perm) + [start]
    
    return min_distance, best_route

# Example usage
graph = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0],
]
print(tsp_brute_force(graph, 0))
```

**Heuristic Approach**:
- Implement the **Nearest Neighbor** heuristic to approximate the solution.

---

### Task 2: Knapsack Problem
Solve the 0/1 Knapsack Problem to maximize value within a weight constraint.

#### Problem
Input: A list of items, each with a weight and value, and a maximum weight capacity.  
Output: The maximum total value of items that can fit in the knapsack.

#### Implementation
**Dynamic Programming Approach**:
```python
def knapsack(values, weights, capacity):
    n = len(values)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            if weights[i - 1] <= w:
                dp[i][w] = max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1])
            else:
                dp[i][w] = dp[i - 1][w]

    return dp[n][capacity]

# Example usage
values = [60, 100, 120]
weights = [10, 20, 30]
capacity = 50
print(knapsack(values, weights, capacity))
```

---

### Task 3: Satisfiability Problem (SAT)
Check whether a given Boolean formula in Conjunctive Normal Form (CNF) is satisfiable.

#### Problem
Input: A Boolean formula in CNF.  
Output: A satisfying assignment of variables, if one exists.

#### Implementation
**Backtracking Approach**:
1. Use recursive backtracking to assign truth values to variables.
2. Check if the assignment satisfies all clauses.

---

### Task 4: Approximation Algorithms
Explore approximation algorithms for NP-complete problems.

#### Problem: Vertex Cover
Input: A graph with vertices and edges.  
Output: A set of vertices that covers all edges.

#### Implementation Hint
Use a greedy algorithm:
1. Pick the edge with the highest degree.
2. Add its vertices to the vertex cover.
3. Remove all edges incident to those vertices.
4. Repeat until all edges are covered.

---

## Code Template
```python
# Sample function for approximation of Vertex Cover
def vertex_cover_approx(graph):
    cover = set()
    edges = set(graph)

    while edges:
        u, v = edges.pop()
        cover.update([u, v])
        edges = {e for e in edges if u not in e and v not in e}

    return cover
```

---

## Submission Instructions
1. Save your solutions in files named `tsp.py`, `knapsack.py`, `sat.py`, and `vertex_cover.py`.
2. Ensure all code is well-documented.
3. Submit your work via Canvas by the deadline.

---

## Additional Resources
- [P vs NP Problem](https://en.wikipedia.org/wiki/P_versus_NP_problem)
- [Dynamic Programming in Knapsack Problem](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)
- [Traveling Salesperson Problem Explanation](https://www.tutorialspoint.com/traveling-salesman-problem)
