# Regular Expression Matching — LC #10

**Pattern:** 2D DP
**Difficulty:** Hard
**Companies:** Google · Facebook · Uber

---

## Problem

Implement regex matching with `.` (matches any single char) and `*` (matches 0 or more of preceding element).

```
Input:  s = "aab", p = "c*a*b"
Output: true
```

---

## Intuition

`dp[i][j]` = does `p[0..j-1]` match `s[0..i-1]`.
- `p[j-1] == '*'`: zero occurrences `dp[i][j-2]` OR one more if prev char matches `dp[i-1][j]`.
- `p[j-1] == '.'` or match: `dp[i][j] = dp[i-1][j-1]`.

---

## Code — Java

```java
public boolean isMatch(String s, String p) {
    int m = s.length(), n = p.length();
    boolean[][] dp = new boolean[m + 1][n + 1];
    dp[0][0] = true;

    for (int j = 2; j <= n; j += 2)
        if (p.charAt(j-1) == '*') dp[0][j] = dp[0][j-2];

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (p.charAt(j-1) == '*') {
                dp[i][j] = dp[i][j-2]; // zero of preceding
                if (p.charAt(j-2) == '.' || p.charAt(j-2) == s.charAt(i-1))
                    dp[i][j] = dp[i][j] || dp[i-1][j]; // one more
            } else if (p.charAt(j-1) == '.' || p.charAt(j-1) == s.charAt(i-1)) {
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

## Common Mistakes

- Confusing with wildcard matching — here `*` means "0 or more of PRECEDING char", not "any sequence".

---

## Related Problems

- **Wildcard Matching (LC 44)** — `*` matches any sequence directly
