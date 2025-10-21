# Binary Search Pattern 🔍

## When to Use

Binary Search applies when:
- **Sorted array** or monotonic search space
- Finding target value
- Finding boundary (first/last occurrence)
- Search space has order property
- "Find minimum/maximum such that..."

**Time:** O(log n) - halves search space each iteration
**Space:** O(1) iterative, O(log n) recursive

---

## Classic Binary Search Template

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = left + (right - left) // 2  # Avoids overflow

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1  # Search right half
        else:
            right = mid - 1  # Search left half

    return -1  # Not found
```

**Key:** `left + (right - left) // 2` avoids integer overflow vs `(left + right) // 2`

---

## Finding Boundaries Template

### Find First Occurrence (Lower Bound)

```python
def find_first(arr, target):
    left, right = 0, len(arr) - 1
    result = -1

    while left <= right:
        mid = left + (right - left) // 2

        if arr[mid] == target:
            result = mid
            right = mid - 1  # Keep searching left
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return result
```

### Find Last Occurrence (Upper Bound)

```python
def find_last(arr, target):
    left, right = 0, len(arr) - 1
    result = -1

    while left <= right:
        mid = left + (right - left) // 2

        if arr[mid] == target:
            result = mid
            left = mid + 1  # Keep searching right
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return result
```

---

## Search Space Binary Search

For "find minimum X such that condition(X) is true"

```python
def search_space_binary_search(left, right, condition):
    result = -1

    while left <= right:
        mid = left + (right - left) // 2

        if condition(mid):
            result = mid
            right = mid - 1  # Try to find smaller
        else:
            left = mid + 1

    return result
```

**Examples:**
- Find minimum speed to deliver packages in time
- Find minimum capacity to ship packages
- Find square root

---

## Common Patterns

### Pattern 1: Search in Rotated Sorted Array

```python
def search_rotated(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid

        # Left half is sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # Right half is sorted
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1
```

**LeetCode:** #33, #81

---

### Pattern 2: Find Peak Element

```python
def findPeakElement(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = left + (right - left) // 2

        if nums[mid] > nums[mid + 1]:
            # Peak is on left side (or mid is peak)
            right = mid
        else:
            # Peak is on right side
            left = mid + 1

    return left
```

**LeetCode:** #162

---

### Pattern 3: Find Minimum in Rotated Array

```python
def findMin(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = left + (right - left) // 2

        if nums[mid] > nums[right]:
            # Minimum is in right half
            left = mid + 1
        else:
            # Minimum is in left half (or mid)
            right = mid

    return nums[left]
```

**LeetCode:** #153

---

### Pattern 4: Search Insert Position

```python
def searchInsert(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return left  # Insert position
```

**LeetCode:** #35

---

### Pattern 5: Capacity to Ship Packages

```python
def shipWithinDays(weights, days):
    def can_ship(capacity):
        current_weight = 0
        days_needed = 1

        for weight in weights:
            if current_weight + weight > capacity:
                days_needed += 1
                current_weight = weight
            else:
                current_weight += weight

        return days_needed <= days

    left = max(weights)  # Minimum possible capacity
    right = sum(weights)  # Maximum possible capacity

    while left < right:
        mid = left + (right - left) // 2

        if can_ship(mid):
            right = mid  # Try smaller capacity
        else:
            left = mid + 1  # Need larger capacity

    return left
```

**LeetCode:** #1011

---

## Template Variations

### Inclusive Right (left <= right)
```python
while left <= right:
    mid = left + (right - left) // 2
    if condition:
        return mid
    elif ...:
        left = mid + 1
    else:
        right = mid - 1
```

**Use when:**
- Looking for exact match
- Can return immediately

### Exclusive Right (left < right)
```python
while left < right:
    mid = left + (right - left) // 2
    if condition:
        right = mid
    else:
        left = mid + 1
```

**Use when:**
- Looking for boundary
- Finding first/last
- Need to converge to single element

---

## Key Insights

### Choosing Template

**`left <= right`:**
- Search terminates when left > right
- Returns -1 if not found
- Can return immediately

**`left < right`:**
- Search terminates when left == right
- Returns left (or right, they're equal)
- Used for finding boundaries

### Mid Calculation

```python
# Standard (avoids overflow)
mid = left + (right - left) // 2

# Alternative
mid = (left + right) // 2  # Can overflow in languages like Java/C++
```

### Update Rules

**Finding exact:**
- Found: return immediately
- Too small: `left = mid + 1`
- Too large: `right = mid - 1`

**Finding boundary:**
- Condition met: `right = mid` (might be answer)
- Condition not met: `left = mid + 1`

---

## Common Mistakes

❌ **Infinite loop**
```python
# BAD: Can loop forever
while left < right:
    mid = left + (right - left) // 2
    if condition:
        left = mid  # Should be mid + 1
```

❌ **Wrong initialization**
```python
# Check if right should be len(arr) - 1 or len(arr)
left, right = 0, len(arr) - 1  # Inclusive
left, right = 0, len(arr)      # Exclusive
```

❌ **Incorrect condition logic**
- Make sure condition correctly determines search direction

❌ **Not handling edge cases**
- Empty array
- Single element
- All same elements

---

## LeetCode Practice

### Easy
- #704: Binary Search
- #35: Search Insert Position
- #69: Sqrt(x)
- #374: Guess Number Higher or Lower

### Medium
- #33: Search in Rotated Sorted Array
- #34: Find First and Last Position
- #162: Find Peak Element
- #153: Find Minimum in Rotated Sorted Array
- #875: Koko Eating Bananas

### Hard
- #4: Median of Two Sorted Arrays
- #410: Split Array Largest Sum

---

**Remember:** Binary search is about eliminating half the search space each iteration by maintaining an invariant!
