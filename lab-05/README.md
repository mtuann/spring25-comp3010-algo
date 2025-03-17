# Minimum Spanning Tree (MST) & Huffman Codes

## Overview
This module covers two important graph algorithms:
1. **Minimum Spanning Trees (MST)** – Efficient ways to connect all nodes in a weighted graph with minimal cost.
2. **Huffman Codes** – A greedy algorithm used for optimal data compression.

---

# 1. **Minimum Spanning Tree (MST)**

### **Definition**
A **Minimum Spanning Tree (MST)** of a weighted graph is a **subset of edges** that:
- Connects all the vertices **without forming a cycle**.
- Has the **minimum possible total weight**.

📌 **Applications**:
- Network Design (Computer networks, power grids).
- Clustering in Machine Learning.
- Approximate solutions to NP-hard problems like **Traveling Salesman Problem (TSP)**.

---

## **Prim’s Algorithm (Greedy Approach)**
Prim’s algorithm builds the MST **incrementally**, starting from any node and **expanding to the nearest vertex**.

### **Steps**
1. Select **any node** as the starting point.
2. Add the **smallest edge** that connects a visited vertex to an unvisited vertex.
3. Repeat until **all vertices are included**.

### **Pseudocode**
```
PrimMST(graph):
    Initialize MST set = { }
    Start from an arbitrary vertex
    While there are unvisited vertices:
        Find the minimum weight edge that connects MST to an unvisited vertex
        Add this edge to the MST set
    Return MST
```

### **Time Complexity**
- **O(V²) using an adjacency matrix** (brute force).
- **O(E log V) using a priority queue** (efficient for sparse graphs).

📌 **Example**:  
Given a weighted graph:
```
     2      3
  A-----B------C
   \    |      |
  6 \   | 8    | 5
     \  |      |
      D-------E
        9
```
Prim’s MST selects **minimum edges** without forming cycles.

---

## **Kruskal’s Algorithm (Greedy + Disjoint Set Union)**
Kruskal’s algorithm sorts edges by **weight** and **adds them if they don’t form a cycle**.

### **Steps**
1. Sort all edges by weight.
2. Initialize an empty MST.
3. Iterate through edges:
   - If an edge connects **two different trees**, add it to the MST.
   - Otherwise, discard it (to prevent cycles).
4. Repeat until **MST contains V-1 edges**.

### **Pseudocode**
```
KruskalMST(graph):
    Sort edges by weight
    Initialize MST set = { }
    For each edge (u, v) in sorted edges:
        If u and v are in different components:
            Add (u, v) to MST
            Merge the components
    Return MST
```

### **Time Complexity**
- **O(E log E) using sorting + DSU (Disjoint Set Union)**.

📌 **Example**:  
For the same graph, Kruskal’s algorithm **selects the lightest edges**, ensuring no cycles.

### **Comparison: Prim vs. Kruskal**
| Feature        | Prim’s Algorithm  | Kruskal’s Algorithm |
|--------------|----------------|----------------|
| Strategy     | Expands from a vertex | Expands from edges |
| Works well for | Dense graphs | Sparse graphs |
| Complexity   | O(E log V) (heap) | O(E log E) (sorting) |

---

# 2. **Huffman Coding (Greedy Algorithm)**
Huffman coding is an **optimal prefix coding** algorithm used in **data compression**.

### **Definition**
- Assigns **variable-length codes** to characters.
- **Frequent characters get shorter codes**.
- **Infrequent characters get longer codes**.

📌 **Applications**:
- File compression (ZIP, GZIP).
- Media compression (JPEG, MP3).
- Transmission encoding.

### **Steps**
1. **Count character frequencies**.
2. **Build a min-heap** where each node is a character.
3. **Merge two smallest nodes** into a new node with their sum as weight.
4. **Repeat until one tree remains**.
5. **Assign 0 to left branches, 1 to right branches**.

### **Pseudocode**
```
HuffmanEncoding(freq):
    Create a min-heap of leaf nodes (characters with frequencies)
    While more than one node in the heap:
        Remove two smallest nodes
        Merge them into a new node (sum of weights)
        Insert back into heap
    Assign binary codes to each character based on tree traversal
```

### **Example**
**Input frequencies**:
```
A: 5, B: 9, C: 12, D: 13, E: 16, F: 45
```
Build tree:
```
        (100)
       /      \
     F(45)    (55)
           /       \
         (30)      (25)
        /    \     /    \
      (14)  E(16) C(12) D(13)
     /   \       
   A(5)  B(9)  
```
Generated **Huffman codes**:
```
A -> 1000
B -> 1001
C -> 110
D -> 111
E -> 101
F -> 0
```
- [Huffman coding step-by-step example](https://www.youtube.com/watch?v=iEm1NRyEe5c).

### **Time Complexity**
- **O(n log n) using heaps**.

📌 **Why Huffman Codes Work?**
- Uses **prefix property**: No code is a prefix of another.
- **Always optimal** for compression when symbol frequencies are known.

---

# **Summary**
✔ **Prim’s & Kruskal’s Algorithms**: Find **Minimum Spanning Trees** for efficient connectivity.  
✔ **Huffman Coding**: A **greedy** method for **optimal compression**.  

---

# **Exercises**
1. Implement **Prim’s and Kruskal’s algorithms** and compare their runtimes on different graphs.
2. Given a set of character frequencies, **construct a Huffman Tree**.
3. Solve **MST problems** on online judges like Codeforces, LeetCode.

---

# **Resources**
- 📖 **Introduction to Algorithms (CLRS)** - MST & Huffman Codes.
- 📖 **Algorithm Design** - Jon Kleinberg & Éva Tardos.