# Coin Change — LC #322

**Pattern:** 1D DP (Unbounded Knapsack)
**Difficulty:** Medium
**Companies:** Google · Amazon · Facebook · Microsoft

---

## Problem

Given coins and an amount, find the minimum number of coins to make that amount. Return -1 if impossible.

```
Input:  coins = [1,5,11], amount = 15
Output: 3   // 5+5+5
```

---

## Intuition

`dp[i]` = minimum coins to make amount `i`. Initialize to `amount+1` (infinity). `dp[0] = 0`. For each amount from 1 to target, try all coins. If `i - coin >= 0`, update `dp[i] = min(dp[i], dp[i-coin]+1)`.

---

## Code — Java

```java
public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1); // "infinity"
    dp[0] = 0;

    for (int i = 1; i <= amount; i++) {
        for (int coin : coins) {
            if (i - coin >= 0) {
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(amount * coins) |
| Space | O(amount) |

---

## Dry Run — coins=[1,5,11], amount=15

dp[0]=0, dp[1]=1, dp[2]=2, ..., dp[5]=1, ..., dp[10]=2, dp[11]=1, dp[15]=3 (5+5+5)

---

## Common Mistakes

- Initializing dp to `Integer.MAX_VALUE` — adding 1 causes overflow. Use `amount+1` instead.

---

## Related Problems

- **Coin Change II (LC 518)** — count number of ways
- **Climbing Stairs (LC 70)** — same bottom-up DP
