# Maximum Sum Circular Subarray — LC #918

**Pattern:** Kadane's + Total Sum Trick
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given circular array `nums`, return the maximum sum of a non-empty subarray (can wrap around).

```
Input:  [1, -2, 3, -2]
Output: 3   // [3]

Input:  [5, -3, 5]
Output: 10  // [5, 5] wrapping around
```

---

## Intuition

Two cases:
1. Max subarray does NOT wrap → standard Kadane's.
2. Max subarray WRAPS → equals `total - min subarray` (the elements NOT in the subarray form the minimum middle part).

Answer = max(maxSubarray, total - minSubarray). Special case: if all elements negative, return maxSubarray (not total - minSubarray, which would be 0).

---

## Code — Java

```java
public int maxSubarraySumCircular(int[] nums) {
    int maxSum = nums[0], minSum = nums[0];
    int curMax = nums[0], curMin = nums[0];
    int total = nums[0];

    for (int i = 1; i < nums.length; i++) {
        curMax = Math.max(nums[i], curMax + nums[i]);
        maxSum = Math.max(maxSum, curMax);

        curMin = Math.min(nums[i], curMin + nums[i]);
        minSum = Math.min(minSum, curMin);

        total += nums[i];
    }

    return maxSum > 0 ? Math.max(maxSum, total - minSum) : maxSum;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | |

---

## Edge Cases

- All negatives: `maxSum < 0` → return `maxSum` directly (total - minSum = 0 which is wrong).

---

## Common Mistakes

- Forgetting the all-negatives edge case — `total - minSum` gives 0 but 0 isn't a valid subarray answer if the array is non-empty with all negatives.
