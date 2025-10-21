# Solution Template

Use this structure when providing complete solutions to ensure consistency and clarity.

**Note:** Adapt code examples to the user's preferred programming language.

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

**Language:** [User's chosen language - Python/JavaScript/Java/C++/Go/etc.]

```[language]
// Straightforward but inefficient approach
// Code in user's preferred language
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

<language-specific-examples>

**Python:**
```python
def optimal_solution(input_param):
    """
    Brief description of approach
    """
    # Initialize variables
    result = None

    # Main logic with comments
    # ...

    return result
```

**JavaScript:**
```javascript
function optimalSolution(inputParam) {
    // Brief description of approach

    // Initialize variables
    let result = null;

    // Main logic with comments
    // ...

    return result;
}
```

**Java:**
```java
class Solution {
    public ReturnType optimalSolution(InputType inputParam) {
        // Brief description of approach

        // Initialize variables
        ReturnType result = null;

        // Main logic with comments
        // ...

        return result;
    }
}
```

**C++:**
```cpp
class Solution {
public:
    ReturnType optimalSolution(InputType inputParam) {
        // Brief description of approach

        // Initialize variables
        ReturnType result;

        // Main logic with comments
        // ...

        return result;
    }
};
```

**Go:**
```go
func optimalSolution(inputParam InputType) ReturnType {
    // Brief description of approach

    // Initialize variables
    var result ReturnType

    // Main logic with comments
    // ...

    return result
}
```

</language-specific-examples>

**Provide code in user's preferred language. Include comments explaining each section.**

**Detailed Explanation:**

**Key components:**
- **Initialization:** [What and why]
- **Main logic:** [How the algorithm works]
- **Return:** [What we're returning]

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

**Format depends on language:**

**Python:**
```python
# Test 1: Basic case
assert solution([example]) == expected

# Test 2: Edge case
assert solution([edge_case]) == expected
```

**JavaScript:**
```javascript
// Test 1: Basic case
console.assert(solution([example]) === expected);

// Test 2: Edge case
console.assert(solution([edgeCase]) === expected);
```

**Java:**
```java
// Test 1: Basic case
assert solution(example).equals(expected);

// Test 2: Edge case
assert solution(edgeCase).equals(expected);
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
[Show trade-offs if space can be reduced]

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

## Language-Specific Notes

**Python:**
- Use list comprehensions for concise code
- `collections.defaultdict` and `Counter` are helpful
- Remember list slicing creates copies

**JavaScript:**
- Use `Map` and `Set` for better performance
- Array methods like `.map()`, `.filter()`, `.reduce()`
- Watch for type coercion

**Java:**
- Use `HashMap`, `HashSet`, `ArrayList`
- Watch for null pointer exceptions
- Consider using streams for cleaner code

**C++:**
- Use `unordered_map`, `unordered_set`, `vector`
- Watch for iterator invalidation
- Consider using STL algorithms

**Go:**
- Use maps and slices effectively
- No built-in set, use `map[Type]bool`
- Slices are references, be careful with modifications

---

**Remember:** Understanding WHY a solution works is more valuable than memorizing the code!
