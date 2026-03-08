# Capacity to Ship Packages in D Days — LC #1011

**Pattern:** Binary Search on Answer Space
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given `weights` array and `days`, find the minimum weight capacity of a ship to ship all packages within `days` days (packages shipped in order, each day's load <= capacity).

```
Input:  weights = [1,2,3,4,5,6,7,8,9,10], days = 5
Output: 15
```

---

## Intuition

Binary search on capacity. Range: `max(weights)` (must carry heaviest package) to `sum(weights)` (ship all in one day). For a given capacity, simulate and count days needed.

---

## Code — Java

```java
public int shipWithinDays(int[] weights, int days) {
    int L = Arrays.stream(weights).max().getAsInt();
    int R = Arrays.stream(weights).sum();

    while (L < R) {
        int mid = L + (R - L) / 2;
        if (canShip(weights, days, mid)) R = mid;
        else L = mid + 1;
    }
    return L;
}

private boolean canShip(int[] weights, int days, int capacity) {
    int daysNeeded = 1, load = 0;
    for (int w : weights) {
        if (load + w > capacity) {
            daysNeeded++;
            load = 0;
        }
        load += w;
    }
    return daysNeeded <= days;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log S) | S = sum of weights |
| Space | O(1)       | |

---

## Related Problems

- **Koko Eating Bananas (LC 875)** — identical pattern
- **Split Array Largest Sum (LC 410)** — same binary search on answer
