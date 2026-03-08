# Subarray with Zero Sum

**Pattern:** Prefix Sum + HashSet
**Difficulty:** Easy
**Companies:** Amazon · Microsoft

---

## Problem

Given array `nums`, check if there is a subarray with sum = 0. Return true/false.

```
Input:  [4, 2, -3, 1, 6]
Output: true   // [2, -3, 1] = 0
```

---

## Intuition

If the same prefix sum appears twice, the subarray between those two indices sums to 0. Use a HashSet. Initialize with 0 (handles subarrays starting at index 0).

---

## Code — Java

```java
public boolean hasZeroSumSubarray(int[] nums) {
    Set<Integer> seen = new HashSet<>();
    seen.add(0);
    int sum = 0;

    for (int num : nums) {
        sum += num;
        if (seen.contains(sum)) return true;
        seen.add(sum);
    }
    return false;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(n) | HashSet |

---

## Related Problems

- **Subarray Sum Equals K (LC 560)** — generalized to any target k
- **Contiguous Array (LC 525)** — equal 0s and 1s (special case of this)
