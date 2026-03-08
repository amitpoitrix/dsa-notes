# Minimum Path Sum — LC #64

**Pattern:** 2D DP
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Given `m x n` grid with non-negative numbers, find path from top-left to bottom-right with minimum sum (can only move right or down).

```
Input:  [[1,3,1],[1,5,1],[4,2,1]]
Output: 7   // 1→3→1→1→1
```

---

## Code — Java

```java
public int minPathSum(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];
    dp[0][0] = grid[0][0];

    for (int r = 1; r < m; r++) dp[r][0] = dp[r-1][0] + grid[r][0];
    for (int c = 1; c < n; c++) dp[0][c] = dp[0][c-1] + grid[0][c];

    for (int r = 1; r < m; r++)
        for (int c = 1; c < n; c++)
            dp[r][c] = grid[r][c] + Math.min(dp[r-1][c], dp[r][c-1]);

    return dp[m-1][n-1];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(m*n) |
| Space | O(m*n) — can modify grid in-place for O(1) |

---

## Related Problems

- **Unique Paths (LC 62)** — count paths
- **Triangle (LC 120)** — triangle grid, bottom-up DP
