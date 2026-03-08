# Longest Common Subsequence — LC #1143

**Pattern:** 2D DP (LCS)
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Given two strings, return the length of their longest common subsequence (characters don't need to be contiguous).

```
Input:  text1 = "abcde", text2 = "ace"
Output: 3   // "ace"
```

---

## Intuition

`dp[i][j]` = LCS of `text1[0..i-1]` and `text2[0..j-1]`.
- If `text1[i-1] == text2[j-1]`: `dp[i][j] = dp[i-1][j-1] + 1`.
- Else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.

---

## Code — Java

```java
public int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length(), n = text2.length();
    int[][] dp = new int[m + 1][n + 1];

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1.charAt(i-1) == text2.charAt(j-1)) {
                dp[i][j] = dp[i-1][j-1] + 1;
            } else {
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
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
| Space | O(m*n) — optimizable to O(n) |

---

## Related Problems

- **Edit Distance (LC 72)** — LCS variant with ops
- **Shortest Common Supersequence (LC 1092)** — build from LCS
- **Longest Common Substring** — must be contiguous (different DP)
