# Maximum Product Subarray — LC #152

**Pattern:** Kadane's (Track Min and Max)
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta · Microsoft

---

## Problem

Given array `nums`, find the contiguous subarray with the largest product and return it.

```
Input:  [2, 3, -2, 4]
Output: 6   // [2, 3]

Input:  [-2, 0, -1]
Output: 0
```

---

## Intuition

Unlike sum, a negative × negative = positive, so the minimum product can suddenly become the maximum. Track both `maxProd` and `minProd` at each step.

---

## Code — Java

```java
public int maxProduct(int[] nums) {
    int maxProd = nums[0], minProd = nums[0], result = nums[0];

    for (int i = 1; i < nums.length; i++) {
        int temp = maxProd;
        maxProd = Math.max(nums[i], Math.max(maxProd * nums[i], minProd * nums[i]));
        minProd = Math.min(nums[i], Math.min(temp * nums[i], minProd * nums[i]));
        result = Math.max(result, maxProd);
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | |

---

## Dry Run — [2, 3, -2, 4]

| i | nums[i] | maxProd | minProd | result |
|---|---------|---------|---------|--------|
| 0 | 2       | 2       | 2       | 2      |
| 1 | 3       | 6       | 3       | 6      |
| 2 | -2      | -2      | -12     | 6      |
| 3 | 4       | -8      | -48     | 6      |

**Result:** 6

---

## Edge Cases

- Zeros reset both min and max to the current element.
- Single negative → returns that negative (least bad).

---

## Common Mistakes

- Not saving `temp = maxProd` before updating — minProd computation needs the old maxProd.

---

## Related Problems

- **Maximum Subarray (LC 53)** — sum version (simpler)
