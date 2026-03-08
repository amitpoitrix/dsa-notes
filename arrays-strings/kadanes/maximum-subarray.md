# Maximum Subarray — LC #53

**Pattern:** Kadane's Algorithm
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given array `nums`, find the contiguous subarray with the largest sum and return its sum.

```
Input:  [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6   // [4, -1, 2, 1]
```

---

## Intuition

At each position, decide: extend the current subarray or start fresh. If the running sum becomes negative, it's a liability — reset to 0 (start fresh from next element). Track the maximum seen.

---

## Code — Java

```java
public int maxSubArray(int[] nums) {
    int maxSum = nums[0];
    int current = nums[0];

    for (int i = 1; i < nums.length; i++) {
        current = Math.max(nums[i], current + nums[i]);
        maxSum = Math.max(maxSum, current);
    }
    return maxSum;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | |

---

## Dry Run — [-2,1,-3,4,-1,2,1,-5,4]

| i | nums[i] | current        | maxSum |
|---|---------|----------------|--------|
| 0 | -2      | -2             | -2     |
| 1 | 1       | max(1,-1)=1    | 1      |
| 2 | -3      | max(-3,-2)=-2  | 1      |
| 3 | 4       | max(4,2)=4     | 4      |
| 4 | -1      | max(-1,3)=3    | 4      |
| 5 | 2       | max(2,5)=5     | 5      |
| 6 | 1       | max(1,6)=6     | 6      |
| 7 | -5      | max(-5,1)=1    | 6      |
| 8 | 4       | max(4,5)=5     | 6      |

**Result:** 6

---

## Edge Cases

- All negatives → return the maximum single element (initialize with nums[0], not 0).

---

## Common Mistakes

- Initializing `maxSum = 0` — fails when all elements are negative.

---

## Related Problems

- **Maximum Product Subarray (LC 152)** — same idea but track min and max
- **Best Time to Buy and Sell Stock (LC 121)** — Kadane variant
- **Maximum Sum Circular Subarray (LC 918)** — wrap-around variant
