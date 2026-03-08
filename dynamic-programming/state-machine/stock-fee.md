# Best Time to Buy and Sell Stock with Transaction Fee — LC #714

**Pattern:** State Machine DP / Greedy
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Unlimited transactions but each transaction has a `fee`. Find max profit.

```
Input:  prices = [1,3,2,8,4,9], fee = 2
Output: 8
```

---

## Intuition

Two states: `cash` (not holding) and `hold` (holding stock). `hold = max(hold, cash - price)`, `cash = max(cash, hold + price - fee)`. Subtract fee when selling.

---

## Code — Java

```java
public int maxProfit(int[] prices, int fee) {
    int cash = 0, hold = Integer.MIN_VALUE;

    for (int price : prices) {
        cash = Math.max(cash, hold + price - fee); // sell
        hold = Math.max(hold, cash - price);        // buy
    }
    return cash;
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

- **Stock with Cooldown (LC 309)** — cooldown constraint
- **Stock II (LC 122)** — same but no fee
