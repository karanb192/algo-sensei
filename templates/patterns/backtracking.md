# Backtracking Pattern 🔙

## When to Use

Backtracking is used when:
- Generate **all combinations/permutations**
- Explore **all possible solutions**
- Make **sequential decisions** with constraints
- "Find all..."
- Constraint satisfaction problems

**Keywords:**
- "all possible"
- "generate all"
- "find all combinations"
- "N-Queens"
- "Sudoku"

---

## Core Concept

Backtracking = DFS + Pruning

Build solution incrementally, and **abandon (backtrack)** if constraints violated.

**Think of it as:** Try a choice → Explore → If fails, undo choice and try another

---

## Universal Backtracking Template

```python
def backtrack(result, path, choices, constraints):
    # Base case: valid solution found
    if is_solution(path):
        result.append(path[:])  # Make copy!
        return

    # Try each possible choice
    for choice in choices:
        # Skip if violates constraints (pruning)
        if not is_valid(choice, path, constraints):
            continue

        # Make choice
        path.append(choice)

        # Explore with this choice
        backtrack(result, path, remaining_choices, constraints)

        # Undo choice (backtrack)
        path.pop()
```

---

## Common Patterns

### Pattern 1: Combinations

**Problem:** Find all k-length combinations from [1..n]

```python
def combine(n, k):
    result = []

    def backtrack(start, path):
        # Base case: found k numbers
        if len(path) == k:
            result.append(path[:])
            return

        # Try numbers from start to n
        for i in range(start, n + 1):
            path.append(i)
            backtrack(i + 1, path)  # Next start is i+1 (no duplicates)
            path.pop()

    backtrack(1, [])
    return result
```

**LeetCode:** #77

**Key:** Start from `i+1` to avoid duplicates and ensure combinations (not permutations)

---

### Pattern 2: Permutations

**Problem:** Find all permutations of array

```python
def permute(nums):
    result = []

    def backtrack(path, remaining):
        # Base case: used all numbers
        if not remaining:
            result.append(path[:])
            return

        # Try each remaining number
        for i in range(len(remaining)):
            # Choose
            path.append(remaining[i])

            # Explore (exclude current number from remaining)
            backtrack(path, remaining[:i] + remaining[i+1:])

            # Undo
            path.pop()

    backtrack([], nums)
    return result
```

**Alternative using visited set:**
```python
def permute(nums):
    result = []
    used = set()

    def backtrack(path):
        if len(path) == len(nums):
            result.append(path[:])
            return

        for num in nums:
            if num not in used:
                path.append(num)
                used.add(num)

                backtrack(path)

                path.pop()
                used.remove(num)

    backtrack([])
    return result
```

**LeetCode:** #46, #47

**Key:** Track which elements are used

---

### Pattern 3: Subsets

**Problem:** Find all subsets of array

```python
def subsets(nums):
    result = []

    def backtrack(start, path):
        # Every path is a valid subset
        result.append(path[:])

        # Try adding each remaining number
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()

    backtrack(0, [])
    return result
```

**LeetCode:** #78

**Key:** Add result at every step (not just base case)

---

### Pattern 4: Combination Sum

**Problem:** Find all combinations that sum to target (can reuse)

```python
def combinationSum(candidates, target):
    result = []

    def backtrack(start, path, current_sum):
        # Pruning: exceeded target
        if current_sum > target:
            return

        # Found valid combination
        if current_sum == target:
            result.append(path[:])
            return

        # Try each candidate
        for i in range(start, len(candidates)):
            path.append(candidates[i])

            # Can reuse same element, so pass i (not i+1)
            backtrack(i, path, current_sum + candidates[i])

            path.pop()

    backtrack(0, [], 0)
    return result
```

**LeetCode:** #39

**Key:** Pass `i` to allow reuse, `i+1` to prevent reuse

---

### Pattern 5: Palindrome Partitioning

```python
def partition(s):
    result = []

    def is_palindrome(sub):
        return sub == sub[::-1]

    def backtrack(start, path):
        # Partitioned entire string
        if start == len(s):
            result.append(path[:])
            return

        # Try each possible partition
        for end in range(start + 1, len(s) + 1):
            substring = s[start:end]

            # Only continue if current part is palindrome
            if is_palindrome(substring):
                path.append(substring)
                backtrack(end, path)
                path.pop()

    backtrack(0, [])
    return result
```

**LeetCode:** #131

---

### Pattern 6: N-Queens

```python
def solveNQueens(n):
    result = []
    board = [['.'] * n for _ in range(n)]

    def is_valid(row, col):
        # Check column
        for i in range(row):
            if board[i][col] == 'Q':
                return False

        # Check diagonal (top-left)
        i, j = row - 1, col - 1
        while i >= 0 and j >= 0:
            if board[i][j] == 'Q':
                return False
            i -= 1
            j -= 1

        # Check diagonal (top-right)
        i, j = row - 1, col + 1
        while i >= 0 and j < n:
            if board[i][j] == 'Q':
                return False
            i -= 1
            j += 1

        return True

    def backtrack(row):
        # Placed queens in all rows
        if row == n:
            result.append([''.join(row) for row in board])
            return

        # Try placing queen in each column
        for col in range(n):
            if is_valid(row, col):
                board[row][col] = 'Q'
                backtrack(row + 1)
                board[row][col] = '.'

    backtrack(0)
    return result
```

**LeetCode:** #51

---

### Pattern 7: Word Search

```python
def exist(board, word):
    rows, cols = len(board), len(board[0])

    def backtrack(r, c, index):
        # Found entire word
        if index == len(word):
            return True

        # Out of bounds or wrong character
        if (r < 0 or r >= rows or c < 0 or c >= cols or
            board[r][c] != word[index]):
            return False

        # Mark as visited
        temp = board[r][c]
        board[r][c] = '#'

        # Explore 4 directions
        found = (backtrack(r + 1, c, index + 1) or
                 backtrack(r - 1, c, index + 1) or
                 backtrack(r, c + 1, index + 1) or
                 backtrack(r, c - 1, index + 1))

        # Restore (backtrack)
        board[r][c] = temp

        return found

    # Try starting from each cell
    for r in range(rows):
        for c in range(cols):
            if backtrack(r, c, 0):
                return True

    return False
```

**LeetCode:** #79

---

## Key Insights

### When to Add to Result?

**At base case:**
- Combinations of fixed size
- Permutations
- N-Queens

**At every step:**
- Subsets (all sizes valid)
- Power set

### Pruning Strategies

**Early termination:**
```python
if current_sum > target:
    return  # Don't explore further
```

**Skip invalid choices:**
```python
if not is_valid(choice):
    continue  # Skip this choice
```

**Sort for pruning:**
```python
candidates.sort()
if current_sum + candidates[i] > target:
    break  # All remaining will exceed
```

### State Management

**Choose-Explore-Unchoose:**
```python
path.append(choice)      # Choose
backtrack(...)           # Explore
path.pop()              # Unchoose
```

**Alternative: Pass copy:**
```python
backtrack(path + [choice])  # No need to pop
# But: more memory overhead
```

---

## Common Mistakes

❌ **Not making a copy**
```python
result.append(path)  # WRONG! Reference changes
result.append(path[:])  # CORRECT! Copy
result.append(list(path))  # Also correct
```

❌ **Forgetting to backtrack**
```python
path.append(choice)
backtrack(...)
# Missing: path.pop()
```

❌ **Wrong start index**
- Combinations: `i + 1` (no duplicates)
- Permutations: all elements (track used)
- Subsets: `i + 1`
- Combination Sum (reusable): `i`

❌ **Modifying input without restoring**
```python
board[r][c] = '#'
backtrack(...)
# Missing: board[r][c] = original_value
```

---

## Optimization Techniques

### 1. Sort for Early Pruning
```python
nums.sort()
for num in nums:
    if current + num > target:
        break  # All remaining too large
```

### 2. Use Sets for Deduplication
```python
if num in used:
    continue
```

### 3. Skip Duplicates
```python
if i > start and nums[i] == nums[i-1]:
    continue
```

---

## Complexity Analysis

**Time:**
- Worst case: O(b^d) where b=branching factor, d=depth
- Permutations: O(n!)
- Subsets: O(2^n)
- Combinations: O(C(n,k))

**Space:**
- Recursion stack: O(d)
- Path storage: O(d)
- Total: O(d)

---

## Practice Problems

### Beginner
- #78: Subsets
- #77: Combinations
- #46: Permutations

### Intermediate
- #39: Combination Sum
- #40: Combination Sum II
- #131: Palindrome Partitioning
- #90: Subsets II

### Advanced
- #51: N-Queens
- #37: Sudoku Solver
- #79: Word Search
- #212: Word Search II

---

## Decision Tree

```
Need all solutions?
    ↓ YES
Sequential decisions with constraints?
    ↓ YES → Backtracking

What type?
    → Fixed size? → Combinations/Permutations
    → All sizes? → Subsets
    → Sum to target? → Combination Sum
    → Placement? → N-Queens
    → Path in grid? → Word Search
```

---

**Remember:** Backtracking is DFS with the ability to "undo" choices. The magic is in choose-explore-unchoose!
