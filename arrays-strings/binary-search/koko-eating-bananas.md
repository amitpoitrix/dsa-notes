# Koko Eating Bananas — LC #875

**Pattern:** Binary Search on Answer Space
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Problem

Koko has `n` piles of bananas and `h` hours. She eats at speed `k` bananas/hour (one pile per hour). Find the minimum `k` such that she can eat all piles within `h` hours.

```
Input:  piles = [3,6,7,11], h = 8
Output: 4
```

---

## Intuition

Binary search on the answer (`k`). Range: 1 to max(piles). For a given speed `k`, hours needed = `sum(ceil(pile/k))`. Find minimum `k` where hours <= h.

---

## Algorithm

1. `L = 1`, `R = max(piles)`.
2. Binary search: for each `mid` speed, compute total hours.
3. If `hours <= h` → try smaller speed (R = mid).
4. Else → need faster speed (L = mid + 1).

---

## Code — Java

```java
public int minEatingSpeed(int[] piles, int h) {
    int L = 1, R = Arrays.stream(piles).max().getAsInt();

    while (L < R) {
        int mid = L + (R - L) / 2;
        int hours = 0;
        for (int pile : piles) hours += (pile + mid - 1) / mid; // ceil(pile/mid)

        if (hours <= h) R = mid;    // can eat slower
        else L = mid + 1;           // need to eat faster
    }
    return L;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log m) | log m iterations, O(n) check each |
| Space | O(1)       | |

---

## Key Pattern

"Binary search on answer space" template:
- Define the answer range [L, R].
- Define a `feasible(mid)` check function.
- Find minimum mid where feasible is true.

---

## Common Mistakes

- Using `(pile / mid)` instead of `ceil(pile / mid)` — underestimates hours.
- Ceiling formula: `(pile + mid - 1) / mid` or `(int) Math.ceil((double) pile / mid)`.

---

## Related Problems

- **Capacity to Ship Packages (LC 1011)** — same binary search on answer pattern
- **Split Array Largest Sum (LC 410)** — same pattern
- **Minimum Days to Make Bouquets (LC 1482)** — same pattern
