# Best Time to Buy and Sell Stock II — LC #122

**Pattern:** Greedy
**Difficulty:** Medium
**Companies:** Amazon · Microsoft · Google

---

## Problem

Given `prices`, find maximum profit with unlimited transactions (must sell before buying again).

```
Input:  [7, 1, 5, 3, 6, 4]
Output: 7   // Buy at 1, sell at 5 (profit 4) + Buy at 3, sell at 6 (profit 3)
```

---

## Intuition

Collect every upward movement. If `prices[i] > prices[i-1]`, take that profit. This is equivalent to summing all positive day-to-day differences.

---

## Code — Java

```java
public int maxProfit(int[] prices) {
    int profit = 0;
    for (int i = 1; i < prices.length; i++) {
        if (prices[i] > prices[i - 1]) {
            profit += prices[i] - prices[i - 1];
        }
    }
    return profit;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | |

---

## Related Problems

- **Best Time I (LC 121)** — single transaction
- **Best Time III (LC 123)** — at most 2 transactions
