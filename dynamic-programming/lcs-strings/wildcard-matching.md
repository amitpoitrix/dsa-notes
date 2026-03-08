# Wildcard Matching — LC #44

**Pattern:** 2D DP
**Difficulty:** Hard
**Companies:** Facebook · Amazon · Google

---

## Problem

Given string `s` and pattern `p` with `?` (matches any single char) and `*` (matches any sequence including empty), return if pattern matches entire string.

```
Input:  s = "adceb", p = "*a*b"
Output: true
```

---

## Intuition

`dp[i][j]` = does `p[0..j-1]` match `s[0..i-1]`.
- `p[j-1] == '*'`: matches empty (`dp[i][j-1]`) or matches one more char in s (`dp[i-1][j]`).
- `p[j-1] == '?'` or chars match: `dp[i][j] = dp[i-1][j-1]`.

---

## Code — Java

```java
public boolean isMatch(String s, String p) {
    int m = s.length(), n = p.length();
    boolean[][] dp = new boolean[m + 1][n + 1];
    dp[0][0] = true;

    for (int j = 1; j <= n; j++)
        dp[0][j] = dp[0][j-1] && p.charAt(j-1) == '*';

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (p.charAt(j-1) == '*') {
                dp[i][j] = dp[i][j-1] || dp[i-1][j]; // empty or one more
            } else if (p.charAt(j-1) == '?' || s.charAt(i-1) == p.charAt(j-1)) {
                dp[i][j] = dp[i-1][j-1];
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

## Related Problems

- **Regular Expression Matching (LC 10)** — `.` and `*` (harder, `*` means 0+ of preceding)
