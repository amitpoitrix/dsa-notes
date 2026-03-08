# Cheapest Flights Within K Stops — LC #787

**Pattern:** Bellman-Ford / BFS with constraint
**Difficulty:** Medium
**Companies:** Amazon · Google · Uber

---

## Problem

Find cheapest price from `src` to `dst` with at most `k` stops.

---

## Code — Java (Bellman-Ford, k+1 rounds)

```java
public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
    int[] prices = new int[n];
    Arrays.fill(prices, Integer.MAX_VALUE);
    prices[src] = 0;

    for (int i = 0; i <= k; i++) {
        int[] temp = Arrays.copyOf(prices, n);
        for (int[] f : flights) {
            if (prices[f[0]] == Integer.MAX_VALUE) continue;
            if (prices[f[0]] + f[2] < temp[f[1]]) temp[f[1]] = prices[f[0]] + f[2];
        }
        prices = temp;
    }
    return prices[dst] == Integer.MAX_VALUE ? -1 : prices[dst];
}
```

---

## Complexity — O(k * E) time, O(n) space

---

## Key: Use temp array to prevent using edges from same round (Bellman-Ford constraint).
