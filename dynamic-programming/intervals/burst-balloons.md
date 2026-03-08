# Burst Balloons — LC #312

**Pattern:** Interval DP
**Difficulty:** Hard
**Companies:** Google · Amazon

---

## Problem

Given `n` balloons each with a number, bursting balloon `i` gives `nums[i-1] * nums[i] * nums[i+1]` coins. Find max coins to burst all balloons.

```
Input:  nums = [3,1,5,8]
Output: 167   // 3*1*5 + 3*5*8 + 1*3*8 + 1*8*1
```

---

## Intuition

Think in reverse: instead of which balloon to burst first, think which to burst LAST in each subinterval `[l, r]`. If `k` is the last balloon in `[l, r]`: coins = `nums[l-1] * nums[k] * nums[r+1] + dp[l][k-1] + dp[k+1][r]`. Add padding (1s) at both ends.

---

## Code — Java

```java
public int maxCoins(int[] nums) {
    int n = nums.length;
    int[] arr = new int[n + 2];
    arr[0] = arr[n + 1] = 1;
    for (int i = 0; i < n; i++) arr[i + 1] = nums[i];

    int[][] dp = new int[n + 2][n + 2];

    for (int len = 1; len <= n; len++) {
        for (int l = 1; l <= n - len + 1; l++) {
            int r = l + len - 1;
            for (int k = l; k <= r; k++) {
                dp[l][r] = Math.max(dp[l][r],
                    dp[l][k-1] + arr[l-1]*arr[k]*arr[r+1] + dp[k+1][r]);
            }
        }
    }
    return dp[1][n];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n³) |
| Space | O(n²) |

---

## Key Insight

Think of the last balloon burst in each interval, not the first. This removes the dependency problem (what's adjacent changes as you burst).

---

## Related Problems

- **Strange Printer (LC 664)** — interval DP
- **Minimum Cost to Cut a Stick (LC 1547)** — interval DP
