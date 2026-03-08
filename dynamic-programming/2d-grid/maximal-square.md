# Maximal Square — LC #221

**Pattern:** 2D DP
**Difficulty:** Medium
**Companies:** Facebook · Amazon · Airbnb

---

## Problem

Given binary matrix, find the largest square containing only `'1'`s and return its area.

```
Input:  [["1","0","1","1","1"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4
```

---

## Intuition

`dp[r][c]` = side length of largest square with bottom-right corner at `(r,c)`. If `matrix[r][c] == '1'`:  
`dp[r][c] = min(dp[r-1][c], dp[r][c-1], dp[r-1][c-1]) + 1`.

The minimum of the three neighbors is the bottleneck — the square can only extend as far as the smallest adjacent square allows.

---

## Code — Java

```java
public int maximalSquare(char[][] matrix) {
    int m = matrix.length, n = matrix[0].length, max = 0;
    int[][] dp = new int[m + 1][n + 1];

    for (int r = 1; r <= m; r++) {
        for (int c = 1; c <= n; c++) {
            if (matrix[r-1][c-1] == '1') {
                dp[r][c] = Math.min(dp[r-1][c], Math.min(dp[r][c-1], dp[r-1][c-1])) + 1;
                max = Math.max(max, dp[r][c]);
            }
        }
    }
    return max * max;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(m*n) |
| Space | O(m*n) |

---

## Common Mistakes

- Returning `max` instead of `max*max` — the problem asks for area, not side length.

---

## Related Problems

- **Maximal Rectangle (LC 85)** — largest rectangle in histogram per row
- **Count Square Submatrices (LC 1277)** — count all valid squares
