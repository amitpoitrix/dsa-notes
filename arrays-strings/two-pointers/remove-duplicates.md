# Remove Duplicates from Sorted Array — LC #26

**Pattern:** Two Pointers (Slow / Fast)
**Difficulty:** Easy
**Companies:** Amazon · Microsoft · Adobe

---

## Problem

Given a sorted array `nums`, remove duplicates **in-place** so each element appears only once. Return the count `k` of unique elements. The first `k` elements of `nums` should hold the result.

```
Input:  nums = [1, 1, 2]
Output: 2, nums = [1, 2, _]

Input:  nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]
Output: 5, nums = [0, 1, 2, 3, 4, _, _, _, _, _]
```

---

## Intuition

Use a slow pointer `k` to track where the next unique element should go, and a fast pointer `i` to scan ahead. When `nums[i]` differs from `nums[k-1]` (last placed unique), copy it to `nums[k]` and advance `k`.

---

## Algorithm

1. If array is empty, return 0.
2. Set `k = 1` (first element is always unique).
3. Loop `i` from 1 to n-1:
   - If `nums[i] != nums[i - 1]` → `nums[k] = nums[i]`, `k++`.
4. Return `k`.

---

## Code — Java

```java
public int removeDuplicates(int[] nums) {
    int k = 1;

    for (int i = 1; i < nums.length; i++) {
        if (nums[i] != nums[i - 1]) {
            nums[k] = nums[i];
            k++;
        }
    }
    return k;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | In-place, no extra array |

---

## Dry Run — [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]

| i | nums[i] | nums[i-1] | Same? | k | Array (first k) |
|---|---------|-----------|-------|---|-----------------|
| 1 | 0       | 0         | yes   | 1 | [0] |
| 2 | 1       | 0         | no    | 2 | [0, 1] |
| 3 | 1       | 1         | yes   | 2 | [0, 1] |
| 4 | 1       | 1         | yes   | 2 | [0, 1] |
| 5 | 2       | 1         | no    | 3 | [0, 1, 2] |
| 6 | 2       | 2         | yes   | 3 | [0, 1, 2] |
| 7 | 3       | 2         | no    | 4 | [0, 1, 2, 3] |
| 8 | 3       | 3         | yes   | 4 | [0, 1, 2, 3] |
| 9 | 4       | 3         | no    | 5 | [0, 1, 2, 3, 4] |

**Result:** k = 5

---

## Edge Cases

- **All same** `[1, 1, 1]` → k = 1, `nums = [1, _, _]`.
- **All unique** `[1, 2, 3]` → k = 3, array unchanged.
- **Single element** `[5]` → k = 1.

---

## Common Mistakes

- Starting `k = 0` and `i = 0` instead of `k = 1`, `i = 1` — leads to off-by-one, first element gets overwritten.
- Comparing `nums[i]` with `nums[k]` instead of `nums[k-1]` — both work but knowing why matters.

---

## Variants

- **Remove Duplicates II (LC 80)** — allow each element at most twice. Change condition to `nums[i] != nums[k-2]`.
- **Remove Element (LC 27)** — remove all occurrences of a given value in-place.

---

## Related Problems

- **Move Zeroes (LC 283)** — same slow/fast pointer pattern
- **Remove Element (LC 27)** — direct variant
- **Remove Duplicates II (LC 80)** — allow up to 2 duplicates
