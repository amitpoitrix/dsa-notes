# Edit Distance — LC #72

**Pattern:** 2D DP (LCS variant)
**Difficulty:** Hard
**Companies:** Google · Amazon · Microsoft · LinkedIn

---

## Problem

Given two strings, find minimum operations (insert, delete, replace) to convert `word1` to `word2`.

```
Input:  word1 = "horse", word2 = "ros"
Output: 3
```

---

## Intuition

`dp[i][j]` = min ops to convert `word1[0..i-1]` to `word2[0..j-1]`.
- If chars match: `dp[i][j] = dp[i-1][j-1]` (no op needed).
- Else: `dp[i][j] = 1 + min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1])`.
  - `dp[i-1][j-1]` = replace, `dp[i-1][j]` = delete, `dp[i][j-1]` = insert.

---

## Code — Java

```java
public int minDistance(String word1, String word2) {
    int m = word1.length(), n = word2.length();
    int[][] dp = new int[m + 1][n + 1];

    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (word1.charAt(i-1) == word2.charAt(j-1)) {
                dp[i][j] = dp[i-1][j-1];
            } else {
                dp[i][j] = 1 + Math.min(dp[i-1][j-1], Math.min(dp[i-1][j], dp[i][j-1]));
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
| Time  | O(m*n) |
| Space | O(m*n) |

---

## Dry Run — "horse" → "ros"

Base: dp[i][0]=i, dp[0][j]=j. Fill table cell by cell, final dp[5][3]=3.

---

## Common Mistakes

- Forgetting to initialize base cases (empty string conversions).

---

## Related Problems

- **Longest Common Subsequence (LC 1143)** — related structure
- **Minimum ASCII Delete Sum (LC 712)** — delete only version
