# Product of Array Except Self — LC #238

**Pattern:** Prefix Product (Left and Right Pass)
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given array `nums`, return array `answer` where `answer[i]` is the product of all elements except `nums[i]`. No division. O(n) time, O(1) extra space.

```
Input:  [1, 2, 3, 4]
Output: [24, 12, 8, 6]
```

---

## Intuition

For each index `i`: `answer[i] = product of all elements left of i * product of all elements right of i`.

Do two passes: left-to-right builds prefix products, right-to-left multiplies in suffix products. Use the output array itself to store prefix, saving O(1) extra space.

---

## Algorithm

1. Initialize `result[0] = 1`. Loop left to right: `result[i] = result[i-1] * nums[i-1]`.
2. Set `suffix = 1`. Loop right to left: `result[i] *= suffix`, then `suffix *= nums[i]`.
3. Return `result`.

---

## Code — Java

```java
public int[] productExceptSelf(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];

    // left pass: result[i] = product of all elements to the left of i
    result[0] = 1;
    for (int i = 1; i < n; i++) {
        result[i] = result[i - 1] * nums[i - 1];
    }

    // right pass: multiply in product of all elements to the right of i
    int suffix = 1;
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= suffix;
        suffix *= nums[i];
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two passes |
| Space | O(1) | Output array doesn't count as extra space |

---

## Dry Run — [1, 2, 3, 4]

Left pass (prefix):
| i | result[i] (left product) |
|---|--------------------------|
| 0 | 1                        |
| 1 | 1                        |
| 2 | 2                        |
| 3 | 6                        |

Right pass (multiply suffix):
| i | suffix before | result[i] | suffix after |
|---|---------------|-----------|--------------|
| 3 | 1             | 6         | 4            |
| 2 | 4             | 8         | 12           |
| 1 | 12            | 12        | 24           |
| 0 | 24            | 24        | 24           |

**Result:** [24, 12, 8, 6]

---

## Edge Cases

- Array contains zeros: if one zero → all positions except the zero's position become 0. If two zeros → entire result is zeros.
- The algorithm handles zeros naturally without special casing.

---

## Common Mistakes

- Using division `totalProduct / nums[i]` — doesn't work when zeros are present.
- Creating a separate suffix array — wastes O(n) space; use a running variable instead.

---

## Related Problems

- **Subarray Sum Equals K (LC 560)** — prefix sum variant
- **Trapping Rain Water (LC 42)** — left/right pass idea
