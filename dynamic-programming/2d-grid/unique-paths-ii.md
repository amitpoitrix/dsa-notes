# Unique Paths II — LC #63

**Pattern:** 2D DP (Grid with obstacles)
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Same as Unique Paths but grid has obstacles (`1`). Can't pass through obstacles.

```
Input:  [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
```

---

## Code — Java

```java
public int uniquePathsWithObstacles(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    if (grid[0][0] == 1) return 0;
    int[][] dp = new int[m][n];
    dp[0][0] = 1;

    for (int r = 1; r < m; r++) dp[r][0] = grid[r][0] == 1 ? 0 : dp[r-1][0];
    for (int c = 1; c < n; c++) dp[0][c] = grid[0][c] == 1 ? 0 : dp[0][c-1];

    for (int r = 1; r < m; r++)
        for (int c = 1; c < n; c++)
            dp[r][c] = grid[r][c] == 1 ? 0 : dp[r-1][c] + dp[r][c-1];

    return dp[m-1][n-1];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(m*n) |
| Space | O(m*n) |

---

## Edge Cases

- Start or end is an obstacle → return 0.

---

## Related Problems

- **Unique Paths (LC 62)** — no obstacles
- **Minimum Path Sum (LC 64)** — minimize cost
