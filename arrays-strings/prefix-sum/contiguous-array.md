# Contiguous Array — LC #525

**Pattern:** Prefix Sum + HashMap
**Difficulty:** Medium
**Companies:** Meta · Amazon · Google

---

## Problem

Given binary array `nums`, find the maximum length subarray with equal number of 0s and 1s.

```
Input:  [0, 1, 0]
Output: 2   // [0, 1] or [1, 0]

Input:  [0, 1, 0, 1]
Output: 4
```

---

## Intuition

Replace 0s with -1. Now the problem becomes: longest subarray with sum = 0. Use prefix sum + HashMap. If the same prefix sum appears at two indices, the subarray between them sums to 0 (equal 0s and 1s).

---

## Algorithm

1. Initialize `map = {0: -1}`.
2. Set `sum = 0`, `maxLen = 0`.
3. Loop `i` through `nums`:
   - `sum += nums[i] == 0 ? -1 : 1`.
   - If `sum` is in map → `maxLen = max(maxLen, i - map.get(sum))`.
   - Else → `map.put(sum, i)` (only first occurrence).
4. Return `maxLen`.

---

## Code — Java

```java
public int findMaxLength(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, -1);

    int sum = 0, maxLen = 0;

    for (int i = 0; i < nums.length; i++) {
        sum += (nums[i] == 0) ? -1 : 1;

        if (map.containsKey(sum)) {
            maxLen = Math.max(maxLen, i - map.get(sum));
        } else {
            map.put(sum, i);
        }
    }
    return maxLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(n) | HashMap |

---

## Dry Run — [0, 1, 0, 1]

| i | nums[i] | sum | map               | maxLen |
|---|---------|-----|-------------------|--------|
| — | —       | 0   | {0:-1}            | 0      |
| 0 | 0       | -1  | {0:-1,-1:0}       | 0      |
| 1 | 1       | 0   | seen at -1, len=2 | 2      |
| 2 | 0       | -1  | seen at 0, len=2  | 2      |
| 3 | 1       | 0   | seen at -1, len=4 | 4      |

**Result:** 4

---

## Edge Cases

- All zeros or all ones → no valid subarray, return 0.
- `[0, 1]` → return 2.

---

## Common Mistakes

- Storing latest index instead of first → gives wrong (shorter) max length.
- `map.put(0, 0)` instead of `map.put(0, -1)` → fails for subarray starting at index 0.

---

## Related Problems

- **Subarray Sum Equals K (LC 560)** — generalized version
- **Binary Subarrays With Sum (LC 930)** — count subarrays with sum = goal
