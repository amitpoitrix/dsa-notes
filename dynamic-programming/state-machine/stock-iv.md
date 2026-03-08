# Best Time to Buy and Sell Stock IV — LC #188

**Pattern:** State Machine DP
**Difficulty:** Hard
**Companies:** Amazon · Google

---

## Problem

At most `k` transactions. Find max profit.

```
Input:  k = 2, prices = [2,4,1]
Output: 2
```

---

## Intuition

Generalize Stock III. Use arrays `buy[k]` and `sell[k]`. If `k >= n/2`, unlimited transactions (use Stock II greedy). Otherwise DP with 2k states.

---

## Code — Java

```java
public int maxProfit(int k, int[] prices) {
    int n = prices.length;
    if (k >= n / 2) return quickSolve(prices); // unlimited

    int[] buy = new int[k], sell = new int[k];
    Arrays.fill(buy, Integer.MIN_VALUE);

    for (int price : prices) {
        for (int i = k - 1; i > 0; i--) {
            sell[i] = Math.max(sell[i], buy[i] + price);
            buy[i]  = Math.max(buy[i],  sell[i-1] - price);
        }
        sell[0] = Math.max(sell[0], buy[0] + price);
        buy[0]  = Math.max(buy[0],  -price);
    }
    return sell[k-1];
}

private int quickSolve(int[] prices) {
    int profit = 0;
    for (int i = 1; i < prices.length; i++)
        if (prices[i] > prices[i-1]) profit += prices[i] - prices[i-1];
    return profit;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n*k) |
| Space | O(k) |

---

## Related Problems

- **Stock III (LC 123)** — k=2
- **Stock II (LC 122)** — unlimited
