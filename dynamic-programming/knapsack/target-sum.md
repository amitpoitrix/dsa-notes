# Target Sum — LC #494

**Pattern:** 0/1 Knapsack (Count Ways)
**Difficulty:** Medium
**Companies:** Facebook · Amazon · Google

---

## Problem

Given `nums` and `target`, assign `+` or `-` to each number. Count the number of ways to reach `target`.

```
Input:  nums = [1,1,1,1,1], target = 3
Output: 5
```

---

## Intuition

DFS/backtracking O(2ⁿ) works but slow. DP optimization: let `P` = sum of positive group, `N` = sum of negative group. `P - N = target`, `P + N = sum`. So `P = (sum + target) / 2`. Count subsets summing to `P`.

---

## Code — Java

```java
public int findTargetSumWays(int[] nums, int target) {
    int sum = 0;
    for (int n : nums) sum += n;
    if ((sum + target) % 2 != 0 || Math.abs(target) > sum) return 0;

    int t = (sum + target) / 2;
    int[] dp = new int[t + 1];
    dp[0] = 1;

    for (int num : nums) {
        for (int j = t; j >= num; j--) {
            dp[j] += dp[j - num];
        }
    }
    return dp[t];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n * target) |
| Space | O(target) |

---

## Related Problems

- **Partition Equal Subset Sum (LC 416)** — same knapsack base
- **Ones and Zeroes (LC 474)** — 2D knapsack
