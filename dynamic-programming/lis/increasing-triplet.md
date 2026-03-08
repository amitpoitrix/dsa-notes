# Increasing Triplet Subsequence — LC #334

**Pattern:** Greedy (LIS variant)
**Difficulty:** Medium
**Companies:** Facebook · Amazon

---

## Problem

Given array, return true if there exist indices i < j < k such that `nums[i] < nums[j] < nums[k]`.

```
Input:  nums = [2,1,5,0,4,6]
Output: true   // 1 < 4 < 6
```

---

## Intuition

Greedy with two variables: `first` (smallest seen), `second` (smallest value larger than some previous first). If any `num > second` → return true. Update `first` and `second` greedily to keep them as small as possible.

---

## Code — Java

```java
public boolean increasingTriplet(int[] nums) {
    int first = Integer.MAX_VALUE, second = Integer.MAX_VALUE;

    for (int num : nums) {
        if (num <= first) first = num;
        else if (num <= second) second = num;
        else return true; // num > second > first
    }
    return false;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n) |
| Space | O(1) |

---

## Common Mistakes

- Thinking you need to track indices — only values matter for existence check.

---

## Related Problems

- **LIS (LC 300)** — find actual length of LIS
