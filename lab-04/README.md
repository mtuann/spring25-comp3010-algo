# Greedy Algorithms: Overview, Interval Scheduling, and Optimal Caching

## Overview
The **greedy paradigm** is a powerful algorithmic approach where we make the best choice at each step without reconsidering past choices. This method is often used in optimization problems where **local choices** lead to a **globally optimal solution**.

### Topics Covered:
1. **Greedy Paradigm**
2. **Interval Scheduling (Activity Selection)**
3. **Optimal Caching (Page Replacement Algorithms)**

---

## 1. **Overview of the Greedy Paradigm**
A **greedy algorithm** builds up a solution step by step, always choosing the **best possible option** at each step. The key components of a greedy algorithm:
- **Greedy Choice Property**: A global optimal solution can be reached by choosing locally optimal choices.
- **Optimal Substructure**: An optimal solution to a problem contains optimal solutions to subproblems.

### **Steps in Designing a Greedy Algorithm**
1. **Identify the problem’s optimal substructure**.
2. **Prove that a greedy choice leads to an optimal solution**.
3. **Design an efficient algorithm (often O(n log n) or O(n))**.

📌 **Use cases**: **Scheduling, caching, Huffman coding, MST (Kruskal’s/Prim’s algorithm).**

---

## 2. **Interval Scheduling (Activity Selection Problem)**
The **Interval Scheduling Problem** involves selecting the **maximum number of non-overlapping intervals** from a given set.

### **Problem Statement**
- Given **n intervals** `[start_i, end_i]`, find the **maximum number of non-overlapping intervals**.

### **Greedy Strategy**
1. **Sort intervals by their end time** (`end_i` in ascending order).
2. **Iterate through the sorted list**, selecting intervals that **do not overlap** with previously chosen ones.
3. **Continue until no more intervals can be selected**.

### **Pseudocode**
```
IntervalScheduling(intervals):
    Sort intervals by increasing end time
    selected = []
    last_end = -∞
    
    for (start, end) in intervals:
        if start ≥ last_end:
            selected.append((start, end))
            last_end = end
    
    return selected  # Maximum set of non-overlapping intervals
```

📌 **Time Complexity**: **O(n log n)** (due to sorting).  
📌 **Use Cases**:
- Scheduling tasks with deadlines.
- Assigning non-overlapping meetings to a room.

---

## 3. **Optimal Caching (Page Replacement Algorithms)**
Optimal caching is about **efficient memory management**. A **cache** stores frequently used items, but when it is **full**, a **replacement strategy** is needed.

### **Common Page Replacement Algorithms**
#### **1. Optimal Page Replacement (Belady’s Algorithm)**
- Replace the page that will **not be used for the longest time** in the future.
- **Requires future knowledge** → **Not practical but optimal**.

**Pseudocode:**
```
OptimalCache(pages, cache_size):
    cache = []
    
    for i in range(len(pages)):
        if pages[i] in cache:
            continue  # Page already in cache
        
        if len(cache) < cache_size:
            cache.append(pages[i])
        else:
            future_uses = {page: pages[i+1:].index(page) if page in pages[i+1:] else float('inf') for page in cache}
            page_to_remove = max(future_uses, key=future_uses.get)
            cache.remove(page_to_remove)
            cache.append(pages[i])
```
📌 **Use Case**: Theoretical **baseline for cache eviction policies**.

#### **2. Least Recently Used (LRU)**
- Replace the **least recently used page**.
- **Implemented using a HashMap + Doubly Linked List** (O(1) operations).

**Pseudocode (Using Linked HashMap-like structure):**
```
LRUCache(capacity):
    cache = OrderedDict()
    
    Get(key):
        if key not in cache:
            return -1
        Move key to end of cache
        return cache[key]
    
    Put(key, value):
        if key in cache:
            Move key to end of cache
        elif len(cache) == capacity:
            Remove oldest item (cache.popitem(last=False))
        cache[key] = value
```
📌 **Time Complexity**: **O(1) for both get and put** using an **OrderedDict**.

#### **3. Least Frequently Used (LFU)**
- Removes the **least frequently accessed item**.
- **More accurate than LRU** but **complex to implement**.

📌 **Use Cases of Caching Algorithms**:
- **Operating systems (virtual memory management)**.
- **Web browsers (page caching)**.
- **Databases (query optimization)**.

---

## **Learning Outcomes**
By the end of this module, you should be able to:
✔ Design **greedy algorithms** for various problems.  
✔ Solve the **interval scheduling problem** optimally.  
✔ Implement **caching strategies** such as **LRU, LFU, and Optimal Page Replacement**.

---

## **Resources**
- 📖 **Algorithm Design** - Jon Kleinberg & Éva Tardos.
- 📖 **Introduction to Algorithms (CLRS)** - Chapter on **Greedy Algorithms**.
- 🔗 **LeetCode Greedy Problems**: [LeetCode](https://leetcode.com/problem-list/greedy/)

---

## **Exercises**
1. Implement **Interval Scheduling** and test with different datasets.
2. Implement **LRU and LFU caching** with different page requests.
3. Solve **"Activity Selection Problem"** using **Greedy Strategy**.
4. Compare **LRU, LFU, and Optimal Caching** in terms of performance.