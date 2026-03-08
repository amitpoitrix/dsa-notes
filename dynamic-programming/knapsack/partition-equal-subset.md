# Partition Equal Subset Sum — LC #416

**Pattern:** 0/1 Knapsack
**Difficulty:** Medium
**Companies:** Amazon · Facebook · Google

---

## Problem

Given array `nums`, determine if it can be partitioned into two subsets with equal sum.

```
Input:  nums = [1,5,11,5]
Output: true   // [1,5,5] and [11]
```

---

## Intuition

If total sum is odd → impossible. Otherwise find if any subset sums to `total/2`. Classic 0/1 knapsack: `dp[j]` = can we form sum `j` using some elements. For each number, update dp backwards.

---

## Code — Java

```java
public boolean canPartition(int[] nums) {
    int sum = 0;
    for (int n : nums) sum += n;
    if (sum % 2 != 0) return false;

    int target = sum / 2;
    boolean[] dp = new boolean[target + 1];
    dp[0] = true;

    for (int num : nums) {
        for (int j = target; j >= num; j--) { // backwards to avoid reuse
            dp[j] = dp[j] || dp[j - num];
        }
    }
    return dp[target];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n * target) |
| Space | O(target) |

---

## Key Insight

Iterate `j` backwards to ensure each element used at most once (0/1 knapsack). Forwards iteration = unbounded knapsack.

---

## Related Problems

- **Subset Sum** — classic version of this
- **Target Sum (LC 494)** — count ways to assign + and -
- **Last Stone Weight II (LC 1049)** — minimize difference of two partitions
