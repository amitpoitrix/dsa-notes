# Maximum Sum Subarray of Size K

**Pattern:** Sliding Window (Fixed)
**Difficulty:** Easy
**Companies:** Amazon · Microsoft

---

## Problem

Given an array `nums` and integer `k`, find the maximum sum of any contiguous subarray of size `k`.

```
Input:  nums = [2, 1, 5, 1, 3, 2], k = 3
Output: 9   // [5, 1, 3]
```

---

## Intuition

Brute force checks every window of size k → O(n*k). Instead, maintain a running window sum. When the window exceeds size k, subtract the element going out from the left. This gives O(n).

---

## Algorithm

1. Compute sum of first `k` elements. Set `maxSum = windowSum`.
2. Loop `i` from `k` to `n-1`:
   - Add `nums[i]`, subtract `nums[i - k]`.
   - Update `maxSum`.
3. Return `maxSum`.

---

## Code — Java

```java
public int maxSumSubarray(int[] nums, int k) {
    int windowSum = 0;
    for (int i = 0; i < k; i++) windowSum += nums[i];

    int maxSum = windowSum;

    for (int i = k; i < nums.length; i++) {
        windowSum += nums[i] - nums[i - k];
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | No extra DS |

---

## Dry Run — [2, 1, 5, 1, 3, 2], k = 3

| i | add    | remove | windowSum | maxSum |
|---|--------|--------|-----------|--------|
| — | init   | —      | 8 (2+1+5) | 8      |
| 3 | 1      | 2      | 7         | 8      |
| 4 | 3      | 1      | 9         | 9      |
| 5 | 2      | 5      | 6         | 9      |

**Result:** 9

---

## Edge Cases

- `k == n` → entire array is the window, return total sum.
- All negatives → still returns the least negative window of size k.

---

## Common Mistakes

- Off-by-one: subtract `nums[i - k]` not `nums[i - k - 1]`.
- Forgetting to initialize `maxSum` before the sliding loop.

---

## Related Problems

- **Longest Substring Without Repeating Characters (LC 3)** — variable window version
- **Minimum Size Subarray Sum (LC 209)** — variable window, find min length
