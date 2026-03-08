# Split Array Largest Sum — LC #410

**Pattern:** Binary Search on Answer Space
**Difficulty:** Hard
**Companies:** Google · Amazon

---

## Problem

Given array `nums` and integer `k`, split into `k` non-empty subarrays to minimize the largest subarray sum.

```
Input:  nums = [7,2,5,10,8], k = 2
Output: 18   // [7,2,5] and [10,8], max sum = 18
```

---

## Intuition

Binary search on the answer (the max sum). Range: `max(nums)` to `sum(nums)`. For a given max sum, greedily check if we can split into at most `k` groups.

---

## Code — Java

```java
public int splitArray(int[] nums, int k) {
    int L = Arrays.stream(nums).max().getAsInt();
    int R = Arrays.stream(nums).sum();

    while (L < R) {
        int mid = L + (R - L) / 2;
        if (canSplit(nums, k, mid)) R = mid;
        else L = mid + 1;
    }
    return L;
}

private boolean canSplit(int[] nums, int k, int maxSum) {
    int groups = 1, sum = 0;
    for (int n : nums) {
        if (sum + n > maxSum) {
            groups++;
            sum = 0;
        }
        sum += n;
    }
    return groups <= k;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log S) | S = sum of nums |
| Space | O(1)       | |

---

## Related Problems

- **Koko Eating Bananas (LC 875)** — same pattern
- **Capacity to Ship Packages (LC 1011)** — same pattern
