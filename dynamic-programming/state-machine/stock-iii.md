# Best Time to Buy and Sell Stock III — LC #123

**Pattern:** State Machine DP
**Difficulty:** Hard
**Companies:** Amazon · Google · Facebook

---

## Problem

Given prices array, find maximum profit with at most 2 transactions. Must sell before buying again.

```
Input:  prices = [3,3,5,0,0,3,1,4]
Output: 6   // buy at 0, sell at 3, buy at 1, sell at 4
```

---

## Intuition

State machine with 4 states: `buy1`, `sell1`, `buy2`, `sell2`. Each day, update all states optimally. `buy1` = max profit after first buy, `sell1` = after first sell, `buy2` = after second buy, `sell2` = after second sell.

---

## Code — Java

```java
public int maxProfit(int[] prices) {
    int buy1 = Integer.MIN_VALUE, sell1 = 0;
    int buy2 = Integer.MIN_VALUE, sell2 = 0;

    for (int price : prices) {
        buy1  = Math.max(buy1,  -price);
        sell1 = Math.max(sell1, buy1 + price);
        buy2  = Math.max(buy2,  sell1 - price);
        sell2 = Math.max(sell2, buy2 + price);
    }
    return sell2;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n) |
| Space | O(1) |

---

## Key Insight

`buy2 = sell1 - price` accounts for profit from first transaction when computing second buy. State transitions happen in order, so all 4 can update in the same loop.

---

## Related Problems

- **Stock I (LC 121)** — one transaction
- **Stock II (LC 122)** — unlimited transactions
- **Stock IV (LC 188)** — at most k transactions
- **Stock with Cooldown (LC 309)** — cooldown after sell
