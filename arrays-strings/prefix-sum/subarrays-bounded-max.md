# Number of Subarrays with Bounded Maximum — LC #795

**Pattern:** Prefix Counting / Two-Pass
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given array `nums` and integers `left` and `right`, return the number of contiguous subarrays where the maximum element is between `left` and `right` inclusive.

```
Input:  nums = [2, 1, 4, 3], left = 2, right = 3
Output: 3   // [2], [2,1], [3]
```

---

## Intuition

Count subarrays with max <= right, minus subarrays with max <= left-1. The difference gives subarrays with max in [left, right].

Helper: `count(nums, bound)` = number of subarrays where all elements <= bound. Use a running counter: reset when element > bound, else add current window length.

---

## Algorithm

1. `return count(nums, right) - count(nums, left - 1)`.
2. `count(nums, bound)`:
   - Set `result = 0`, `cur = 0`.
   - For each num: if `num <= bound` → `cur++` else `cur = 0`.
   - `result += cur`.
   - Return `result`.

---

## Code — Java

```java
public int numSubarrayBoundedMax(int[] nums, int left, int right) {
    return count(nums, right) - count(nums, left - 1);
}

private int count(int[] nums, int bound) {
    int result = 0, cur = 0;
    for (int num : nums) {
        cur = (num <= bound) ? cur + 1 : 0;
        result += cur;
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two linear passes |
| Space | O(1) | Only counters |

---

## Dry Run — [2, 1, 4, 3], left=2, right=3

count(bound=3):
- 2 ≤ 3: cur=1, result=1
- 1 ≤ 3: cur=2, result=3
- 4 > 3: cur=0, result=3
- 3 ≤ 3: cur=1, result=4 → total=4

count(bound=1):
- 2 > 1: cur=0, result=0
- 1 ≤ 1: cur=1, result=1
- 4 > 1: cur=0, result=1
- 3 > 1: cur=0, result=1 → total=1

**Result:** 4 - 1 = 3

---

## Edge Cases

- `left == 1` → `count(nums, left-1) = count(nums, 0)`. Any element ≥ 1 resets count, so only zeros contribute (usually 0).

---

## Common Mistakes

- Trying to directly count instead of using complement — direct counting is much harder.

---

## Related Problems

- **Subarray Sum Equals K (LC 560)** — prefix sum counting
- **Count Number of Nice Subarrays (LC 1248)** — similar complement counting
