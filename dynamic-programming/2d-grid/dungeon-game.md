# Dungeon Game — LC #174

**Pattern:** 2D DP (Reverse / Bottom-up)
**Difficulty:** Hard
**Companies:** Amazon · Google

---

## Problem

Knight starts at top-left, needs to reach bottom-right. Each cell has a value (negative = lose health, positive = gain). Find minimum initial health needed (always ≥ 1).

---

## Intuition

Work backwards from destination. `dp[r][c]` = minimum health needed when entering cell `(r,c)` to survive from there to destination. At each cell: health needed = `max(1, min(down, right) - dungeon[r][c])`. Need at least 1 health entering any cell.

---

## Code — Java

```java
public int calculateMinimumHP(int[][] dungeon) {
    int m = dungeon.length, n = dungeon[0].length;
    int[][] dp = new int[m + 1][n + 1];
    // init with high values; right and bottom borders = 1
    for (int[] row : dp) Arrays.fill(row, Integer.MAX_VALUE);
    dp[m][n-1] = dp[m-1][n] = 1;

    for (int r = m - 1; r >= 0; r--) {
        for (int c = n - 1; c >= 0; c--) {
            int need = Math.min(dp[r+1][c], dp[r][c+1]) - dungeon[r][c];
            dp[r][c] = Math.max(1, need);
        }
    }
    return dp[0][0];
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

- Going forward instead of backward — can't know minimum health going forward because you don't know future cells yet.

---

## Related Problems

- **Minimum Path Sum (LC 64)** — forward DP on grid
- **Triangle (LC 120)** — bottom-up path DP
