# First Missing Positive — LC #41

**Pattern:** Cyclic Sort / Index Placement
**Difficulty:** Hard
**Companies:** Amazon · Google · Meta · Microsoft

---

## Problem

Given unsorted array, find the smallest missing positive integer. O(n) time, O(1) space.

```
Input:  [3, 4, -1, 1]
Output: 2

Input:  [1, 2, 0]
Output: 3
```

---

## Intuition

Place each number `nums[i]` in its "correct" position: `nums[i] - 1`. After placement, the first index where `nums[i] != i + 1` gives the missing positive.

---

## Algorithm

1. For each `i`, while `nums[i]` is in range `[1, n]` and not in correct position (`nums[nums[i]-1] != nums[i]`): swap to correct position.
2. Scan: first `i` where `nums[i] != i + 1` → return `i + 1`.
3. If all correct → return `n + 1`.

---

## Code — Java

```java
public int firstMissingPositive(int[] nums) {
    int n = nums.length;

    // place each number in its correct position
    for (int i = 0; i < n; i++) {
        while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
            int correct = nums[i] - 1;
            int temp = nums[correct];
            nums[correct] = nums[i];
            nums[i] = temp;
        }
    }

    // find first position where number is wrong
    for (int i = 0; i < n; i++) {
        if (nums[i] != i + 1) return i + 1;
    }
    return n + 1;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each element placed at most once |
| Space | O(1) | In-place |

---

## Dry Run — [3, 4, -1, 1]

After cyclic sort: nums becomes [1, -1, 3, 4]
- Index 0: nums[0]=1 ✓
- Index 1: nums[1]=-1 ✗ → missing is 2

**Result:** 2

---

## Common Mistakes

- Not checking `nums[nums[i]-1] != nums[i]` before swapping — causes infinite loop on duplicates.

---

## Related Problems

- **Missing Number (LC 268)** — range [0, n], no negatives
- **Find All Duplicates (LC 442)** — find duplicates using same index trick
