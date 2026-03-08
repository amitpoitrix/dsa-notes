# Counting Bits — LC #338

**Pattern:** DP + Bit Manipulation
**Difficulty:** Easy
**Companies:** Google · Amazon

---

## Problem

Given `n`, return array of length `n+1` where `ans[i]` = number of 1s in binary representation of `i`.

```
Input:  n = 5
Output: [0,1,1,2,1,2]
```

---

## Intuition

`dp[i] = dp[i >> 1] + (i & 1)`. Right shift removes the LSB — same bit count minus/plus that bit. `dp[i]` = bits in `i/2` + last bit of `i`.

---

## Code — Java

```java
public int[] countBits(int n) {
    int[] dp = new int[n + 1];
    for (int i = 1; i <= n; i++) {
        dp[i] = dp[i >> 1] + (i & 1);
    }
    return dp;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n) |
| Space | O(n) |

---

## Related Problems

- **Number of 1 Bits (LC 191)** — single number
- **Sum of Two Integers (LC 371)** — bit addition
