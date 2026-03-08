# Find Peak Element — LC #162

**Pattern:** Binary Search
**Difficulty:** Medium
**Companies:** Google · Microsoft · Amazon

---

## Problem

Given array `nums`, find a peak element (greater than its neighbors). Return any peak index. Must run in O(log n).

```
Input:  nums = [1, 2, 3, 1]
Output: 2   // nums[2] = 3 is a peak
```

---

## Intuition

If `nums[mid] < nums[mid+1]`, a peak exists on the right (elements are rising). Otherwise, a peak exists on the left (including mid). Binary search converges on a peak.

---

## Code — Java

```java
public int findPeakElement(int[] nums) {
    int L = 0, R = nums.length - 1;

    while (L < R) {
        int mid = L + (R - L) / 2;
        if (nums[mid] < nums[mid + 1]) L = mid + 1; // peak is to the right
        else R = mid;                                // peak is at mid or left
    }
    return L;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(log n) | |
| Space | O(1)     | |

---

## Related Problems

- **Find Minimum in Rotated Sorted Array (LC 153)** — similar convergence logic
