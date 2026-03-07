# 3Sum — LC #15

**Pattern:** Sort + Two Pointers
**Difficulty:** Medium
**Companies:** Google · Meta · Amazon

---

## Problem

Given array `nums`, return all unique triplets `[a, b, c]` such that `a + b + c = 0`. No duplicate triplets in output.

```
Input:  [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]
```

---

## Intuition

Brute force = 3 nested loops → O(n³). We can do better.

**Key idea:** Sort the array. Fix one element `nums[i]`, then find two numbers in the remaining sorted subarray that sum to `-nums[i]`. That inner search is Two Sum on a sorted array → O(n) with two pointers.

Sort O(n log n) + outer loop × two-pointer O(n) = **O(n²) total.**

---

## Algorithm

1. Sort the array.
2. Loop `i` from 0 to n-3. If `nums[i] > 0`, break (all remaining are positive, no triplet possible).
3. Skip duplicates for `i` — if `nums[i] == nums[i-1]`, continue.
4. Set `L = i+1`, `R = n-1`. Run two-pointer while `L < R`:
   - `sum == 0` → add triplet, skip dups for L and R, then L++, R--
   - `sum < 0`  → L++ (need bigger value)
   - `sum > 0`  → R-- (need smaller value)

---

## Code — Java

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);

    for (int i = 0; i < nums.length - 2; i++) {
        if (nums[i] > 0) break;                        // all positive from here, stop
        if (i > 0 && nums[i] == nums[i - 1]) continue; // skip duplicate i

        int L = i + 1, R = nums.length - 1;

        while (L < R) {
            int sum = nums[i] + nums[L] + nums[R];

            if (sum == 0) {
                result.add(Arrays.asList(nums[i], nums[L], nums[R]));
                while (L < R && nums[L] == nums[L + 1]) L++; // skip duplicate L
                while (L < R && nums[R] == nums[R - 1]) R--; // skip duplicate R
                L++; R--;
            } else if (sum < 0) {
                L++;
            } else {
                R--;
            }
        }
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n²) | Sort O(n log n) + outer × two-pointer O(n²) |
| Space | O(1)  | In-place sort, no extra DS (excluding output) |

---

## Dry Run — [-4, -1, -1, 0, 1, 2]

| i  | L  | R | Sum | Action              |
|----|----|---|-----|---------------------|
| -4 | -1 | 2 | -3  | L++                 |
| -1 | -1 | 2 | 0 ✓ | add [-1,-1,2], L++, R-- |
| -1 | 0  | 1 | 0 ✓ | add [-1,0,1], L++, R--  |
| -1 (idx 2) | — | — | — | skip, dup of idx 1  |
| 0  | 1  | 2 | 3   | R--                 |
| 0  | 1  | 1 | —   | L == R, stop        |

**Result:** [[-1, -1, 2], [-1, 0, 1]]

---

## Edge Cases

- `[0, 0, 0]` → `[[0,0,0]]`. Dup-skip after finding triplet handles it.
- All positive / all negative → early break when `nums[i] > 0`.
- Many duplicates like `[-2,0,0,2,2]` → only `[[-2,0,2]]`. Both inner dup-skips needed.
- No valid triplet → returns empty list naturally.

---

## Common Mistakes

- Using `break` instead of `continue` for the duplicate-i skip.
- Missing `L < R` guard inside inner dup-skip while loops → ArrayIndexOutOfBounds.
- Forgetting `L++` and `R--` after adding triplet → infinite loop.
- Not sorting first — entire approach only works on a sorted array.

---

## Related Problems

- **Two Sum II (LC 167)** — simpler warm-up, the exact base pattern
- **3Sum Closest (LC 16)** — same structure, track min diff instead of exact match
- **4Sum (LC 18)** — one more outer loop on top of this, O(n³)
