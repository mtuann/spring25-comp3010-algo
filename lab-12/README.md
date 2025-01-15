# Lab 12: P vs NP

## Overview
This lab explores one of the most fundamental questions in computer science: **P vs NP**. The focus is on understanding the difference between P and NP problems, the significance of NP-completeness, and practical approaches to identify and tackle NP problems.

Through a series of tasks and examples, students will:
1. Examine the theoretical foundations of P vs NP.
2. Study NP-complete problems and their characteristics.
3. Implement and analyze solutions for problems in both P and NP.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the concepts of P, NP, NP-complete, and NP-hard problems.
2. Differentiate between problems in P and those in NP.
3. Explore NP-completeness through reductions and practical examples.
4. Implement brute-force and heuristic algorithms to solve NP-complete problems.

---

## Lab Outline

### 1. **Introduction to P vs NP**
- **P (Polynomial Time)**: Problems solvable in polynomial time.
- **NP (Nondeterministic Polynomial Time)**: Problems for which solutions can be verified in polynomial time.
- **NP-Complete Problems**: 
  - A subset of NP problems to which any NP problem can be reduced in polynomial time.
  - Examples: Traveling Salesperson Problem (TSP), SAT, and Knapsack.

### 2. **Reduction and NP-Completeness**
- Concept of reducing one problem to another in polynomial time.
- Understanding the Cook-Levin theorem, which proves that SAT is NP-complete.

### 3. **Practical Approaches to NP Problems**
- Brute-force algorithms for small instances.
- Approximation and heuristic algorithms for larger instances.

---

## Tasks

### Task 1: Identify P and NP Problems
#### Objective
Categorize the following problems as P, NP, or NP-complete:
1. Sorting an array.
2. Finding the shortest path in a graph.
3. 0/1 Knapsack Problem.
4. Boolean Satisfiability Problem (SAT).

#### Instructions
1. Write a brief explanation for each problem.
2. Justify the categorization based on problem complexity.

---

### Task 2: Polynomial Reduction
#### Objective
Perform a reduction from the 3-SAT problem to the Clique problem to understand NP-completeness.

#### Instructions
1. Study the 3-SAT problem:
   - Input: A Boolean formula in Conjunctive Normal Form (CNF) with 3 literals per clause.
   - Output: True if the formula is satisfiable, False otherwise.
2. Learn about the Clique problem:
   - Input: A graph $G$ and a number $k$.
   - Output: True if $G$ has a clique of size $k$.

#### Implementation
1. Write a function that transforms a 3-SAT formula into an equivalent Clique problem instance.
2. Use the following Python template:

```python
def sat_to_clique(clauses, num_variables):
    """
    Convert a 3-SAT problem into a Clique problem.
    Args:
        clauses: List of tuples representing 3-SAT clauses.
        num_variables: Total number of variables in the formula.
    Returns:
        graph: Adjacency matrix representing the graph.
        k: The size of the clique.
    """
    # Example logic to construct graph
    graph = {}
    k = len(clauses)
    # Add logic for reduction
    return graph, k
```

---

### Task 3: Solve the SAT Problem
#### Objective
Implement a brute-force solution for the SAT problem.

#### Problem
Input: A Boolean formula in CNF.  
Output: True if the formula is satisfiable, otherwise False.

#### Implementation
```python
from itertools import product

def is_satisfiable(clauses, num_variables):
    """
    Brute-force solution to SAT.
    Args:
        clauses: List of tuples representing the clauses.
        num_variables: Number of variables in the formula.
    Returns:
        True if satisfiable, False otherwise.
    """
    for assignment in product([True, False], repeat=num_variables):
        if all(any(assignment[abs(lit) - 1] == (lit > 0) for lit in clause) for clause in clauses):
            return True
    return False

# Example usage
clauses = [(-1, 2, 3), (1, -2, 3), (-1, -2, -3)]
num_variables = 3
print(is_satisfiable(clauses, num_variables))
```

---

### Task 4: Approximation Algorithm for Vertex Cover
#### Objective
Solve the Vertex Cover problem using an approximation algorithm.

#### Problem
Input: A graph represented as an adjacency list.  
Output: A vertex cover of the graph.

#### Implementation
```python
def vertex_cover_approx(graph):
    """
    Approximation algorithm for Vertex Cover.
    Args:
        graph: Adjacency list of the graph.
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
print(vertex_cover_approx(graph))
```

---

## Additional Exercises
1. Solve the Hamiltonian Path problem using backtracking.
2. Write a function to reduce the Hamiltonian Path problem to TSP.

---

## Submission Instructions
1. Submit the following files:
   - `problem_classification.txt`: Categorization of problems in Task 1.
   - `sat_to_clique.py`: Implementation of polynomial reduction.
   - `sat_solver.py`: SAT problem solver.
   - `vertex_cover.py`: Approximation algorithm for Vertex Cover.
2. Ensure all code is well-commented and properly structured.
3. Submit via Canvas by the due date.

---

## Additional Resources
- [P vs NP Problem (Wikipedia)](https://en.wikipedia.org/wiki/P_versus_NP_problem)
- [Understanding NP-Completeness](https://www.geeksforgeeks.org/np-completeness-set-1/)
- [Cook-Levin Theorem](https://en.wikipedia.org/wiki/Cook%E2%80%93Levin_theorem)