# Randomized Algorithms: Contention Resolution, Global Min Cut, Linearity of Expectation; Max 3-Satisfiability, Universal Hashing, Chernoff Bounds, Load Balancing

This document provides a structured overview of key topics in **probabilistic algorithms, combinatorial optimization, and randomized methods**. Each section includes definitions, examples, pseudocode, and applications.

---

## **1. Contention Resolution**
### **Definition**
- **Contention resolution** deals with allocating shared resources among competing users **without conflicts**.
- Used in **distributed computing, scheduling, and networking**.

### **Randomized Backoff Algorithm (Exponential)**
```
RandomizedBackoff():
    for each process:
        Wait for a random time `t` (exponential distribution)
        If resource is free, acquire it
        Else, double waiting time and retry
```
✅ **Used in:** **Ethernet, Wi-Fi (CSMA/CA), and network protocols**.

### **Applications**
- **Wireless networks** (collision avoidance in CSMA/CA).
- **Parallel computing** (task scheduling in multi-core systems).

---

## **2. Global Min Cut**
### **Definition**
- Given a graph `G = (V, E)`, a **minimum cut** is a set of edges that, when removed, **disconnects the graph** with minimum weight.

### **Karger’s Randomized Min Cut Algorithm**
```
KargerMinCut(G):
    while |V| > 2:
        Pick a random edge (u, v)
        Merge u and v (contract edge)
        Remove self-loops
    return remaining edges as min cut
```
✅ **Expected time complexity:** `O(n^2 log n)`

### **Applications**
- **Network reliability analysis**
- **Graph partitioning**

---

## **3. Linearity of Expectation**
### **Definition**
- If `X` and `Y` are two random variables, then:
  ```
  E[X + Y] = E[X] + E[Y]
  ```
  even if `X` and `Y` are dependent.

### **Example: Number of Empty Bins in Hashing**
- If `n` balls are thrown into `m` bins randomly, the expected number of empty bins is:
  ```
  E[# empty bins] = ∑ P(bin i is empty) = m * (1 - 1/m)^n
  ```
✅ **Useful in:** **Algorithm analysis, probabilistic counting, randomized algorithms**.

---

## **4. Max 3-Satisfiability (MAX 3-SAT)**
### **Definition**
- Given a **Boolean formula** with **3 literals per clause**, find an assignment that **maximizes the number of satisfied clauses**.

### **Randomized Approximation Algorithm**
```
MAX3SAT(Formula):
    Assign each variable True/False randomly
    return fraction of satisfied clauses
```
✅ **Guarantees:** `7/8` approximation.

### **Applications**
- **AI (constraint satisfaction problems)**
- **Circuit design**

---

## **5. Universal Hashing**
### **Definition**
- A **family of hash functions** `{h: U → [m]}` is **universal** if:
  ```
  P(h(x) = h(y)) ≤ 1/m  for x ≠ y
  ```
- Ensures low probability of **collisions**.

### **Construction of a Universal Hash Family**
```
UniversalHash(x, a, b, p, m):
    return ((a * x + b) mod p) mod m
```
where:
- `p` is a prime number `> U`
- `a, b` are random integers from `[1, p-1]`

✅ **Used in:** **Hash tables, cryptography, data structures**.

---

## **6. Chernoff Bounds**
### **Definition**
- **Chernoff Bounds** provide a way to bound the probability that a sum of independent random variables deviates significantly from its expectation.

### **Chernoff Bound for Coin Tosses**
- If `X` is the sum of `n` independent {0,1} variables with expectation `μ`, then:
  ```
  P(X ≥ (1+δ)μ) ≤ e^(-δ²μ/3)  for 0 ≤ δ ≤ 1
  ```

### **Applications**
- **Randomized algorithms**
- **Load balancing**
- **Network analysis**

---

## **7. Load Balancing (Randomized)**
### **Definition**
- **Distribute `n` tasks across `m` machines** to balance the load.

### **Randomized Load Balancing Algorithm**
```
RandomizedLoadBalancing(jobs, machines):
    for each job:
        Assign to a random machine
    return max load on any machine
```
✅ **Expected max load:** `O(log log m / log m)`

### **Applications**
- **Parallel computing**
- **Distributed systems**

---

## **8. Summary Table**
| **Concept** | **Definition** | **Example Algorithm** |
|-------------|---------------|----------------------|
| **Contention Resolution** | Avoiding conflicts in resource allocation | Randomized Backoff |
| **Global Min Cut** | Finding smallest cut in a graph | Karger’s Algorithm |
| **Linearity of Expectation** | Expected value is additive | Expected empty bins in hashing |
| **MAX 3-SAT** | Maximizing satisfied clauses | Randomized Assignment |
| **Universal Hashing** | Reducing hash collisions | `(ax + b) mod p` |
| **Chernoff Bounds** | Bounding deviation probability | Tail bound for coin tosses |
| **Load Balancing** | Distributing tasks randomly | Assign to random machine |

---

## **9. Practice Problems**
1. Implement **Karger’s Min Cut Algorithm**.
2. Simulate **randomized contention resolution** for network requests.
3. Prove **linearity of expectation** for summing random variables.
4. Solve **MAX 3-SAT** using a randomized algorithm.
5. Implement **universal hashing** for a dictionary.
6. Use **Chernoff Bounds** to analyze **randomized load balancing**.

---

## **10. References**
- 📖 **Randomized Algorithms – Motwani & Raghavan**
- 📖 **Probability and Computing – Mitzenmacher & Upfal**
- 📖 **Introduction to Algorithms – Cormen et al.**
- 🔗 [Chernoff Bounds (Wikipedia)](https://en.wikipedia.org/wiki/Chernoff_bound)