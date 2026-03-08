# Distinct Subsequences — LC #115

**Pattern:** 2D DP
**Difficulty:** Hard
**Companies:** Google · Facebook

---

## Problem

Given strings `s` and `t`, count distinct subsequences of `s` that equal `t`.

```
Input:  s = "rabbbit", t = "rabbit"
Output: 3
```

---

## Intuition

`dp[i][j]` = ways to form `t[0..j-1]` using `s[0..i-1]`.
- If `s[i-1] == t[j-1]`: `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]` (use this match OR skip it).
- Else: `dp[i][j] = dp[i-1][j]` (skip current s char).

---

## Code — Java

```java
public int numDistinct(String s, String t) {
    int m = s.length(), n = t.length();
    int[][] dp = new int[m + 1][n + 1];
    for (int i = 0; i <= m; i++) dp[i][0] = 1; // empty t matched in 1 way

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            dp[i][j] = dp[i-1][j]; // skip s[i-1]
            if (s.charAt(i-1) == t.charAt(j-1))
                dp[i][j] += dp[i-1][j-1];
        }
    }
    return dp[m][n];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(m*n) |
| Space | O(m*n) |

---

## Related Problems

- **Longest Common Subsequence (LC 1143)** — find length
- **Edit Distance (LC 72)** — allow ops
