# Russian Doll Envelopes — LC #354

**Pattern:** 2D LIS
**Difficulty:** Hard
**Companies:** Google · Facebook

---

## Problem

Envelopes `[w, h]`. Can put one inside another if both width and height strictly increase. Find maximum envelopes you can nest.

```
Input:  [[5,4],[6,4],[6,7],[2,3]]
Output: 3   // [2,3] → [5,4] → [6,7]
```

---

## Intuition

Sort by width ascending, then height **descending** (for same width). Then find LIS on heights only. Descending heights for same width ensures we can't pick two envelopes with same width (they'd never be part of the same LIS).

---

## Code — Java

```java
public int maxEnvelopes(int[][] envelopes) {
    Arrays.sort(envelopes, (a, b) -> a[0] == b[0] ? b[1] - a[1] : a[0] - b[0]);

    int[] tails = new int[envelopes.length];
    int size = 0;

    for (int[] env : envelopes) {
        int h = env[1];
        int lo = 0, hi = size;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (tails[mid] < h) lo = mid + 1;
            else hi = mid;
        }
        tails[lo] = h;
        if (lo == size) size++;
    }
    return size;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n log n) |
| Space | O(n) |

---

## Common Mistakes

- Sorting heights ascending for same width — allows picking multiple same-width envelopes.

---

## Related Problems

- **LIS (LC 300)** — 1D version of this
