# Max-Flow Problem, Ford-Fulkerson Algorithm, Maximum Flows, and Minimum Cuts

This document covers **maximum flow problems**, including **Ford-Fulkerson Algorithm**, and explores the **Max-Flow Min-Cut Theorem**. We discuss problem formulations, recurrence relations, pseudocode, and real-world applications.

---

## **1. The Maximum Flow Problem**
### **Problem Statement**
Given a directed graph `G = (V, E)`, where:
- Each edge `(u, v)` has a **capacity** `c(u, v)`.
- There is a **source** `s` and a **sink** `t`.
- The goal is to determine the **maximum amount of flow** that can be pushed from `s` to `t` without violating the edge capacities.

### **Flow Constraints**
1. **Capacity Constraint**: Flow on an edge cannot exceed its capacity:
   ```
   0 ≤ f(u, v) ≤ c(u, v)
   ```
2. **Flow Conservation**: For every vertex except `s` and `t`, incoming flow must equal outgoing flow:
   ```
   ∑ f(v, u) = ∑ f(u, w)  for all u ∈ V \ {s, t}
   ```
3. **Skew Symmetry**: Flow in one direction negates flow in the reverse direction:
   ```
   f(u, v) = -f(v, u)
   ```

---

## **2. Ford-Fulkerson Algorithm**
### **Key Idea**
The algorithm repeatedly finds an **augmenting path** from `s` to `t` in the **residual graph**, increasing the flow along the path until no more augmenting paths exist.

### **Steps**
1. Start with `f(u, v) = 0` for all edges.
2. While there is an **augmenting path** in the residual graph:
   - Find the **minimum residual capacity** along the path.
   - Augment the flow along the path.
   - Update the residual graph.
3. When no augmenting path exists, the current flow is the **maximum flow**.

### **Pseudocode**
```
FordFulkerson(G, s, t):
    Initialize flow f(u, v) = 0 for all edges
    While there exists an augmenting path P in residual graph G_f:
        Find bottleneck capacity: Δ = min {c_f(u, v) | (u, v) ∈ P}
        Augment flow along P by Δ
        Update residual capacities: c_f(u, v) -= Δ, c_f(v, u) += Δ
    Return max flow value
```
✅ **Time Complexity**:
- **O(E * max flow value)** (for DFS-based search).
- **O(VE²)** (for BFS-based Edmonds-Karp variant).

---

## **3. Residual Graph and Augmenting Paths**
The **residual graph** `G_f` contains:
- Forward edges with remaining capacity.
- Backward edges representing the flow that can be reduced.

An **augmenting path** is a path from `s` to `t` in `G_f` where all edges have positive residual capacity.

**Example of Residual Graph Update**
```
Original Graph:
s → (5) → A → (10) → t
s → (5) → B → (5) → t

After augmenting `s → A → t` with flow = 5:
Residual Graph:
s ← (5) ← A  (Back edge added)
A → (5) → t  (Capacity reduced)
```

---

## **4. Maximum Flows and Minimum Cuts**
### **Max-Flow Min-Cut Theorem**
The **maximum flow** in a network is equal to the **minimum cut capacity**, where a **minimum cut** `(S, T)` is a partition of `V` such that:
```
Capacity(S, T) = ∑ c(u, v) for all edges (u, v) where u ∈ S, v ∈ T
```
### **Finding the Minimum Cut**
1. Run **Ford-Fulkerson** to find `max-flow`.
2. Construct the **residual graph**.
3. Perform a **BFS/DFS from `s`** in the residual graph to identify **reachable vertices** (`S`).
4. **Cut edges** are edges from `S` to `T`.

---

## **5. Edmonds-Karp Algorithm**
### **Key Idea**
- Uses **BFS** instead of DFS to find **shortest augmenting paths**.
- Guarantees **O(VE²) complexity**.

### **Pseudocode**
```
EdmondsKarp(G, s, t):
    Initialize flow f(u, v) = 0 for all edges
    While BFS(G_f, s, t) finds an augmenting path P:
        Find bottleneck capacity: Δ = min {c_f(u, v) | (u, v) ∈ P}
        Augment flow along P by Δ
        Update residual capacities
    Return max flow value
```
✅ **O(VE²) time complexity**.

---

## **6. Applications of Max-Flow**
✔ **Network Routing** – Maximize data flow in networks.  
✔ **Bipartite Matching** – Assign tasks to workers optimally.  
✔ **Circulation Problems** – Model traffic, logistics, and supply chains.  
✔ **Image Segmentation** – Used in **computer vision**.  

---

## **Summary Table**
| **Concept** | **Explanation** | **Time Complexity** |
|------------|----------------|---------------------|
| **Max-Flow Problem** | Find the maximum flow in a network from `s` to `t` | – |
| **Ford-Fulkerson** | Finds augmenting paths and updates residual graph | O(E * max flow) |
| **Residual Graph** | Tracks remaining capacities and possible augmenting paths | – |
| **Min-Cut Theorem** | Max flow equals the minimum cut capacity | – |
| **Edmonds-Karp** | BFS-based Ford-Fulkerson | O(VE²) |

---

## **Practice Problems**
1. Implement **Ford-Fulkerson Algorithm** for a directed graph.
2. Find the **minimum cut** in a flow network using residual graphs.
3. Modify **Edmonds-Karp** to handle undirected graphs.

---

## **References**
- 📖 **Introduction to Algorithms – CLRS**.
- 📖 **Algorithm Design – Jon Kleinberg & Éva Tardos**.
- 🔗 [Max-Flow Visualization](https://www.cs.usfca.edu/~galles/visualization/Flow.html).