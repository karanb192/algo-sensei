# Sliding Window Pattern 🪟

## When to Use

Use Sliding Window when you have:
- **Contiguous** subarray or substring problems
- Need to find max/min length with a condition
- "All distinct characters"
- "At most K elements"
- Fixed or variable window size

**Keywords to look for:**
- "contiguous subarray"
- "substring"
- "longest/shortest"
- "maximum/minimum sum"
- "all characters"
- "at most K"

## Core Concept

Instead of recalculating for each window from scratch (O(n×k)), maintain a window and slide it efficiently (O(n)).

## Two Types of Windows

### 1. Fixed-Size Window
Window size is constant (k).

### 2. Variable-Size Window
Window size changes based on condition.

---

## Fixed-Size Window Template

**Use when:** "subarray of size k", "average of k elements"

```python
def fixed_window(arr, k):
    if len(arr) < k:
        return None

    # Initialize first window
    window_sum = sum(arr[:k])
    result = window_sum

    # Slide the window
    for i in range(k, len(arr)):
        # Add new element, remove leftmost
        window_sum += arr[i] - arr[i - k]
        result = max(result, window_sum)  # or min, or other operation

    return result
```

**Time:** O(n)
**Space:** O(1)

**Example Problems:**
- Maximum sum of subarray of size K
- Average of subarrays of size K

---

## Variable-Size Window Template

**Use when:** window size depends on a condition

### Template 1: Maximum Window (Longest)

```python
def max_window(arr):
    left = 0
    max_length = 0
    window_state = {}  # Track window contents

    for right in range(len(arr)):
        # Add arr[right] to window
        window_state[arr[right]] = window_state.get(arr[right], 0) + 1

        # Shrink window while condition violated
        while not is_valid(window_state):
            # Remove arr[left] from window
            window_state[arr[left]] -= 1
            if window_state[arr[left]] == 0:
                del window_state[arr[left]]
            left += 1

        # Update result (window is valid here)
        max_length = max(max_length, right - left + 1)

    return max_length
```

### Template 2: Minimum Window (Shortest)

```python
def min_window(arr, target):
    left = 0
    min_length = float('inf')
    window_state = {}

    for right in range(len(arr)):
        # Add arr[right] to window
        window_state[arr[right]] = window_state.get(arr[right], 0) + 1

        # Shrink window while condition satisfied
        while is_valid(window_state, target):
            # Update result before shrinking
            min_length = min(min_length, right - left + 1)

            # Remove arr[left] from window
            window_state[arr[left]] -= 1
            if window_state[arr[left]] == 0:
                del window_state[arr[left]]
            left += 1

    return min_length if min_length != float('inf') else 0
```

**Time:** O(n) - each element added and removed at most once
**Space:** O(k) - where k is window size or alphabet size

---

## Common Problem Patterns

### Pattern 1: Longest Substring Without Repeating Characters

```python
def lengthOfLongestSubstring(s):
    left = 0
    max_length = 0
    char_index = {}  # Track last seen index

    for right in range(len(s)):
        # If character seen before and in current window
        if s[right] in char_index and char_index[s[right]] >= left:
            # Move left past the previous occurrence
            left = char_index[s[right]] + 1

        char_index[s[right]] = right
        max_length = max(max_length, right - left + 1)

    return max_length
```

**LeetCode:** #3
**Pattern:** Variable window, track characters in hash map

---

### Pattern 2: Minimum Window Substring

```python
def minWindow(s, t):
    if not t or not s:
        return ""

    # Count characters in t
    target_count = {}
    for char in t:
        target_count[char] = target_count.get(char, 0) + 1

    required = len(target_count)  # Unique chars needed
    formed = 0  # Unique chars matched so far

    window_count = {}
    left = 0
    min_length = float('inf')
    result = (0, 0)

    for right in range(len(s)):
        # Add character to window
        char = s[right]
        window_count[char] = window_count.get(char, 0) + 1

        # Check if this character count matches target
        if char in target_count and window_count[char] == target_count[char]:
            formed += 1

        # Try to shrink window
        while left <= right and formed == required:
            # Update result if this window is smaller
            if right - left + 1 < min_length:
                min_length = right - left + 1
                result = (left, right)

            # Remove left character
            char = s[left]
            window_count[char] -= 1
            if char in target_count and window_count[char] < target_count[char]:
                formed -= 1

            left += 1

    return "" if min_length == float('inf') else s[result[0]:result[1] + 1]
```

**LeetCode:** #76
**Pattern:** Minimum window with all characters

---

### Pattern 3: Longest Substring with At Most K Distinct

```python
def lengthOfLongestSubstringKDistinct(s, k):
    if k == 0:
        return 0

    left = 0
    max_length = 0
    char_count = {}

    for right in range(len(s)):
        # Add character to window
        char_count[s[right]] = char_count.get(s[right], 0) + 1

        # Shrink until we have at most k distinct
        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1

        max_length = max(max_length, right - left + 1)

    return max_length
```

**LeetCode:** #340, #159
**Pattern:** At most K distinct elements

---

### Pattern 4: Maximum Sum Subarray of Size K (Fixed)

```python
def maxSumSubarray(arr, k):
    if len(arr) < k:
        return -1

    # First window
    window_sum = sum(arr[:k])
    max_sum = window_sum

    # Slide window
    for i in range(k, len(arr)):
        window_sum += arr[i] - arr[i - k]
        max_sum = max(max_sum, window_sum)

    return max_sum
```

**Pattern:** Fixed-size window

---

### Pattern 5: Fruit Into Baskets (At Most 2 Types)

```python
def totalFruit(fruits):
    left = 0
    max_fruits = 0
    basket = {}  # Type -> count

    for right in range(len(fruits)):
        # Add fruit to basket
        basket[fruits[right]] = basket.get(fruits[right], 0) + 1

        # More than 2 types? Shrink window
        while len(basket) > 2:
            basket[fruits[left]] -= 1
            if basket[fruits[left]] == 0:
                del basket[fruits[left]]
            left += 1

        max_fruits = max(max_fruits, right - left + 1)

    return max_fruits
```

**LeetCode:** #904
**Pattern:** At most K distinct (K=2)

---

## Key Insights

### Window State Tracking

Use appropriate data structure:
- **Hash Map:** Count frequencies, track characters
- **Set:** Track distinct elements
- **Counter (Python):** Simplify counting
- **Variables:** Simple sum/product/etc.

### Shrinking the Window

**For MAXIMUM (longest):**
- Shrink WHILE condition is VIOLATED
- Update result AFTER shrinking

**For MINIMUM (shortest):**
- Shrink WHILE condition is SATISFIED
- Update result BEFORE shrinking

### Window Validity

Define `is_valid()` based on problem:
- All distinct? `len(window) == len(set(window))`
- At most K? `len(distinct_chars) <= k`
- Contains all? `window_count >= target_count`

## Common Mistakes

❌ **Not considering empty inputs**
```python
if not arr or len(arr) < k:
    return result
```

❌ **Off-by-one in window size**
- Window size = `right - left + 1`, not `right - left`

❌ **Forgetting to shrink**
- MUST shrink when condition violated

❌ **Wrong result update timing**
- Maximum: after shrinking
- Minimum: before shrinking

❌ **Not handling edge of window removal**
```python
window_count[arr[left]] -= 1
if window_count[arr[left]] == 0:
    del window_count[arr[left]]  # Clean up!
```

## Complexity Analysis

**Time Complexity:** O(n)
- Each element added once (right pointer)
- Each element removed once (left pointer)
- Total: 2n operations

**Space Complexity:**
- O(1) for fixed windows with simple operations
- O(k) where k is window size or alphabet size

## Sliding Window vs Two Pointers

| Sliding Window | Two Pointers |
|----------------|--------------|
| Contiguous elements | Can skip elements |
| Window expands/shrinks | Pointers move based on condition |
| Subarray/substring | Pairs/triplets |
| Need to track window state | Usually just compare values |

## Practice Problems

### Beginner
- #643: Maximum Average Subarray I (fixed)
- #1456: Maximum Number of Vowels in Substring (fixed)

### Intermediate
- #3: Longest Substring Without Repeating Characters
- #424: Longest Repeating Character Replacement
- #904: Fruit Into Baskets
- #159: Longest Substring with At Most Two Distinct Characters

### Advanced
- #76: Minimum Window Substring
- #340: Longest Substring with At Most K Distinct Characters
- #209: Minimum Size Subarray Sum
- #992: Subarrays with K Different Integers

## Quick Decision Tree

```
Subarray/substring problem?
    ↓ YES
Is window size fixed?
    ↓ YES → Use fixed-size template
    ↓ NO
        ↓
    Looking for MAXIMUM (longest)?
        ↓ YES → Shrink while VIOLATED
    Looking for MINIMUM (shortest)?
        ↓ YES → Shrink while SATISFIED
```

---

**Remember:** Sliding window transforms nested loops O(n×k) into single pass O(n) by reusing computation!
