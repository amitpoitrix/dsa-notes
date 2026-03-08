# 132 Pattern — LC #456

**Pattern:** Monotonic Decreasing Stack
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given array `nums`, check if there exists `i < j < k` such that `nums[i] < nums[k] < nums[j]` (a "132 pattern").

```
Input:  [3, 1, 4, 2]
Output: true   // 1 < 2 < 4
```

---

## Intuition

Traverse right to left. Use a decreasing stack. Maintain `k` (the "2" — third element) as the largest value popped from the stack so far. For each element, check if it's less than `k` (found the "1").

---

## Code — Java

```java
public boolean find132pattern(int[] nums) {
    Deque<Integer> stack = new ArrayDeque<>(); // candidates for "3" (middle)
    int k = Integer.MIN_VALUE; // the "2" (third element, between 1 and 3)

    for (int i = nums.length - 1; i >= 0; i--) {
        if (nums[i] < k) return true; // found "1" less than "2"
        while (!stack.isEmpty() && nums[i] > stack.peek()) {
            k = stack.pop(); // pop smaller "2" candidates, update k
        }
        stack.push(nums[i]);
    }
    return false;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(n) | Stack |

---

## Common Mistakes

- Traversing left to right — the right-to-left traversal is key to this approach.
