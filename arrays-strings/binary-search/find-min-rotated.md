# Find Minimum in Rotated Sorted Array — LC #153

**Pattern:** Binary Search (Modified)
**Difficulty:** Medium
**Companies:** Amazon · Microsoft · Google

---

## Problem

Given rotated sorted array `nums` with no duplicates, find the minimum element.

```
Input:  nums = [3, 4, 5, 1, 2]
Output: 1
```

---

## Intuition

The minimum is at the rotation point. If `nums[mid] > nums[R]`, the minimum is in the right half. Otherwise it's in the left half (including mid).

---

## Code — Java

```java
public int findMin(int[] nums) {
    int L = 0, R = nums.length - 1;

    while (L < R) {
        int mid = L + (R - L) / 2;
        if (nums[mid] > nums[R]) L = mid + 1; // min is in right half
        else R = mid;                          // min is at mid or left
    }
    return nums[L];
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(log n) | |
| Space | O(1)     | |

---

## Key Insight

Compare `nums[mid]` with `nums[R]` (not nums[L]). If mid > R, rotation happened in the right, so min is right of mid. If mid <= R, min is at mid or left.

---

## Common Mistakes

- Comparing with `nums[L]` instead of `nums[R]` — leads to wrong logic.
- Using `L <= R` instead of `L < R` — causes infinite loop since we set `R = mid` not `R = mid-1`.
