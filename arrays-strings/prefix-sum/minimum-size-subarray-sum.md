# Minimum Size Subarray Sum — LC #209

**Pattern:** Sliding Window (Variable)
**Difficulty:** Medium
**Companies:** Amazon · Microsoft · Google

---

## Problem

Given array `nums` of positive integers and `target`, find the minimum length contiguous subarray whose sum >= target. Return 0 if none.

```
Input:  target = 7, nums = [2, 3, 1, 2, 4, 3]
Output: 2   // [4, 3]
```

---

## Intuition

Expand R to grow sum. Once `sum >= target`, try to shrink from L to find the smallest valid window. Keep doing this greedily.

---

## Algorithm

1. Set `L = 0`, `sum = 0`, `minLen = Integer.MAX_VALUE`.
2. Loop R from 0 to n-1:
   - `sum += nums[R]`.
   - While `sum >= target`:
     - `minLen = min(minLen, R - L + 1)`.
     - `sum -= nums[L++]`.
3. Return `minLen == MAX_VALUE ? 0 : minLen`.

---

## Code — Java

```java
public int minSubArrayLen(int target, int[] nums) {
    int L = 0, sum = 0, minLen = Integer.MAX_VALUE;

    for (int R = 0; R < nums.length; R++) {
        sum += nums[R];
        while (sum >= target) {
            minLen = Math.min(minLen, R - L + 1);
            sum -= nums[L++];
        }
    }
    return minLen == Integer.MAX_VALUE ? 0 : minLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each element added and removed once |
| Space | O(1) | Only counters |

---

## Dry Run — [2, 3, 1, 2, 4, 3], target = 7

| R | sum  | action                   | minLen |
|---|------|--------------------------|--------|
| 0 | 2    | < 7                      | MAX    |
| 1 | 5    | < 7                      | MAX    |
| 2 | 6    | < 7                      | MAX    |
| 3 | 8    | ≥7 → shrink: 8-2=6, L=1  | 4      |
| 4 | 10   | ≥7 → shrink: 10-3=7, L=2 | 4      |
|   | 7    | ≥7 → shrink: 7-1=6, L=3  | 3      |
| 5 | 9    | ≥7 → shrink: 9-2=7, L=4  | 3      |
|   | 7    | ≥7 → shrink: 7-4=3, L=5  | 2      |

**Result:** 2

---

## Edge Cases

- Sum of entire array < target → return 0.
- Single element >= target → return 1.
- Only works with positive numbers (for negative, need prefix sum + deque).

---

## Common Mistakes

- Using `sum > target` instead of `sum >= target`.
- Returning -1 instead of 0.

---

## Related Problems

- **Maximum Sum Subarray of Size K** — fixed window version
- **Subarray Sum Equals K (LC 560)** — exact sum, needs HashMap (has negatives)
