# Unique Paths — LC #62

**Pattern:** 2D DP (Grid)
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Robot starts at top-left of `m x n` grid, wants to reach bottom-right. Can only move right or down. Count unique paths.

```
Input:  m = 3, n = 7
Output: 28
```

---

## Intuition

`dp[r][c]` = number of ways to reach cell `(r,c)` = `dp[r-1][c]` (came from above) + `dp[r][c-1]` (came from left). First row and column = 1 (only one way to reach them).

---

## Code — Java

```java
public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for (int r = 0; r < m; r++) dp[r][0] = 1;
    for (int c = 0; c < n; c++) dp[0][c] = 1;

    for (int r = 1; r < m; r++)
        for (int c = 1; c < n; c++)
            dp[r][c] = dp[r-1][c] + dp[r][c-1];

    return dp[m-1][n-1];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(m*n) |
| Space | O(m*n) — optimizable to O(n) |

---

## Related Problems

- **Unique Paths II (LC 63)** — with obstacles
- **Minimum Path Sum (LC 64)** — minimize sum along path
