# Binary Search — LC #704

**Pattern:** Binary Search (Classic)
**Difficulty:** Easy
**Companies:** Everywhere

---

## Problem

Given sorted array `nums` and `target`, return index of target or -1 if not found.

```
Input:  nums = [-1,0,3,5,9,12], target = 9
Output: 4
```

---

## Code — Java

```java
public int search(int[] nums, int target) {
    int L = 0, R = nums.length - 1;

    while (L <= R) {
        int mid = L + (R - L) / 2; // avoid overflow
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) L = mid + 1;
        else R = mid - 1;
    }
    return -1;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(log n) | Halve search space each step |
| Space | O(1)     | |

---

## Key Details

- Use `mid = L + (R - L) / 2` not `(L + R) / 2` — avoids integer overflow.
- Loop condition `L <= R` (not `L < R`) — checks single element too.

---

## Common Mistakes

- `mid = (L + R) / 2` — can overflow for large arrays.
- Using `L < R` — misses the case when answer is a single element.
