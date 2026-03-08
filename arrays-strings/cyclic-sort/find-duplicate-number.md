# Find the Duplicate Number — LC #287

**Pattern:** Floyd's Cycle Detection
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Problem

Given array of `n+1` integers where each value is in `[1, n]`, find the duplicate. Must not modify array, O(1) space.

```
Input:  [1, 3, 4, 2, 2]
Output: 2
```

---

## Intuition

Treat array as a linked list where `nums[i]` points to `nums[nums[i]]`. A duplicate creates a cycle. Use Floyd's cycle detection (fast/slow pointer) to find the cycle entry point.

---

## Algorithm

1. Phase 1: Find intersection point inside cycle.
   - slow = nums[slow], fast = nums[nums[fast]].
2. Phase 2: Find cycle entry (the duplicate).
   - Reset slow to start. Move both one step. They meet at the duplicate.

---

## Code — Java

```java
public int findDuplicate(int[] nums) {
    int slow = nums[0], fast = nums[0];

    // phase 1: find intersection
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);

    // phase 2: find cycle entry
    slow = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Floyd's algorithm |
| Space | O(1) | No extra DS |

---

## Common Mistakes

- Starting both pointers at index 0 without doing `nums[0]` first — the "linked list" starts at `nums[0]` not index 0.

---

## Related Problems

- **Linked List Cycle II (LC 142)** — same Floyd's cycle detection
- **Find All Duplicates (LC 442)** — multiple duplicates
