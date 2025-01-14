# Lab 06: Sorting and Searching

## Overview
In this lab, we will delve into two fundamental topics in computer science: **Sorting** and **Searching**. These algorithms are essential for efficient data processing and are often used as building blocks in more complex algorithms.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the importance of sorting and searching algorithms.
2. Implement various sorting algorithms (e.g., Bubble Sort, Selection Sort, Merge Sort, Quick Sort).
3. Explore linear and binary searching techniques.
4. Analyze and compare the performance of these algorithms.

---

## Lab Outline

### 1. **Introduction to Sorting and Searching**
- **Sorting**: Organizing a collection of data in a specific order (e.g., ascending or descending).
  - Applications: Data analysis, databases, search algorithms, etc.
- **Searching**: Finding an element in a collection of data.
  - Applications: Indexing, retrieval systems, etc.

**Why Learn Sorting and Searching?**
- Sorting often simplifies problem-solving.
- Efficient searching relies on sorted data (e.g., binary search).

---

## Getting Started

### Prerequisites
- Familiarity with lists, loops, and functions in Python.
- Knowledge of basic algorithm design principles.

### Files Provided
1. `sorting_searching.py` - A template for your implementations.
2. `test_cases.txt` - Sample data for testing.
3. `README.md` - This instruction file.

---

## Tasks

### Task 1: Implement Sorting Algorithms
#### (a) Bubble Sort
- A simple comparison-based sorting algorithm.
- Repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.
- **Time Complexity**: $O(n^2)$ in the worst and average cases.

**Steps**:
1. Loop through the list multiple times.
2. Swap adjacent elements if needed.
3. Stop early if the list is already sorted.

Example:
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr
```

---

#### (b) Merge Sort
- A divide-and-conquer algorithm that splits the list into halves, sorts each half, and merges them back.
- **Time Complexity**: $O(n \log n)$ in all cases.

**Steps**:
1. Divide the list into two halves.
2. Recursively sort each half.
3. Merge the sorted halves.

Example:
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    sorted_list = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            sorted_list.append(left[i])
            i += 1
        else:
            sorted_list.append(right[j])
            j += 1
    sorted_list.extend(left[i:])
    sorted_list.extend(right[j:])
    return sorted_list
```

---

#### (c) Quick Sort
- Another divide-and-conquer algorithm that selects a pivot and partitions the array.
- **Time Complexity**:
  - Best/Average Case: $O(n \log n)$
  - Worst Case: $O(n^2)$ (when the pivot is poorly chosen).

**Steps**:
1. Pick a pivot.
2. Partition the array around the pivot.
3. Recursively sort the partitions.

Example:
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[0]
    less = [x for x in arr[1:] if x <= pivot]
    greater = [x for x in arr[1:] if x > pivot]
    return quick_sort(less) + [pivot] + quick_sort(greater)
```

---

### Task 2: Implement Searching Algorithms
#### (a) Linear Search
- Sequentially checks each element.
- **Time Complexity**: $O(n)$.

Example:
```python
def linear_search(arr, target):
    for i, val in enumerate(arr):
        if val == target:
            return i
    return -1
```

---

#### (b) Binary Search
- Searches for an element in a sorted array by dividing the search interval in half.
- **Time Complexity**: $O(\log n)$.

Example:
```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```

---

### Task 3: Analyze and Compare Algorithms
1. Compare sorting algorithms:
   - Bubble Sort: Simple but slow.
   - Merge Sort: Efficient and stable.
   - Quick Sort: Fast in practice but sensitive to pivot choice.
2. Compare searching algorithms:
   - Linear Search: Works on unsorted data.
   - Binary Search: Requires sorted data but is faster.

---

## Bonus Task: Visualize Sorting Algorithms
1. Use `matplotlib` to visualize the sorting process.
2. Example:
```python
import matplotlib.pyplot as plt
import time

def visualize_sorting(arr, sort_fn):
    for step in sort_fn(arr):
        plt.bar(range(len(step)), step)
        plt.pause(0.5)
        plt.clf()
    plt.show()
```

---

## Submission Instructions
1. Save your implementations in `sorting_searching.py`.
2. Include screenshots or graphs for the visualization (if completed).
3. Submit all files on Canvas by the deadline.

---

## Additional Resources
- [Sorting Algorithms Visualization](https://visualgo.net/en/sorting)
- [Binary Search Algorithm](https://www.geeksforgeeks.org/binary-search/)

---

## Notes
- Test your code on both small and large datasets.
- Handle edge cases (e.g., empty list, single-element list).
- Include comments explaining your implementation and complexity analysis.