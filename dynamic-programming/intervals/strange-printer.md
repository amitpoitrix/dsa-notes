# Strange Printer — LC #664

**Pattern:** Interval DP
**Difficulty:** Hard
**Companies:** Google

---

## Problem

A printer can print a sequence of same characters in one turn and can overwrite previous characters. Given string `s`, find minimum turns to print it.

```
Input:  s = "aaabbb"
Output: 2

Input:  s = "aba"
Output: 2
```

---

## Intuition

`dp[i][j]` = min turns to print `s[i..j]`. Base: `dp[i][i] = 1`. For each interval, try splitting at all points. Key optimization: if `s[i] == s[k]` for some `k` in `[i+1, j]`, we can print `s[i]` as part of printing `s[k]`, saving one turn: `dp[i][j] = min(dp[i][j], dp[i+1][k] + dp[k+1][j])` when `s[i]==s[k]`.

---

## Code — Java

```java
public int strangePrinter(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];

    for (int i = n-1; i >= 0; i--) {
        dp[i][i] = 1;
        for (int j = i+1; j < n; j++) {
            dp[i][j] = dp[i+1][j] + 1; // print s[i] alone + rest
            for (int k = i+1; k <= j; k++) {
                if (s.charAt(k) == s.charAt(i)) {
                    dp[i][j] = Math.min(dp[i][j],
                        (k+1 <= j ? dp[k+1][j] : 0) + dp[i+1][k]);
                }
            }
        }
    }
    return dp[0][n-1];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n³) |
| Space | O(n²) |

---

## Related Problems

- **Burst Balloons (LC 312)** — interval DP
- **Palindrome Partitioning II (LC 132)** — interval DP
