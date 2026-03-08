# Max Consecutive Ones III — LC #1004

**Pattern:** Sliding Window (Variable)
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Given binary array `nums` and integer `k`, return the maximum number of consecutive 1s if you can flip at most `k` zeros.

```
Input:  nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6   // flip two zeros at index 4,5 → [1,1,1,0,1,1,1,1,1,1,0] → 6 consecutive
```

---

## Intuition

The window can contain at most `k` zeros. Expand R freely. When zero count exceeds `k`, shrink from L until we've dropped a zero. Track max window size.

---

## Algorithm

1. Set `L = 0`, `zeros = 0`, `maxLen = 0`.
2. Loop R from 0 to n-1:
   - If `nums[R] == 0` → `zeros++`.
   - While `zeros > k` → if `nums[L] == 0`: `zeros--`. `L++`.
   - Update `maxLen = max(maxLen, R - L + 1)`.
3. Return `maxLen`.

---

## Code — Java

```java
public int longestOnes(int[] nums, int k) {
    int L = 0, zeros = 0, maxLen = 0;

    for (int R = 0; R < nums.length; R++) {
        if (nums[R] == 0) zeros++;

        while (zeros > k) {
            if (nums[L] == 0) zeros--;
            L++;
        }
        maxLen = Math.max(maxLen, R - L + 1);
    }
    return maxLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each element processed at most twice |
| Space | O(1) | Only counters |

---

## Dry Run — [1,1,1,0,0,0,1,1,1,1,0], k = 2

| R | nums[R] | zeros | L | window len |
|---|---------|-------|---|------------|
| 3 | 0       | 1     | 0 | 4          |
| 4 | 0       | 2     | 0 | 5          |
| 5 | 0       | 3→shrink | 4 (skip zeros until zeros=2) | 2 |
| 6-9 | 1s    | 2     | 4 | 6          |
| 10 | 0      | 3→shrink | 6 | 5          |

**Result:** 6

---

## Edge Cases

- `k == 0` → longest run of 1s with no flips.
- All zeros, `k >= n` → return n.
- All ones → return n.

---

## Common Mistakes

- Using `if` instead of `while` to shrink — need to keep shrinking until zeros ≤ k.

---

## Related Problems

- **Max Consecutive Ones (LC 485)** — k = 0 version
- **Longest Substring with At Most K Distinct (LC 340)** — same variable window pattern
- **Fruits Into Baskets (LC 904)** — same pattern, different domain
