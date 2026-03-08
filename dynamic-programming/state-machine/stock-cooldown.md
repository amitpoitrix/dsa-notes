# Best Time to Buy and Sell Stock with Cooldown — LC #309

**Pattern:** State Machine DP
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Unlimited transactions but after selling, must wait 1 day (cooldown) before buying again.

```
Input:  prices = [1,2,3,0,2]
Output: 3   // buy(1), sell(2), cooldown, buy(0), sell(2)
```

---

## Intuition

3 states: `held` (holding stock), `sold` (just sold, in cooldown), `rest` (not holding, past cooldown). Transitions: `held = max(held, rest - price)`, `sold = held + price`, `rest = max(rest, sold)`.

---

## Code — Java

```java
public int maxProfit(int[] prices) {
    int held = Integer.MIN_VALUE, sold = 0, rest = 0;

    for (int price : prices) {
        int prevSold = sold;
        sold = held + price;
        held = Math.max(held, rest - price);
        rest = Math.max(rest, prevSold);
    }
    return Math.max(sold, rest);
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

- **Stock III (LC 123)** — limited transactions
- **Stock with Fee (LC 714)** — transaction fee instead of cooldown
