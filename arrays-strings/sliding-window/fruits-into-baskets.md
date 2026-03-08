# Fruits Into Baskets — LC #904

**Pattern:** Sliding Window (Variable)
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given array `fruits` where `fruits[i]` is the type of fruit at tree `i`, you have two baskets (each holds one type). Find the maximum number of fruits you can collect from a contiguous subarray using both baskets.

```
Input:  fruits = [1, 2, 1]
Output: 3   // pick all [1, 2, 1]

Input:  fruits = [0, 1, 2, 2]
Output: 3   // [1, 2, 2]
```

---

## Intuition

Identical to "Longest Substring with At Most K Distinct Characters" with k = 2. Find the longest subarray with at most 2 distinct values.

---

## Algorithm

1. Use `HashMap<Integer, Integer>` for basket (type → count).
2. Expand R. When basket size > 2, shrink from L.
3. Track max window length.

---

## Code — Java

```java
public int totalFruit(int[] fruits) {
    Map<Integer, Integer> basket = new HashMap<>();
    int L = 0, maxLen = 0;

    for (int R = 0; R < fruits.length; R++) {
        basket.put(fruits[R], basket.getOrDefault(fruits[R], 0) + 1);

        while (basket.size() > 2) {
            basket.put(fruits[L], basket.get(fruits[L]) - 1);
            if (basket.get(fruits[L]) == 0) basket.remove(fruits[L]);
            L++;
        }
        maxLen = Math.max(maxLen, R - L + 1);
    }
    return maxLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each element added and removed at most once |
| Space | O(1) | Map has at most 3 entries at any time |

---

## Dry Run — [0, 1, 2, 2]

| R | fruit | basket           | L | maxLen |
|---|-------|------------------|---|--------|
| 0 | 0     | {0:1}            | 0 | 1      |
| 1 | 1     | {0:1, 1:1}       | 0 | 2      |
| 2 | 2     | {0:1,1:1,2:1}→shrink {1:1,2:1} | 2 | 2 |
| 3 | 2     | {1:1, 2:2}       | 2 | 3      |

**Result:** 3

---

## Edge Cases

- All same fruits → entire array.
- Only two types → entire array.

---

## Related Problems

- **Longest Substring with At Most K Distinct (LC 340)** — same problem, generalized to k
- **Max Consecutive Ones III (LC 1004)** — variable window with a replacement budget
