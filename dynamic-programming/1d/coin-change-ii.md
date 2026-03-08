# Coin Change II — LC #518

**Pattern:** 1D DP (Unbounded Knapsack — Count Ways)
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given coins and an amount, return the number of combinations that make up that amount.

```
Input:  coins = [1,2,5], amount = 5
Output: 4   // 5; 2+2+1; 2+1+1+1; 1+1+1+1+1
```

---

## Intuition

Similar to Coin Change but counting ways instead of minimum coins. To avoid counting permutations (e.g., [1,2] and [2,1] as different), iterate coins in outer loop and amounts in inner loop.

`dp[i]` = number of ways to make amount `i`. For each coin, for each amount ≥ coin: `dp[i] += dp[i - coin]`.

---

## Code — Java

```java
public int change(int amount, int[] coins) {
    int[] dp = new int[amount + 1];
    dp[0] = 1; // one way to make 0: use no coins

    for (int coin : coins) {
        for (int i = coin; i <= amount; i++) {
            dp[i] += dp[i - coin];
        }
    }
    return dp[amount];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(amount * coins) |
| Space | O(amount) |

---

## Key Insight

- Outer loop = coins, inner loop = amounts → counts **combinations** (order doesn't matter).
- Outer loop = amounts, inner loop = coins → counts **permutations** (order matters).

---

## Related Problems

- **Coin Change (LC 322)** — minimum coins
- **Partition Equal Subset Sum (LC 416)** — subset knapsack
