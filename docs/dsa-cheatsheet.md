# DSA Quick Reference Cheatsheet 📋

## Time Complexity Hierarchy (Best to Worst)

```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2^n) < O(n!)
```

**Common Examples:**
- `O(1)`: Array access, hash map lookup
- `O(log n)`: Binary search, balanced tree operations
- `O(n)`: Linear search, array traversal
- `O(n log n)`: Merge sort, heap sort, quick sort (average)
- `O(n²)`: Bubble sort, nested loops
- `O(2^n)`: Recursive fibonacci, subsets
- `O(n!)`: Permutations

---

## Data Structure Operations

### Array / List
| Operation | Time |
|-----------|------|
| Access | O(1) |
| Search | O(n) |
| Insert (end) | O(1) amortized |
| Insert (middle) | O(n) |
| Delete | O(n) |

**Use when:** Need fast access by index

---

### Hash Map / Dict
| Operation | Time (avg) | Time (worst) |
|-----------|------------|--------------|
| Access | O(1) | O(n) |
| Insert | O(1) | O(n) |
| Delete | O(1) | O(n) |
| Search | O(1) | O(n) |

**Use when:** Need O(1) lookups, counting frequencies

---

### Set
| Operation | Time (avg) |
|-----------|------------|
| Add | O(1) |
| Remove | O(1) |
| Contains | O(1) |

**Use when:** Need to track unique elements, fast membership testing

---

### Stack
| Operation | Time |
|-----------|------|
| Push | O(1) |
| Pop | O(1) |
| Peek | O(1) |

**Use when:** LIFO, expression parsing, backtracking, DFS

---

### Queue
| Operation | Time |
|-----------|------|
| Enqueue | O(1) |
| Dequeue | O(1) |
| Peek | O(1) |

**Use when:** FIFO, BFS, task scheduling

---

### Heap (Priority Queue)
| Operation | Time |
|-----------|------|
| Insert | O(log n) |
| Get min/max | O(1) |
| Remove min/max | O(log n) |
| Heapify | O(n) |

**Use when:** Top K elements, median, priority scheduling

---

### Binary Search Tree (Balanced)
| Operation | Time (avg) | Time (worst) |
|-----------|------------|--------------|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

**Use when:** Need sorted order + fast operations

---

### Trie
| Operation | Time |
|-----------|------|
| Insert | O(m) |
| Search | O(m) |
| Prefix search | O(m) |

*m = length of word*

**Use when:** Prefix matching, autocomplete, spell check

---

## Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable? |
|-----------|------|---------|-------|-------|---------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes |

**When to use:**
- **Merge Sort**: Need stable, guaranteed O(n log n)
- **Quick Sort**: Average case, in-place
- **Heap Sort**: O(1) space, O(n log n) guaranteed
- **Counting Sort**: Small range of integers

---

## Graph Algorithms

### DFS (Depth-First Search)
- **Time:** O(V + E)
- **Space:** O(V)
- **Use:** Connected components, cycle detection, topological sort

### BFS (Breadth-First Search)
- **Time:** O(V + E)
- **Space:** O(V)
- **Use:** Shortest path (unweighted), level-order traversal

### Dijkstra's Algorithm
- **Time:** O((V + E) log V) with heap
- **Space:** O(V)
- **Use:** Shortest path (weighted, non-negative)

### Topological Sort
- **Time:** O(V + E)
- **Space:** O(V)
- **Use:** Task scheduling, course prerequisites

---

## Pattern Recognition Guide

### Problem → Pattern Mapping

**"Contiguous subarray with condition"** → Sliding Window

**"Pairs in sorted array"** → Two Pointers

**"All combinations/permutations"** → Backtracking

**"Optimization (max/min)"** → Dynamic Programming or Greedy

**"Shortest path"** → BFS (unweighted) or Dijkstra (weighted)

**"Is there a cycle?"** → DFS or Union Find

**"Top K elements"** → Heap

**"Range queries"** → Segment Tree or Binary Indexed Tree

**"Search in sorted"** → Binary Search

**"Parentheses matching"** → Stack

**"Tree level-order"** → BFS (queue)

**"Tree paths"** → DFS (recursion)

---

## Common Code Patterns

### Binary Search Template
```python
left, right = 0, len(arr) - 1
while left <= right:
    mid = left + (right - left) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        left = mid + 1
    else:
        right = mid - 1
```

### DFS (Recursion)
```python
def dfs(node, visited):
    if node in visited:
        return
    visited.add(node)
    for neighbor in graph[node]:
        dfs(neighbor, visited)
```

### BFS (Queue)
```python
from collections import deque
queue = deque([start])
visited = {start}
while queue:
    node = queue.popleft()
    for neighbor in graph[node]:
        if neighbor not in visited:
            visited.add(neighbor)
            queue.append(neighbor)
```

### Sliding Window
```python
left = 0
for right in range(len(arr)):
    # Add arr[right] to window
    while window_invalid:
        # Remove arr[left] from window
        left += 1
    # Update result
```

### Two Pointers
```python
left, right = 0, len(arr) - 1
while left < right:
    if condition:
        # move appropriate pointer
```

### Backtracking
```python
def backtrack(path, choices):
    if is_solution(path):
        result.append(path[:])
        return
    for choice in choices:
        path.append(choice)
        backtrack(path, remaining_choices)
        path.pop()
```

---

## Edge Cases Checklist

Always consider:
- ✅ Empty input (`[]`, `""`, `None`)
- ✅ Single element
- ✅ All elements same
- ✅ Duplicates
- ✅ Negative numbers
- ✅ Maximum constraints (10^5 elements)
- ✅ Minimum constraints (0, 1 element)
- ✅ Sorted vs unsorted
- ✅ Integer overflow (for large numbers)

---

## Python Built-ins Quick Reference

### Collections
```python
from collections import Counter, defaultdict, deque

# Counter: frequency counting
count = Counter([1,2,2,3])  # {1:1, 2:2, 3:1}

# defaultdict: default values
graph = defaultdict(list)

# deque: double-ended queue
queue = deque([1,2,3])
queue.append(4)      # Add right
queue.appendleft(0)  # Add left
queue.pop()          # Remove right
queue.popleft()      # Remove left
```

### Heapq (Min Heap)
```python
import heapq

heap = []
heapq.heappush(heap, item)
smallest = heapq.heappop(heap)
heapq.heapify(list)  # Convert list to heap

# Max heap: negate values
heapq.heappush(heap, -item)
```

### Bisect (Binary Search)
```python
import bisect

# Find insertion point
pos = bisect.bisect_left(arr, x)   # Leftmost
pos = bisect.bisect_right(arr, x)  # Rightmost

# Insert in sorted order
bisect.insort(arr, x)
```

---

## Bit Manipulation

| Operation | Code | Use Case |
|-----------|------|----------|
| Check if bit set | `n & (1 << i)` | Test i-th bit |
| Set bit | `n \| (1 << i)` | Set i-th bit to 1 |
| Clear bit | `n & ~(1 << i)` | Set i-th bit to 0 |
| Toggle bit | `n ^ (1 << i)` | Flip i-th bit |
| Check power of 2 | `n & (n-1) == 0` | True if power of 2 |
| Count set bits | `bin(n).count('1')` | Number of 1s |

---

## Math Formulas

**Sum of 1 to n:** `n * (n + 1) / 2`

**Sum of squares:** `n * (n + 1) * (2n + 1) / 6`

**Combinations:** `C(n, k) = n! / (k! * (n-k)!)`

**Permutations:** `P(n, k) = n! / (n-k)!`

**GCD:** Use `math.gcd(a, b)`

**LCM:** `(a * b) / gcd(a, b)`

---

## Interview Tips

**Before coding:**
1. Clarify requirements and constraints
2. Work through 2-3 examples manually
3. Identify pattern/approach
4. Explain your approach
5. Discuss time/space complexity
6. Get confirmation before coding

**While coding:**
- Think out loud
- Use meaningful variable names
- Handle edge cases
- Test with examples

**After coding:**
- Walk through code
- Test with examples
- Discuss optimizations
- Time/space analysis

---

**Keep this cheatsheet handy during practice!**
