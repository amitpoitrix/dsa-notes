# Ones and Zeroes — LC #474

**Pattern:** 2D Knapsack
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given array of binary strings `strs` and integers `m` (max 0s) and `n` (max 1s), find the largest subset where total 0s ≤ m and total 1s ≤ n.

```
Input:  strs = ["10","0001","111001","1","0"], m=5, n=3
Output: 4
```

---

## Intuition

2D knapsack. `dp[i][j]` = max strings using at most `i` zeros and `j` ones. For each string, iterate backwards on both dimensions.

---

## Code — Java

```java
public int findMaxForm(String[] strs, int m, int n) {
    int[][] dp = new int[m + 1][n + 1];

    for (String s : strs) {
        int zeros = 0, ones = 0;
        for (char c : s.toCharArray()) {
            if (c == '0') zeros++; else ones++;
        }
        for (int i = m; i >= zeros; i--) {
            for (int j = n; j >= ones; j--) {
                dp[i][j] = Math.max(dp[i][j], dp[i-zeros][j-ones] + 1);
            }
        }
    }
    return dp[m][n];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(L * m * n) — L = total string length |
| Space | O(m * n) |

---

## Related Problems

- **Partition Equal Subset Sum (LC 416)** — 1D knapsack
- **Coin Change II (LC 518)** — unbounded knapsack
