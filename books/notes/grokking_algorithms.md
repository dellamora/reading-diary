# Grokking Algorithms

## Big O Notation

- `log` always refers to log₂ in computer science.
- Examples:
  - 2³ = 8, so log₂(8) = 3
  - 2⁴ = 16, so log₂(16) = 4
  - 2⁵ = 32, so log₂(32) = 5

- Big O notation describes an algorithm's worst-case time complexity.
- Common Big O run times (from fastest to slowest):
  1. O(log n): Logarithmic time (e.g., Binary Search)
  2. O(n): Linear time (e.g., Simple Search)
  3. O(n log n): Linearithmic time (e.g., Quicksort)
  4. O(n²): Quadratic time (e.g., Selection Sort)
  5. O(n!): Factorial time (e.g., Traveling Salesperson problem)

- Algorithm speed is measured by the growth in the number of operations as input size increases.
- O(log n) is faster than O(n), with the difference becoming more significant as the input size grows.
- Binary search:
  - Only works on sorted lists
  - Has logarithmic time complexity O(log n)
  - Significantly faster than simple search

- The constant factor in Big O notation can matter in practice (e.g., Quicksort vs. Merge Sort).
- For simple vs. binary search, the difference in Big O complexity (O(n) vs. O(log n)) usually outweighs constant factors.

## Memory and Data Structures

| Operation | Arrays | Linked Lists |
|-----------|--------|--------------|
| Reading   | O(1)   | O(n)         |
| Insertion | O(n)   | O(1)         |

- Computer memory is conceptually similar to a set of numbered drawers.
- Arrays store elements of the same type contiguously in memory.
- Linked lists can store different types and dynamically grow or shrink.
- Stack: Last In, First Out (LIFO)
- Queue: First In, First Out (FIFO)

## Recursion

- Recursion occurs when a function calls itself.
- Every recursive function has:
  1. Base case (termination condition)
  2. Recursive case
- All function calls are added to the call stack.
- Excessive recursion can lead to stack overflow.

## Hash Tables

- Hash functions map strings to numbers.
- Ideal for mapping web addresses to IP addresses.
- Collisions occur when multiple keys hash to the same slot.
- Collision resolution: often implemented using linked lists at each slot.
- Performance depends on:
  1. Low load factor
  2. Good hash function
- Useful for caching and detecting duplicates.

## Graphs

- Breadth-First Search (BFS): Finds shortest path in unweighted graphs.
- Dijkstra's Algorithm: Finds shortest path in weighted graphs (no negative weights).
- Bellman-Ford Algorithm: Handles graphs with negative weights.

## Greedy Algorithms

- Make locally optimal choices at each step.
- Often provide good approximations but not always optimal solutions.

## Dynamic Programming

- Useful for optimization problems with constraints.
- Applicable when problems can be broken into discrete subproblems.
- Typically involves creating a grid of subproblem solutions.
- Grid cells usually contain the values being optimized.

## K-Nearest Neighbors (KNN)

- Used for classification and regression tasks.
- Classification: Categorizing into groups.
- Regression: Predicting a numerical value.
- Requires feature extraction: converting items into comparable numerical lists.
- Selecting relevant features is crucial for KNN's success.