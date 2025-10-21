# Solution Template

Use this structure when providing complete solutions to ensure consistency and clarity.

---

## Problem: [Problem Name]

**LeetCode #XXX** | **Difficulty:** [Easy/Medium/Hard]

### Problem Statement
[Concise restatement of the problem in plain English]

### Examples
```
Input: [example input]
Output: [example output]
Explanation: [why]

Input: [edge case]
Output: [output]
```

### Constraints
- [Constraint 1]
- [Constraint 2]
- [Important bounds]

---

## Approach

### Pattern Identification
**Pattern:** [Pattern Name - e.g., Two Pointers, Sliding Window, DP]

**Why this pattern fits:**
- [Reason 1]
- [Reason 2]

### Key Insight
[The "aha!" moment that makes this problem click]

### Algorithm Strategy
1. [High-level step 1]
2. [High-level step 2]
3. [High-level step 3]

---

## Solution

### Approach 1: [Brute Force / Naive]

**Idea:** [Simplest approach, even if inefficient]

```python
def solution_brute_force(input):
    # Straightforward but inefficient approach
    pass
```

**Time Complexity:** O(?)
**Space Complexity:** O(?)

**Why this works:**
- [Explanation]

**Why it's not optimal:**
- [Bottleneck explanation]

---

### Approach 2: [Optimized Solution]

**Idea:** [How we improve on brute force]

**Walkthrough with Example:**
```
Input: [specific example]

Step 1: [What happens]
State: [show variables]

Step 2: [What happens]
State: [show variables]

Step 3: [What happens]
State: [show variables]

Output: [result]
```

**Code:**
```python
def optimal_solution(input):
    """
    Brief description of approach
    """
    # Initialize variables
    result = None

    # Main logic with comments
    # ...

    return result
```

**Detailed Explanation:**

**Line-by-line breakdown:**
- `Line X`: [What it does and why]
- `Line Y`: [What it does and why]

**Why this is optimal:**
- [Explanation of why this is the best approach]

---

## Complexity Analysis

### Time Complexity: O(?)

**Breakdown:**
- [Operation 1]: O(?)
- [Operation 2]: O(?)
- **Total:** O(?)

**Explanation:**
[Detailed reasoning for why this complexity]

### Space Complexity: O(?)

**Breakdown:**
- [Structure 1]: O(?)
- [Structure 2]: O(?)
- **Total:** O(?)

**Explanation:**
[What auxiliary space is used]

---

## Edge Cases & Testing

### Edge Cases to Consider
1. **Empty input:** `[]` or `""` → Expected: [result]
2. **Single element:** `[x]` → Expected: [result]
3. **All same elements:** `[1,1,1]` → Expected: [result]
4. **Maximum size:** [large input] → Should handle efficiently
5. **[Problem-specific edge case]:** → Expected: [result]

### Test Cases
```python
# Test 1: Basic case
input = [example]
expected = [output]
assert solution(input) == expected

# Test 2: Edge case
input = [edge case]
expected = [output]
assert solution(input) == expected

# Test 3: Maximum constraint
input = [max case]
expected = [output]
assert solution(input) == expected
```

---

## Alternative Approaches

### Approach 3: [Alternative Method]

**Idea:** [Different way to solve]

**Pros:**
- [Advantage 1]
- [Advantage 2]

**Cons:**
- [Disadvantage 1]
- [Disadvantage 2]

**When to use:** [Scenarios where this might be preferred]

---

## Optimization Opportunities

### Current Solution
- Time: O(?)
- Space: O(?)

### Can we do better?

**Time optimization:**
- [If possible, how to reduce time]
- [Or, why current time is optimal]

**Space optimization:**
```python
def space_optimized_solution(input):
    # Space-optimized version
    # Trade time for space or vice versa
    pass
```

**Trade-offs:**
- [What we gain vs what we sacrifice]

---

## Common Mistakes to Avoid

❌ **Mistake 1:** [Common error]
- **Why it's wrong:** [Explanation]
- **Correct approach:** [Fix]

❌ **Mistake 2:** [Common error]
- **Why it's wrong:** [Explanation]
- **Correct approach:** [Fix]

❌ **Mistake 3:** [Off-by-one, wrong initialization, etc.]
- **Why it's wrong:** [Explanation]
- **Correct approach:** [Fix]

---

## Interview Discussion Points

### If interviewer asks:
**"Can you optimize further?"**
- Response: [Analysis of current optimality]

**"What if input was [modified constraint]?"**
- Response: [How approach would change]

**"How would you test this?"**
- Response: [Testing strategy]

**"What's the bottleneck?"**
- Response: [Identify computational bottleneck]

### Follow-up variations
- [Variation 1]: [How approach changes]
- [Variation 2]: [How approach changes]

---

## Similar Problems

Practice these related problems:
- **LeetCode #XXX:** [Problem name] - [Why similar]
- **LeetCode #YYY:** [Problem name] - [Why similar]
- **LeetCode #ZZZ:** [Problem name] - [Why similar]

---

## Key Takeaways

1. **Pattern:** This is a [pattern] problem
2. **Recognition:** Look for [signals] to identify this pattern
3. **Technique:** Use [data structure/algorithm] for efficiency
4. **Pitfall:** Watch out for [common mistake]
5. **Next time:** When you see [characteristic], think [approach]

---

## Complete Code (Production-Ready)

```python
def solution(input_param):
    """
    [Problem description in one line]

    Args:
        input_param: [Description and type]

    Returns:
        [Return type and description]

    Time Complexity: O(?)
    Space Complexity: O(?)
    """
    # Input validation
    if not input_param:
        return [edge case result]

    # Initialize
    result = None

    # Main algorithm
    # [Clean, well-commented code]

    return result


# Example usage
if __name__ == "__main__":
    # Test cases
    test_cases = [
        ([input1], expected1),
        ([input2], expected2),
        ([input3], expected3),
    ]

    for i, (input_val, expected) in enumerate(test_cases):
        result = solution(input_val)
        status = "✓" if result == expected else "✗"
        print(f"Test {i+1}: {status} Expected: {expected}, Got: {result}")
```

---

**Remember:** Understanding WHY a solution works is more valuable than memorizing the code!
