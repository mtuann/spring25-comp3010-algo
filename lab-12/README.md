# Definition of NP, NP-Completeness, co-NP, Asymmetry of NP

This document covers **complexity classes**, the concept of **NP-completeness**, the **co-NP** class, and the **asymmetry of NP**. It includes definitions, examples, pseudocode, and applications.

---

## **1. Definition of NP**
### **Complexity Classes Overview**
- **P (Polynomial Time):** Problems that can be solved in polynomial time `O(n^k)`, where `k` is a constant.
- **NP (Nondeterministic Polynomial Time):** Problems where a given solution can be **verified** in polynomial time.

### **Formal Definition**
A problem belongs to **NP** if there exists a polynomial-time algorithm that **verifies** a proposed solution.

#### **Example: Hamiltonian Cycle Problem**
**Input:** Graph `G = (V, E)`.  
**Output:** Does `G` contain a cycle that visits every vertex exactly once?  
**Verification:** Given a proposed cycle, we can check if:
- It includes all vertices.
- Each edge exists in `G`.
- It forms a cycle.

✅ **Verification takes O(n²), so the problem is in NP**.

### **Pseudocode: Hamiltonian Cycle Verification**
```
Verify_Hamiltonian_Cycle(G, cycle):
    if length(cycle) ≠ |V|:
        return False
    for i in range(|V|):
        if (cycle[i], cycle[i+1]) not in E:
            return False
    return True
```
✅ **Time Complexity:** O(n²).

---

## **2. NP-Completeness**
### **Definition**
A problem **X** is **NP-complete** if:
1. `X` is in NP (**Verifiable in polynomial time**).
2. Every problem in NP **reduces to X in polynomial time** (NP-hardness).

### **Why NP-Completeness Matters?**
- If **any** NP-complete problem is solved in polynomial time, then **P = NP**.
- **Key open question in CS:** **Does P = NP?**

### **Examples of NP-Complete Problems**
1. **SAT (Boolean Satisfiability Problem)**
   - Given a Boolean formula, determine if there exists an assignment of variables that makes the formula true.
   - **First known NP-complete problem** (Cook’s Theorem).
   
2. **Traveling Salesman Problem (TSP)**
   - Given `n` cities and distances, find the shortest tour visiting all cities exactly once.

3. **3-SAT Reduction to Independent Set**
   - Convert a SAT formula into a graph where satisfying assignments correspond to independent sets.

### **Pseudocode: SAT Verification**
```
Verify_SAT(Formula, Assignment):
    for each clause in Formula:
        if no literal in clause is satisfied by Assignment:
            return False
    return True
```
✅ **Time Complexity:** O(nm) (where `n` is variables, `m` is clauses).

---

## **3. co-NP**
### **Definition**
- **co-NP** consists of problems where **NO-instance** can be verified in polynomial time.
- A problem `X` is in **co-NP** if its complement (`not X`) is in **NP**.

### **Example: Composite Numbers**
- **NP Problem:** Checking if a number is **prime** (difficult to verify directly).
- **co-NP Problem:** Checking if a number is **composite** (easy to verify with a factor).

### **NP vs co-NP**
| **Class**  | **Verification** |
|------------|----------------|
| **NP**     | Fast verification of **YES** instances |
| **co-NP**  | Fast verification of **NO** instances |

#### **Does NP = co-NP?**
- **Unknown** (similar to P vs NP).
- Many believe **NP ≠ co-NP**.
- **Factoring** is in **co-NP**, but unknown if it's in NP.

---

## **4. Asymmetry of NP**
### **Key Observation**
- Many **NP problems** don’t have known polynomial-time solutions.
- **co-NP problems** often behave differently than NP problems.
- **Example:** If SAT is in P, then SAT’s complement (TAUT) is also in P.

### **Open Problems**
1. **Does NP = co-NP?**  
   - If `X` is NP-complete, then `not X` is likely not in NP.
2. **If P ≠ NP, is there a problem in NP but not in P or NP-complete?**  
   - **Example:** Factoring is in NP, but not known to be NP-complete.

---

## **5. Summary Table**
| **Concept**              | **Definition** | **Examples** |
|--------------------------|---------------|-------------|
| **P**                    | Solvable in polynomial time | Sorting, Shortest Path |
| **NP**                   | Solution verifiable in polynomial time | SAT, Hamiltonian Cycle |
| **NP-Complete**          | Hardest problems in NP | 3-SAT, TSP, Vertex Cover |
| **co-NP**                | Problems where **NO** can be verified in poly-time | Composite Number |
| **Asymmetry of NP**      | Some problems may be in NP but not in co-NP | Open Question |

---

## **6. Practice Problems**
1. Prove that **3-SAT is NP-complete**.
2. Verify if a given **TSP tour** is correct in polynomial time.
3. Show that **Factoring is in co-NP**.
4. If SAT is in P, prove that **TAUT is in P**.

---

## **7. References**
- 📖 **Introduction to Algorithms – CLRS**.
- 📖 **Computers and Intractability – Garey & Johnson**.
- 🔗 [P vs NP Problem](https://www.claymath.org/wp-content/uploads/2022/06/pvsnp.pdf).