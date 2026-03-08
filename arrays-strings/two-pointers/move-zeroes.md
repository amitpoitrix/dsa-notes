# Move Zeroes — LC #283

**Pattern:** Two Pointers (Slow / Fast)
**Difficulty:** Easy
**Companies:** Meta · Amazon · Microsoft · Bloomberg

---

## Problem

Given array `nums`, move all `0`s to the end while maintaining the relative order of non-zero elements. Do it **in-place**.

```
Input:  [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]

Input:  [0, 0, 1]
Output: [1, 0, 0]
```

---

## Intuition

Use a slow pointer `k` to track the next position for a non-zero element. Fast pointer `i` scans the array. When `nums[i] != 0`, place it at `nums[k]` and advance `k`. After the loop, fill remaining positions with 0.

---

## Algorithm

1. Set `k = 0`.
2. Loop `i` from 0 to n-1:
   - If `nums[i] != 0` → `nums[k] = nums[i]`, `k++`.
3. Loop from `k` to n-1: `nums[k] = 0`.

---

## Code — Java

```java
public void moveZeroes(int[] nums) {
    int k = 0;

    // move all non-zeroes to the front
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != 0) {
            nums[k] = nums[i];
            k++;
        }
    }

    // fill rest with zeroes
    while (k < nums.length) {
        nums[k] = 0;
        k++;
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two passes, both O(n) |
| Space | O(1) | In-place |

---

## Dry Run — [0, 1, 0, 3, 12]

Pass 1 (collect non-zeros):

| i | nums[i] | k before | Action | k after |
|---|---------|----------|--------|---------|
| 0 | 0       | 0        | skip   | 0       |
| 1 | 1       | 0        | nums[0]=1 | 1   |
| 2 | 0       | 1        | skip   | 1       |
| 3 | 3       | 1        | nums[1]=3 | 2   |
| 4 | 12      | 2        | nums[2]=12 | 3  |

Array after pass 1: `[1, 3, 12, 3, 12]` (tail doesn't matter yet)

Pass 2 (fill zeros from k=3): `[1, 3, 12, 0, 0]`

**Result:** `[1, 3, 12, 0, 0]`

---

## Edge Cases

- **No zeros** `[1, 2, 3]` → unchanged.
- **All zeros** `[0, 0, 0]` → `[0, 0, 0]` (zeroed out again).
- **Zero at end** `[1, 2, 0]` → `[1, 2, 0]`, unchanged.

---

## Common Mistakes

- Swapping instead of overwriting — swapping works too but does more writes. Overwrite + fill zeros is cleaner.
- Forgetting the second pass to fill zeros — non-zero elements are placed but old values remain in the tail.

---

## Related Problems

- **Remove Duplicates from Sorted Array (LC 26)** — same slow/fast pointer pattern
- **Remove Element (LC 27)** — same idea, remove a specific value
- **Sort Colors (LC 75)** — 3-way partition, extension of this pattern
