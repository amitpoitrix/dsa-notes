# Palindrome Partitioning II — LC #132

**Pattern:** DP (Interval + 1D)
**Difficulty:** Hard
**Companies:** Amazon · Google

---

## Problem

Given string `s`, return minimum cuts to partition it into palindrome substrings.

```
Input:  s = "aab"
Output: 1   // "aa" | "b"
```

---

## Intuition

Precompute palindrome table `isPalin[i][j]`. Then `dp[i]` = min cuts for `s[0..i]`. For each `i`, for each `j <= i`: if `s[j..i]` is palindrome, `dp[i] = min(dp[i], (j == 0 ? 0 : dp[j-1]+1))`.

---

## Code — Java

```java
public int minCut(String s) {
    int n = s.length();
    boolean[][] isPalin = new boolean[n][n];

    for (int i = n-1; i >= 0; i--) {
        for (int j = i; j < n; j++) {
            if (s.charAt(i) == s.charAt(j) && (j - i <= 2 || isPalin[i+1][j-1]))
                isPalin[i][j] = true;
        }
    }

    int[] dp = new int[n];
    Arrays.fill(dp, Integer.MAX_VALUE);
    for (int i = 0; i < n; i++) {
        if (isPalin[0][i]) { dp[i] = 0; continue; }
        for (int j = 1; j <= i; j++) {
            if (isPalin[j][i] && dp[j-1] != Integer.MAX_VALUE)
                dp[i] = Math.min(dp[i], dp[j-1] + 1);
        }
    }
    return dp[n-1];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n²) |
| Space | O(n²) |

---

## Related Problems

- **Palindrome Partitioning (LC 131)** — return all partitions
- **Burst Balloons (LC 312)** — interval DP
