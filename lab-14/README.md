# Lab 14: Randomized Algorithms

## Overview
In this lab, you will explore **randomized algorithms**, which use randomness to make decisions during execution. These algorithms are particularly useful for solving problems efficiently when deterministic methods are slow or infeasible. You'll learn about different types of randomized algorithms, their applications, and implement some of the most common ones.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the concept of randomized algorithms and their classifications (Monte Carlo, Las Vegas).
2. Learn about the trade-offs between efficiency and accuracy in randomized algorithms.
3. Implement randomized techniques to solve real-world computational problems.
4. Analyze the expected runtime and success probabilities of randomized algorithms.

---

## Lab Outline

### 1. **Introduction to Randomized Algorithms**
- **What are randomized algorithms?**
  Algorithms that make random choices during their execution.
- **Types of randomized algorithms:**
  - **Monte Carlo**: Guarantees efficiency; correctness is probabilistic.
  - **Las Vegas**: Guarantees correctness; runtime is probabilistic.
- **Applications:**
  - Optimization.
  - Probabilistic data structures (e.g., Bloom filters).
  - Randomized graph algorithms.

---

## Tasks

### Task 1: Randomized QuickSort
#### Objective
Implement the **Randomized QuickSort** algorithm and analyze its expected runtime.

#### Algorithm
1. Choose a random pivot instead of a fixed pivot.
2. Partition the array around the pivot.
3. Recursively sort the partitions.

#### Implementation
```python
import random

def randomized_partition(arr, low, high):
    pivot_index = random.randint(low, high)
    arr[pivot_index], arr[high] = arr[high], arr[pivot_index]
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

def randomized_quicksort(arr, low, high):
    if low < high:
        pivot_index = randomized_partition(arr, low, high)
        randomized_quicksort(arr, low, pivot_index - 1)
        randomized_quicksort(arr, pivot_index + 1, high)

# Example usage
arr = [10, 7, 8, 9, 1, 5]
randomized_quicksort(arr, 0, len(arr) - 1)
print("Sorted array:", arr)
```

---

### Task 2: Randomized Selection
#### Objective
Find the $k$-th smallest element in an unsorted array using a randomized approach.

#### Algorithm
1. Choose a random pivot.
2. Partition the array around the pivot.
3. Recursively search in the appropriate partition.

#### Implementation
```python
def randomized_select(arr, low, high, k):
    if low == high:
        return arr[low]
    pivot_index = randomized_partition(arr, low, high)
    rank = pivot_index - low + 1
    if rank == k:
        return arr[pivot_index]
    elif k < rank:
        return randomized_select(arr, low, pivot_index - 1, k)
    else:
        return randomized_select(arr, pivot_index + 1, high, k - rank)

# Example usage
arr = [3, 2, 9, 1, 7, 5]
k = 3
print(f"{k}-th smallest element:", randomized_select(arr, 0, len(arr) - 1, k))
```

---

### Task 3: Randomized Graph Algorithm - Minimum Cut
#### Objective
Implement Karger's algorithm to find the **minimum cut** in an undirected graph.

#### Algorithm
1. Randomly select an edge and contract it.
2. Repeat until only two nodes remain.
3. The edges between the remaining nodes form the minimum cut.

#### Implementation
```python
import random
from collections import defaultdict

def karger_min_cut(graph):
    vertices = list(graph.keys())
    edges = [(u, v) for u in graph for v in graph[u]]
    while len(vertices) > 2:
        u, v = random.choice(edges)
        vertices.remove(v)
        graph[u].extend(graph[v])
        for w in graph[v]:
            graph[w] = [u if x == v else x for x in graph[w]]
        edges = [(x, y) for x, y in edges if x != v and y != v and x != y]
    return len(edges)

# Example usage
graph = {
    0: [1, 2],
    1: [0, 2, 3],
    2: [0, 1, 3],
    3: [1, 2]
}
print("Minimum cut:", karger_min_cut(graph))
```

---

## Additional Exercises
1. Implement a Monte Carlo algorithm to estimate $\pi$ using random sampling.
2. Write a program to simulate randomized load balancing in a distributed system.
3. Extend Karger's algorithm to run multiple trials and return the smallest cut.

---

## Submission Instructions
1. Submit the following files:
   - `randomized_quicksort.py`: Randomized QuickSort implementation.
   - `randomized_selection.py`: Randomized selection implementation.
   - `karger_min_cut.py`: Minimum cut algorithm.
2. Include a report (`report.pdf`) discussing:
   - The trade-offs between deterministic and randomized algorithms.
   - Analysis of runtimes and success probabilities.
3. Submit via Canvas by the due date.

---

## Additional Resources
- [Randomized Algorithms (GeeksforGeeks)](https://www.geeksforgeeks.org/randomized-algorithms/)
- [Introduction to Randomized Algorithms (MIT OpenCourseWare)](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-046j-design-and-analysis-of-algorithms-spring-2015/)
- [Karger's Algorithm](https://en.wikipedia.org/wiki/Karger%27s_algorithm)

---

## Key Takeaways
- Randomized algorithms often provide simpler and faster solutions than deterministic ones for certain problems.
- The randomness can lead to trade-offs between performance and reliability.
- Understanding the types and applications of randomized algorithms helps in choosing the right approach for a given problem.