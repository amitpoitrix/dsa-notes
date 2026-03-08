# Best Time to Buy and Sell Stock — LC #121

**Pattern:** Kadane's Variant / Single Pass
**Difficulty:** Easy
**Companies:** Amazon · Google · Meta · Microsoft · Everywhere

---

## Problem

Given `prices` array where `prices[i]` is the price on day `i`, find the maximum profit from one transaction.

```
Input:  [7, 1, 5, 3, 6, 4]
Output: 5   // Buy at 1, sell at 6
```

---

## Intuition

Track the minimum price seen so far. For each day, compute `profit = prices[i] - minPrice`. Update max profit.

---

## Code — Java

```java
public int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE;
    int maxProfit = 0;

    for (int price : prices) {
        minPrice = Math.min(minPrice, price);
        maxProfit = Math.max(maxProfit, price - minPrice);
    }
    return maxProfit;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | |

---

## Common Mistakes

- Buying after selling — tracking minPrice ensures we always buy before the current day.
- Using nested loops → O(n²).

---

## Related Problems

- **Best Time II (LC 122)** — multiple transactions
- **Best Time III (LC 123)** — at most 2 transactions (DP)
- **Best Time with Cooldown (LC 309)** — state machine DP
