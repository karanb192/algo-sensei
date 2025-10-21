# Dynamic Programming Pattern 💎

## When to Use

Dynamic Programming (DP) is used when:
- **Optimization problems**: Find maximum/minimum
- **Counting problems**: Count number of ways
- **Decision problems**: Is it possible to...?
- **Overlapping subproblems**: Same calculation repeated
- **Optimal substructure**: Optimal solution contains optimal subsolutions

**Keywords to look for:**
- "maximum/minimum"
- "longest/shortest"
- "count number of ways"
- "is it possible"
- Often involves sequences, strings, or grids

## Core Concept

Break problem into smaller subproblems, solve each once, and store results to avoid recalculation.

**Recursion → Recursion + Memoization → Bottom-Up DP**

---

## DP Problem-Solving Framework

### Step 1: Identify if it's DP
- Can you break it into smaller identical subproblems?
- Do subproblems overlap?
- Does optimal solution depend on optimal subsolutions?

### Step 2: Define State
What information do you need to track?
- `dp[i]` = answer for first i elements
- `dp[i][j]` = answer for substring s[i:j]
- `dp[i][j]` = answer at position (i, j) in grid

### Step 3: Find Recurrence Relation
How does `dp[i]` relate to previous states?
- Example: `dp[i] = dp[i-1] + dp[i-2]` (Fibonacci)

### Step 4: Identify Base Cases
What are the simplest subproblems?
- `dp[0] = ...`
- `dp[1] = ...`

### Step 5: Determine Iteration Order
Which direction to fill the DP table?

### Step 6: Compute Final Answer
Where is the final answer stored?

---

## Approach 1: Top-Down (Memoization)

Start with recursion, add caching.

```python
def dp_memoization(n, memo=None):
    # Initialize memo
    if memo is None:
        memo = {}

    # Base case
    if n <= 1:
        return n

    # Check if already computed
    if n in memo:
        return memo[n]

    # Recursive relation
    memo[n] = dp_memoization(n - 1, memo) + dp_memoization(n - 2, memo)

    return memo[n]
```

**Pros:**
- Intuitive (follows natural recursion)
- Only computes needed subproblems
- Easy to convert from recursion

**Cons:**
- Recursion overhead
- Stack space usage
- Can hit recursion limit

---

## Approach 2: Bottom-Up (Tabulation)

Build solution iteratively from base cases.

```python
def dp_tabulation(n):
    # Base cases
    if n <= 1:
        return n

    # Initialize DP table
    dp = [0] * (n + 1)
    dp[0] = 0
    dp[1] = 1

    # Fill table bottom-up
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]

    return dp[n]
```

**Pros:**
- No recursion overhead
- More space-efficient (can optimize)
- Faster in practice

**Cons:**
- Less intuitive
- Computes all subproblems (even if not needed)

---

## Common DP Patterns

### Pattern 1: Linear DP (1D)

**Structure:** `dp[i]` depends on previous elements

**Example: House Robber**
```python
def rob(nums):
    if not nums:
        return 0
    if len(nums) == 1:
        return nums[0]

    dp = [0] * len(nums)
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])

    for i in range(2, len(nums)):
        # Either rob current house or skip it
        dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

    return dp[-1]
```

**Space Optimization:**
```python
def rob_optimized(nums):
    if not nums:
        return 0

    prev2 = 0  # dp[i-2]
    prev1 = 0  # dp[i-1]

    for num in nums:
        current = max(prev1, prev2 + num)
        prev2 = prev1
        prev1 = current

    return prev1
```

**LeetCode Examples:**
- #198: House Robber
- #70: Climbing Stairs
- #746: Min Cost Climbing Stairs

---

### Pattern 2: 2D DP (Grid/Matrix)

**Structure:** `dp[i][j]` depends on previous cells

**Example: Unique Paths**
```python
def uniquePaths(m, n):
    # dp[i][j] = number of ways to reach (i, j)
    dp = [[0] * n for _ in range(m)]

    # Base cases: first row and column
    for i in range(m):
        dp[i][0] = 1
    for j in range(n):
        dp[0][j] = 1

    # Fill table
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1]

    return dp[m - 1][n - 1]
```

**Space Optimization (1D array):**
```python
def uniquePaths_optimized(m, n):
    dp = [1] * n  # Only need one row

    for i in range(1, m):
        for j in range(1, n):
            dp[j] += dp[j - 1]

    return dp[n - 1]
```

**LeetCode Examples:**
- #62: Unique Paths
- #64: Minimum Path Sum
- #221: Maximal Square

---

### Pattern 3: String DP (Subsequence/Substring)

**Structure:** `dp[i][j]` for two strings or `dp[i][j]` for substring

**Example: Longest Common Subsequence**
```python
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i - 1] == text2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    return dp[m][n]
```

**Example: Longest Palindromic Substring**
```python
def longestPalindrome(s):
    n = len(s)
    if n < 2:
        return s

    # dp[i][j] = is s[i:j+1] a palindrome?
    dp = [[False] * n for _ in range(n)]

    start = 0
    max_length = 1

    # Every single character is a palindrome
    for i in range(n):
        dp[i][i] = True

    # Check for length 2
    for i in range(n - 1):
        if s[i] == s[i + 1]:
            dp[i][i + 1] = True
            start = i
            max_length = 2

    # Check for lengths 3 and above
    for length in range(3, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1

            if s[i] == s[j] and dp[i + 1][j - 1]:
                dp[i][j] = True
                start = i
                max_length = length

    return s[start:start + max_length]
```

**LeetCode Examples:**
- #1143: Longest Common Subsequence
- #5: Longest Palindromic Substring
- #72: Edit Distance
- #10: Regular Expression Matching

---

### Pattern 4: Knapsack (0/1, Unbounded)

**0/1 Knapsack:**
```python
def knapsack(weights, values, capacity):
    n = len(weights)
    # dp[i][w] = max value using first i items with capacity w
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            # Don't take item i-1
            dp[i][w] = dp[i - 1][w]

            # Take item i-1 if it fits
            if weights[i - 1] <= w:
                dp[i][w] = max(
                    dp[i][w],
                    dp[i - 1][w - weights[i - 1]] + values[i - 1]
                )

    return dp[n][capacity]
```

**Space Optimized:**
```python
def knapsack_optimized(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for i in range(len(weights)):
        # Traverse backwards to avoid using same item twice
        for w in range(capacity, weights[i] - 1, -1):
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i])

    return dp[capacity]
```

**Unbounded Knapsack (can use items multiple times):**
```python
def unbounded_knapsack(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for w in range(capacity + 1):
        for i in range(len(weights)):
            if weights[i] <= w:
                dp[w] = max(dp[w], dp[w - weights[i]] + values[i])

    return dp[capacity]
```

**LeetCode Examples:**
- #416: Partition Equal Subset Sum
- #518: Coin Change II
- #322: Coin Change

---

### Pattern 5: Decision Making

**Example: Best Time to Buy and Sell Stock**
```python
def maxProfit(prices):
    if not prices:
        return 0

    # State: hold stock or not hold
    hold = -prices[0]  # Max profit if holding stock
    not_hold = 0       # Max profit if not holding

    for price in prices[1:]:
        new_hold = max(hold, not_hold - price)
        new_not_hold = max(not_hold, hold + price)
        hold = new_hold
        not_hold = new_not_hold

    return not_hold
```

**LeetCode Examples:**
- #121: Best Time to Buy and Sell Stock
- #122: Best Time to Buy and Sell Stock II
- #123: Best Time to Buy and Sell Stock III

---

## Key Insights

### State Definition

Good state definition is crucial:
- Contains all necessary information
- Minimal (avoid redundant info)
- Allows clear recurrence relation

### Recurrence Relation Patterns

**Linear:**
- `dp[i] = f(dp[i-1], dp[i-2], ...)`

**Grid:**
- `dp[i][j] = f(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])`

**String:**
- If match: `dp[i][j] = dp[i-1][j-1] + 1`
- If not: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

**Choice:**
- `dp[i] = max(take_it, leave_it)`

### Space Optimization

**1D DP:** O(n) → O(1)
- Use variables instead of array

**2D DP:** O(m×n) → O(n)
- Only need previous row/column

**Technique:** Process backwards if using same array

---

## Common Mistakes

❌ **Wrong iteration order**
- Must compute dependencies first!

❌ **Off-by-one errors**
- Be careful with indices and sizes

❌ **Missing base cases**
- Initialize properly

❌ **Wrong state definition**
- State must capture all necessary information

❌ **Forgetting to return right value**
- Is answer at dp[n] or dp[n-1]?

---

## DP vs Greedy

| DP | Greedy |
|----|--------|
| Explores all choices | Makes local optimal choice |
| Optimal substructure + overlapping | Greedy choice property |
| Slower (polynomial) | Faster (linear) |
| Always correct for applicable problems | Must prove correctness |

**When to use DP:**
- Greedy doesn't work (counterexample exists)
- Need to count all possibilities
- Optimization with constraints

---

## Practice Problems

### Beginner
- #70: Climbing Stairs
- #746: Min Cost Climbing Stairs
- #198: House Robber

### Intermediate
- #322: Coin Change
- #300: Longest Increasing Subsequence
- #62: Unique Paths
- #5: Longest Palindromic Substring

### Advanced
- #72: Edit Distance
- #1143: Longest Common Subsequence
- #416: Partition Equal Subset Sum
- #1049: Last Stone Weight II

---

**Remember:** DP is recursion + memoization, or bottom-up iteration. The key is finding the right state and recurrence!
