# Two Pointers Pattern 🔀

## When to Use

Use Two Pointers when you have:
- **Sorted array or linked list**
- Need to find pairs/triplets with specific properties
- Processing elements from both ends
- Removing duplicates in-place
- Detecting cycles (fast & slow variant)

## Core Variations

### 1. Opposite Directions (Most Common)
Start from both ends, move toward middle.

**Use cases:**
- Finding pairs that sum to target
- Palindrome checking
- Trapping water problems
- Container with most water

**Template:**
```python
def two_pointer_opposite(arr, target):
    left, right = 0, len(arr) - 1

    while left < right:
        current_sum = arr[left] + arr[right]

        if current_sum == target:
            return [left, right]  # Found answer
        elif current_sum < target:
            left += 1  # Need larger sum
        else:
            right -= 1  # Need smaller sum

    return [-1, -1]  # Not found
```

**Time:** O(n)
**Space:** O(1)

---

### 2. Same Direction (Fast & Slow)
Both pointers move forward, but at different speeds.

**Use cases:**
- Removing duplicates in-place
- Moving zeros to end
- Partition arrays
- Removing elements

**Template:**
```python
def two_pointer_same_direction(arr):
    slow = 0  # Position to place next valid element

    for fast in range(len(arr)):
        if is_valid(arr[fast]):  # Your condition here
            arr[slow] = arr[fast]
            slow += 1

    return slow  # New length or position
```

**Time:** O(n)
**Space:** O(1)

---

### 3. Cycle Detection (Floyd's Tortoise & Hare)
One slow pointer, one fast pointer (2x speed).

**Use cases:**
- Linked list cycle detection
- Find cycle start
- Find duplicate number
- Happy number

**Template:**
```python
def has_cycle(head):
    slow = fast = head

    while fast and fast.next:
        slow = slow.next          # Move 1 step
        fast = fast.next.next     # Move 2 steps

        if slow == fast:
            return True  # Cycle detected

    return False  # No cycle

def find_cycle_start(head):
    # First detect cycle
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break

    if not fast or not fast.next:
        return None  # No cycle

    # Find start of cycle
    slow = head
    while slow != fast:
        slow = slow.next
        fast = fast.next

    return slow
```

**Time:** O(n)
**Space:** O(1)

---

## Common Problem Patterns

### Pattern 1: Find Pair with Target Sum
```python
# Two Sum II (sorted array)
def twoSum(numbers, target):
    left, right = 0, len(numbers) - 1

    while left < right:
        current = numbers[left] + numbers[right]

        if current == target:
            return [left + 1, right + 1]  # 1-indexed
        elif current < target:
            left += 1
        else:
            right -= 1

    return []
```

**LeetCode Examples:**
- #167: Two Sum II
- #15: 3Sum
- #16: 3Sum Closest

---

### Pattern 2: Palindrome Check
```python
def isPalindrome(s):
    left, right = 0, len(s) - 1

    while left < right:
        # Skip non-alphanumeric
        while left < right and not s[left].isalnum():
            left += 1
        while left < right and not s[right].isalnum():
            right -= 1

        if s[left].lower() != s[right].lower():
            return False

        left += 1
        right -= 1

    return True
```

**LeetCode Examples:**
- #125: Valid Palindrome
- #680: Valid Palindrome II

---

### Pattern 3: Remove Duplicates In-Place
```python
def removeDuplicates(nums):
    if not nums:
        return 0

    slow = 1  # Position for next unique element

    for fast in range(1, len(nums)):
        if nums[fast] != nums[fast - 1]:
            nums[slow] = nums[fast]
            slow += 1

    return slow
```

**LeetCode Examples:**
- #26: Remove Duplicates from Sorted Array
- #80: Remove Duplicates from Sorted Array II
- #283: Move Zeroes

---

### Pattern 4: Container With Most Water
```python
def maxArea(height):
    left, right = 0, len(height) - 1
    max_area = 0

    while left < right:
        width = right - left
        current_area = min(height[left], height[right]) * width
        max_area = max(max_area, current_area)

        # Move pointer with smaller height
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1

    return max_area
```

**LeetCode Examples:**
- #11: Container With Most Water
- #42: Trapping Rain Water

---

## Key Insights

### When to Move Which Pointer?

**Opposite Direction:**
- If sum too small → move left (increase)
- If sum too large → move right (decrease)
- If comparing values → move the pointer at smaller value

**Same Direction:**
- Fast pointer always moves
- Slow pointer only moves when condition met

**Cycle Detection:**
- Fast always moves 2 steps
- Slow always moves 1 step

### Common Mistakes

❌ **Forgetting sorted requirement**
- Two pointers (opposite) only works on sorted data
- Sort first if needed!

❌ **Wrong pointer movement**
- Make sure you're moving the right pointer

❌ **Not handling edge cases**
- Empty array
- Single element
- All same elements

❌ **Off-by-one errors**
- `left < right` vs `left <= right`
- Be careful with boundaries

### Complexity Analysis

**Time Complexity:** Almost always O(n)
- Each pointer moves through array once
- No nested loops despite while loop

**Space Complexity:** O(1)
- Only using two pointer variables
- In-place modifications

## Practice Problems

### Beginner
- #167: Two Sum II - Input Array Is Sorted
- #125: Valid Palindrome
- #283: Move Zeroes

### Intermediate
- #15: 3Sum
- #11: Container With Most Water
- #26: Remove Duplicates from Sorted Array
- #141: Linked List Cycle

### Advanced
- #42: Trapping Rain Water
- #923: 3Sum With Multiplicity
- #287: Find the Duplicate Number

## Quick Decision Tree

```
Two Pointers?
    ↓
Is array sorted?
    ↓ YES → Opposite direction (find pairs/triplets)
    ↓ NO → Can you sort it? Or use same direction

Need to process from both ends?
    ↓ YES → Opposite direction

Need to partition/filter in-place?
    ↓ YES → Same direction (fast & slow)

Linked list cycle?
    ↓ YES → Fast & slow (Floyd's)
```

## Template Selection Guide

| Problem Type | Template |
|--------------|----------|
| Find pair sum in sorted array | Opposite Direction |
| Remove elements in-place | Same Direction |
| Palindrome check | Opposite Direction |
| Cycle detection | Fast & Slow |
| Partition array | Same Direction |
| 3Sum, 4Sum | Opposite Direction (with outer loop) |

---

**Remember:** Two pointers is about efficiently using two positions to avoid nested loops, reducing O(n²) to O(n)!
