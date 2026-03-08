# 3Sum Closest — LC #16

**Pattern:** Sort + Two Pointers
**Difficulty:** Medium
**Companies:** Amazon · Bloomberg · Facebook

---

## Problem

Given array `nums` and integer `target`, find three integers whose sum is closest to `target`. Return the sum.

```
Input:  nums = [-1, 2, 1, -4], target = 1
Output: 2    // -1 + 2 + 1 = 2, closest to 1
```

---

## Intuition

Same structure as 3Sum — sort + fix one element + two pointers. The only difference: instead of looking for exact sum = 0, we track the minimum absolute difference from target and update our best answer as we go.

---

## Algorithm

1. Sort the array.
2. Initialize `closest = nums[0] + nums[1] + nums[2]`.
3. Loop `i` from 0 to n-3:
   - Skip duplicate `i` values.
   - Set `L = i+1`, `R = n-1`. While `L < R`:
     - Compute `sum = nums[i] + nums[L] + nums[R]`.
     - If `|sum - target| < |closest - target|` → update `closest = sum`.
     - If `sum == target` → return immediately (can't get closer).
     - If `sum < target` → `L++`.
     - If `sum > target` → `R--`.
4. Return `closest`.

---

## Code — Java

```java
public int threeSumClosest(int[] nums, int target) {
    Arrays.sort(nums);
    int closest = nums[0] + nums[1] + nums[2];

    for (int i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue; // skip duplicate i

        int L = i + 1, R = nums.length - 1;

        while (L < R) {
            int sum = nums[i] + nums[L] + nums[R];

            if (Math.abs(sum - target) < Math.abs(closest - target)) {
                closest = sum;
            }

            if (sum == target) {
                return sum; // exact match, can't do better
            } else if (sum < target) {
                L++;
            } else {
                R--;
            }
        }
    }
    return closest;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n²) | Sort O(n log n) + outer × two-pointer O(n²) |
| Space | O(1)  | No extra data structures |

---

## Dry Run — [-4, -1, 1, 2], target = 1

| i   | L  | R | sum | closest | Action |
|-----|----|---|-----|---------|--------|
| -4  | -1 | 2 | -3  | -3      | L++ (sum < 1) |
| -4  | 1  | 2 | -1  | -1      | L++ (sum < 1) |
| -1  | 1  | 2 | 2 ✓ | 2       | return 2 (closest) |

**Result:** 2

---

## Edge Cases

- **Exact match exists** → early return as soon as `sum == target`.
- **All same elements** `[1, 1, 1], target = 3` → returns 3.
- **Target very large or very small** → still works, closest tracks the best seen.

---

## Common Mistakes

- Forgetting the early return when `sum == target` — not a bug but a missed optimization.
- Initializing `closest` to 0 or `Integer.MAX_VALUE` instead of an actual triplet sum — causes wrong diff calculation.

---

## Related Problems

- **3Sum (LC 15)** — exact version of this problem (target = 0)
- **3Sum Smaller (LC 259)** — count triplets with sum < target
- **Two Sum II (LC 167)** — base two-pointer pattern
