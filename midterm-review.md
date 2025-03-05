# Midterm Exam Revision – Algorithm Design Course

This document provides an overview of key algorithmic topics, including definitions, pseudocode, examples, and applications.

---

# **1. Basic Definitions & Applications**
## **Graph Connectivity and Traversal**
- **Graph Representation**: Adjacency List vs. Adjacency Matrix.
- **Graph Traversal**: Depth-First Search (DFS) and Breadth-First Search (BFS).

### **Depth-First Search (DFS)**
```
DFS(graph, node, visited):
    mark node as visited
    for each neighbor in graph[node]:
        if neighbor is not visited:
            DFS(graph, neighbor)
```
✅ Used in **cycle detection**, **topological sorting**, and **connected components**.

### **Breadth-First Search (BFS)**
```
BFS(graph, start):
    queue = [start]
    mark start as visited
    while queue is not empty:
        node = queue.pop()
        for each neighbor in graph[node]:
            if neighbor is not visited:
                mark neighbor as visited
                queue.append(neighbor)
```
✅ Used in **shortest paths in unweighted graphs**.

## **Testing Bipartiteness**
- A graph is **bipartite** if it can be colored using **two colors** without adjacent nodes having the same color.
- BFS can test bipartiteness in **O(V + E)**.

## **DAGs and Topological Ordering**
- **Directed Acyclic Graph (DAG)**: A directed graph with no cycles.
- **Topological Sorting** orders vertices **such that every directed edge (u, v) has u before v**.
- **Kahn’s Algorithm** (BFS-based) & **DFS-based sorting**.

---

# **2. Greedy Paradigm & Interval Scheduling**
## **Greedy Algorithm Concept**
1. **Make the best local choice at each step**.
2. **Prove correctness via greedy stays ahead, exchange argument, or optimal substructure**.

## **Interval Scheduling**
- Given `n` activities `(start, end)`, **maximize the number of non-overlapping activities**.
- **Greedy Strategy**: Always select the activity that **finishes earliest**.

### **Pseudocode for Interval Scheduling**
```
sort activities by finish time
selected = []
for each activity a:
    if a does not overlap with last selected:
        add a to selected
```
✅ **O(n log n)** due to sorting.

## **Optimal Caching**
- **Least Recently Used (LRU)**: Replace the least recently accessed element.
- **FIFO (First-In-First-Out)**: Replace the oldest element.

---

# **3. Algorithm Design Paradigms**
## **Motivation & Efficiency**
- **Brute-force algorithms**: Try all possibilities.
- **Divide & Conquer, Greedy, and Dynamic Programming**: Structured approaches for optimization.

## **Run-Time Analysis**
- **Big-O Notation**: Upper bound complexity.
- **Common Complexities**: O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ).

---

# **4. Minimum Spanning Tree (MST)**
## **Prim’s Algorithm**
- Start from any node, repeatedly pick the **smallest edge** that connects to the tree.
```
Prim(graph):
    initialize min-heap and add start node
    while heap is not empty:
        pick the minimum edge
        add its neighbor to the MST
```
✅ **O(E log V)** using a priority queue.

## **Kruskal’s Algorithm**
- Sort edges by weight.
- Add edge if it doesn’t form a cycle (use Union-Find).

✅ **O(E log E)**.

---

# **5. Huffman Coding**
## **Lossless Compression**
1. **Build a frequency table**.
2. **Create a priority queue** (min-heap).
3. **Construct Huffman Tree**.

### **Huffman Encoding Algorithm**
```
Huffman(frequencies):
    create a priority queue of nodes
    while more than one node:
        extract two smallest nodes
        merge them into a new node
        insert back into queue
```
✅ **O(n log n)**.

---

# **6. Divide-and-Conquer Paradigm**
## **Merge Sort**
```
MergeSort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = MergeSort(arr[:mid])
    right = MergeSort(arr[mid:])
    return Merge(left, right)
```
✅ **O(n log n)**.

## **Counting Inversions**
- Modify merge sort to count **out-of-order pairs**.

---

# **7. Divide-and-Conquer II: Integer Multiplication & Closest Pair of Points**
## **Karatsuba Algorithm**
```
Karatsuba(x, y):
    if x or y is small, return x * y
    split x and y into halves
    compute three multiplications recursively
    combine results
```
✅ **O(n^log₂3) ≈ O(n¹.⁵⁸)**.

## **Closest Pair of Points**
- **Divide points into two halves**.
- **Find closest pair in each half**.
- **Merge step: Check across the split**.
✅ **O(n log n)**.

---

# **8. Stable Matching Problem**
## **Gale-Shapley Algorithm**
- **Deferred acceptance** strategy.

### **Pseudocode**
```
GaleShapley(menPrefs, womenPrefs):
    while there is an unengaged man:
        m proposes to his favorite w who hasn't rejected him
        if w is free:
            match (m, w)
        else:
            if w prefers m over current partner m':
                match (m, w)
                unengage(m')
            else:
                w rejects m
```
✅ **O(n²)**.

## **Key Properties**
- Always finds a **stable matching**.
- **Men-optimal, women-pessimal**.

## **Applications**
1. **College admissions**.
2. **Medical residency matching**.
3. **Job recruitment**.

---

# **Summary Table**
| Topic | Algorithm | Complexity |
|--------|------------|-------------|
| **Graph Traversal** | BFS/DFS | O(V+E) |
| **Bipartiteness** | BFS | O(V+E) |
| **Topological Sorting** | DFS/Kahn’s | O(V+E) |
| **Greedy** | Interval Scheduling | O(n log n) |
| **MST** | Prim/Kruskal | O(E log V) |
| **Huffman Coding** | Huffman Tree | O(n log n) |
| **Sorting** | Merge Sort | O(n log n) |
| **Integer Multiplication** | Karatsuba | O(n^1.58) |
| **Closest Pair of Points** | Divide & Conquer | O(n log n) |
| **Stable Matching** | Gale-Shapley | O(n²) |

---

# **Practice Problems**
1. Implement **DFS & BFS** for a graph.
2. Implement **Kruskal’s & Prim’s Algorithm** for MST.
3. Implement **Huffman Encoding**.
4. Implement **Merge Sort** with inversion counting.
5. Implement **Gale-Shapley Algorithm** for stable matching.
6. Solve **interval scheduling** using a greedy approach.

---

# **References**
- 📖 **Introduction to Algorithms – CLRS**.
- 📖 **Algorithm Design – Jon Kleinberg & Éva Tardos**.