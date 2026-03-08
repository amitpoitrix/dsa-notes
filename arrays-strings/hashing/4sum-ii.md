# 4Sum II — LC #454

**Pattern:** HashMap (Split into two halves)
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given four integer arrays `A`, `B`, `C`, `D` of length `n`, count tuples `(i, j, k, l)` such that `A[i] + B[j] + C[k] + D[l] == 0`.

```
Input:  A=[1,2], B=[-2,-1], C=[-1,2], D=[0,2]
Output: 2
```

---

## Intuition

Split into two pairs. Store all `A[i] + B[j]` sums in a HashMap. For each `C[k] + D[l]`, check if `-(C[k]+D[l])` exists in the map.

---

## Code — Java

```java
public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
    Map<Integer, Integer> map = new HashMap<>();

    for (int a : A)
        for (int b : B)
            map.put(a + b, map.getOrDefault(a + b, 0) + 1);

    int count = 0;
    for (int c : C)
        for (int d : D)
            count += map.getOrDefault(-(c + d), 0);

    return count;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n²) | Two nested loops twice |
| Space | O(n²) | Map stores all A+B sums |

---

## Common Mistakes

- Trying all four arrays with 4 loops → O(n⁴). Always split into two halves.

---

## Related Problems

- **Two Sum (LC 1)** — single pair version
- **4Sum (LC 18)** — single array, no duplicates in output
