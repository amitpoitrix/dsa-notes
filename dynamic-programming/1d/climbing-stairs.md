# Climbing Stairs — LC #70

**Pattern:** 1D DP (Fibonacci variant)
**Difficulty:** Easy
**Companies:** Amazon · Google · Adobe

---

## Problem

You can climb 1 or 2 steps at a time. Given `n` steps, how many distinct ways to reach the top?

```
Input:  n = 4
Output: 5   // 1+1+1+1, 1+1+2, 1+2+1, 2+1+1, 2+2
```

---

## Intuition

`dp[i]` = ways to reach step `i` = ways from step `i-1` (take 1 step) + ways from step `i-2` (take 2 steps). This is exactly Fibonacci. Optimize space to O(1) with two variables.

---

## Code — Java

```java
public int climbStairs(int n) {
    if (n <= 2) return n;
    int prev2 = 1, prev1 = 2;
    for (int i = 3; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n) |
| Space | O(1) |

---

## Related Problems

- **House Robber (LC 198)** — same DP structure
- **Fibonacci Number (LC 509)** — exactly this
- **Min Cost Climbing Stairs (LC 746)** — add costs
