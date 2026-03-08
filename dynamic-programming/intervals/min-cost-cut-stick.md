# Minimum Cost to Cut a Stick — LC #1547

**Pattern:** Interval DP
**Difficulty:** Hard
**Companies:** Google · Amazon

---

## Problem

Stick of length `n`. Given `cuts` positions, find minimum total cost to perform all cuts. Cost of each cut = length of stick being cut.

```
Input:  n = 7, cuts = [1,3,4,5]
Output: 16
```

---

## Intuition

Add 0 and n to cuts, sort. For each subinterval `[l, r]` (adjacent cuts), try every cut `m` in between as the first cut. Cost = `r - l + dp[l][m] + dp[m][r]`. Classic "optimal BST" style interval DP.

---

## Code — Java

```java
public int minCost(int n, int[] cuts) {
    int[] c = new int[cuts.length + 2];
    c[0] = 0; c[c.length-1] = n;
    for (int i = 0; i < cuts.length; i++) c[i+1] = cuts[i];
    Arrays.sort(c);
    int m = c.length;
    int[][] dp = new int[m][m];

    for (int len = 2; len < m; len++) {
        for (int l = 0; l < m - len; l++) {
            int r = l + len;
            dp[l][r] = Integer.MAX_VALUE;
            for (int mid = l+1; mid < r; mid++) {
                dp[l][r] = Math.min(dp[l][r], c[r]-c[l] + dp[l][mid] + dp[mid][r]);
            }
        }
    }
    return dp[0][m-1];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(m³) — m = cuts+2 |
| Space | O(m²) |

---

## Related Problems

- **Burst Balloons (LC 312)** — same interval DP structure
- **Strange Printer (LC 664)** — interval DP on strings
