# Longest Increasing Subsequence — LC #300

**Pattern:** DP / Binary Search (Patience Sort)
**Difficulty:** Medium
**Companies:** Microsoft · Amazon · Google

---

## Problem

Given array `nums`, return length of the longest strictly increasing subsequence.

```
Input:  nums = [10,9,2,5,3,7,101,18]
Output: 4   // [2,3,7,101]
```

---

## Intuition

**DP O(n²):** `dp[i]` = LIS ending at index `i`. For each `j < i`, if `nums[j] < nums[i]`, update `dp[i] = max(dp[i], dp[j]+1)`.

**Binary Search O(n log n):** Maintain a `tails` array where `tails[i]` is the smallest tail element of all increasing subsequences of length `i+1`. For each number, binary search for its position in tails and replace/extend.

---

## Code — Java (O(n log n))

```java
public int lengthOfLIS(int[] nums) {
    List<Integer> tails = new ArrayList<>();

    for (int num : nums) {
        int lo = 0, hi = tails.size();
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (tails.get(mid) < num) lo = mid + 1;
            else hi = mid;
        }
        if (lo == tails.size()) tails.add(num);
        else tails.set(lo, num);
    }
    return tails.size();
}
```

---

## Complexity

| Approach | Time | Space |
|---|---|---|
| DP | O(n²) | O(n) |
| Binary Search | O(n log n) | O(n) |

---

## Key Insight

`tails` doesn't store a real subsequence — it stores the optimal "patience sort" state. Its length = LIS length.

---

## Related Problems

- **Russian Doll Envelopes (LC 354)** — 2D LIS
- **Increasing Triplet Subsequence (LC 334)** — just check if length ≥ 3
- **Longest Bitonic Subsequence** — LIS from both ends
