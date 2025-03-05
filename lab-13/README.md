# Approximation Algorithms and Local Search: Load Balancing, Center Selection, Pricing Method, LP Rounding, Knapsack Problem; Local Search, Metropolis Algorithm, Hopfield Neural Network, Maximum Cut

This document provides a structured overview of key topics in **optimization, approximation algorithms, and heuristic methods**. Each section includes definitions, examples, pseudocode, and applications.

---

## **1. Load Balancing**
### **Definition**
- The **Load Balancing Problem** involves distributing computational tasks across multiple processors to minimize the **maximum load**.
- Given `m` machines and `n` jobs with processing times `p1, p2, ..., pn`, assign jobs to machines **minimizing** the maximum load.

### **Greedy Algorithm for Load Balancing**
**Pseudocode (List Scheduling Algorithm)**:
```
LoadBalancing(jobs, machines):
    Initialize an empty list for each machine
    for each job in sorted(jobs, descending order):
        Assign job to machine with the least load
    return maximum load across all machines
```
✅ **Time Complexity:** O(n log n)  

### **Applications**
- **Parallel computing:** Distributing tasks across processors.
- **Network traffic management:** Balancing requests across servers.

---

## **2. Center Selection**
### **Definition**
- Given a set of points in a metric space, choose `k` centers to **minimize the maximum distance** of any point to its nearest center.
- Special case: **k-Center Problem** (NP-hard).

### **Greedy Approximation Algorithm**
**Pseudocode:**
```
GreedyCenterSelection(points, k):
    Choose an arbitrary point as the first center
    for i = 2 to k:
        Select the farthest point from the chosen centers
    return selected centers
```
✅ **Approximation Factor:** `2`

### **Applications**
- **Facility location:** Placing warehouses for optimized delivery.
- **Data clustering:** k-Means initialization.

---

## **3. Pricing Method**
### **Definition**
- **Pricing algorithms** determine **optimal prices** for items based on demand and constraints.
- Used in **auctions, airline ticket pricing, and online ads**.

### **Simple Demand-Based Pricing Algorithm**
```
DynamicPricing(demand, base_price):
    if demand is high:
        increase price
    else if demand is low:
        decrease price
    return new_price
```
✅ **Time Complexity:** O(1) per update.

### **Applications**
- **Airline ticket pricing**
- **E-commerce dynamic pricing**
- **Advertising auctions**

---

## **4. LP Rounding**
### **Definition**
- **Linear Programming (LP) rounding** is used in **approximation algorithms**.
- Solve an **LP relaxation** of an **integer programming problem**, then round fractional values.

### **LP Relaxation Example: Vertex Cover**
#### **LP Formulation**
```
Minimize: ∑ x_v   (sum over all vertices)
Subject to: x_u + x_v ≥ 1 for every edge (u, v)
           0 ≤ x_v ≤ 1
```
#### **LP Rounding Algorithm**
```
LP_Rounding():
    Solve the LP relaxation optimally
    Round all x_v ≥ 0.5 to 1
    Return the rounded solution as the vertex cover
```
✅ **Approximation Factor:** `2`

### **Applications**
- **Approximate solutions for NP-hard problems**
- **Network design optimization**

---

## **5. Knapsack Problem**
### **Definition**
- Given `n` items with **values** `v[i]` and **weights** `w[i]`, and a knapsack of capacity `W`, maximize:
```
Maximize ∑ v[i] * x[i]
Subject to ∑ w[i] * x[i] ≤ W
```
- **0/1 Knapsack:** Items are either taken or not (`x[i] ∈ {0,1}`).
- **Fractional Knapsack:** Items can be split (`x[i] ∈ [0,1]`).

### **Greedy Algorithm for Fractional Knapsack**
```
FractionalKnapsack(items, W):
    Sort items by value/weight ratio in descending order
    for each item:
        if item fits, take full item
        else take fraction
    return total value
```
✅ **Time Complexity:** O(n log n)  

---

## **6. Local Search**
### **Definition**
- Iteratively improves a solution by making **local modifications**.
- Used in **combinatorial optimization**.

### **Example: Local Search for Traveling Salesman**
```
LocalSearch(Tour):
    while there exists an improving swap:
        swap two edges to reduce tour cost
    return optimized tour
```
✅ **Used in:** Scheduling, routing, clustering.

---

## **7. Metropolis Algorithm**
### **Definition**
- **Simulated annealing** variant that **accepts worse solutions with a probability**.
- Helps escape **local minima**.

### **Algorithm**
```
MetropolisAlgorithm(initial_solution, T):
    while not converged:
        new_solution = small_random_change(current_solution)
        if new_solution is better:
            accept
        else accept with probability exp(-ΔE/T)
        Reduce temperature T
    return best solution
```
✅ **Used in:** Optimization, physics simulations.

---

## **8. Hopfield Neural Network**
### **Definition**
- **Recurrent artificial neural network** used for **associative memory and optimization**.

### **Energy Function**
```
E = -1/2 * ∑ Wij * Si * Sj - ∑ θi * Si
```
- `S`: State of neurons.
- `W`: Weights between neurons.

### **Hopfield Network Algorithm**
```
HopfieldNetwork(weights, inputs):
    Initialize neurons randomly
    while state changes:
        Update neurons based on weight connections
    return final stable state
```
✅ **Used in:** Image recognition, memory retrieval.

---

## **9. Maximum Cut**
### **Definition**
- Given a graph `G = (V, E)`, partition `V` into two subsets **maximizing the number of edges between them**.

### **Greedy Approximation Algorithm**
```
MaxCut(G):
    Assign each node to a random partition
    for each node:
        if moving the node increases the cut:
            move it
    return partition
```
✅ **Approximation Factor:** `2`

### **Applications**
- **Network partitioning**
- **VLSI design**
- **Image segmentation**

---

## **10. Summary Table**
| **Concept** | **Definition** | **Example Algorithm** |
|-------------|---------------|----------------------|
| **Load Balancing** | Distributing tasks to minimize max load | Greedy Assignment |
| **Center Selection** | Choosing `k` centers to minimize max distance | Greedy Selection |
| **Pricing Method** | Adjusting prices dynamically | Demand-based Pricing |
| **LP Rounding** | Solving LP relaxations & rounding | Vertex Cover Approximation |
| **Knapsack Problem** | Selecting items to maximize value | Greedy (Fractional) |
| **Local Search** | Iterative solution improvement | 2-Opt for TSP |
| **Metropolis Algorithm** | Simulated annealing variant | Energy-based acceptance |
| **Hopfield Neural Network** | Recurrent NN for optimization | Associative Memory |
| **Maximum Cut** | Partitioning a graph to maximize cut edges | Randomized Approximation |

---

## **11. Practice Problems**
1. Implement **Greedy Load Balancing** for `n` jobs.
2. Solve the **Knapsack Problem** using **Dynamic Programming**.
3. Implement the **Metropolis Algorithm** for TSP.
4. Apply **Hopfield Networks** for pattern recognition.
5. Implement an **approximation algorithm for Maximum Cut**.

---

## **12. References**
- 📖 **Algorithm Design – Kleinberg & Tardos**.
- 📖 **Approximation Algorithms – Vazirani**.
- 📖 **Neural Networks – Haykin**.
- 🔗 [Metropolis Algorithm](https://en.wikipedia.org/wiki/Metropolis_algorithm).