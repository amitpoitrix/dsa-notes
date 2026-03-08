# Median of Two Sorted Arrays — LC #4

**Pattern:** Binary Search on Partition
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given two sorted arrays `nums1` and `nums2`, return the median of the combined arrays. Must run in O(log(m+n)).

```
Input:  nums1 = [1,3], nums2 = [2]
Output: 2.0

Input:  nums1 = [1,2], nums2 = [3,4]
Output: 2.5
```

---

## Intuition

Binary search on the partition point of the smaller array. For a valid partition: all left elements <= all right elements. The median is derived from the elements at the partition boundary.

---

## Algorithm

1. Ensure `nums1` is the smaller array.
2. Binary search on partition `i` of nums1 (0 to m). Derive partition `j` of nums2: `j = (m + n + 1) / 2 - i`.
3. Valid partition when: `maxLeft1 <= minRight2` AND `maxLeft2 <= minRight1`.
4. If `maxLeft1 > minRight2` → too many from nums1 → R = i - 1.
5. Else if `maxLeft2 > minRight1` → too few from nums1 → L = i + 1.
6. Compute median from boundary values.

---

## Code — Java

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    if (nums1.length > nums2.length) return findMedianSortedArrays(nums2, nums1);

    int m = nums1.length, n = nums2.length;
    int L = 0, R = m;

    while (L <= R) {
        int i = L + (R - L) / 2;
        int j = (m + n + 1) / 2 - i;

        int maxLeft1  = (i == 0) ? Integer.MIN_VALUE : nums1[i - 1];
        int minRight1 = (i == m) ? Integer.MAX_VALUE : nums1[i];
        int maxLeft2  = (j == 0) ? Integer.MIN_VALUE : nums2[j - 1];
        int minRight2 = (j == n) ? Integer.MAX_VALUE : nums2[j];

        if (maxLeft1 <= minRight2 && maxLeft2 <= minRight1) {
            if ((m + n) % 2 == 1) return Math.max(maxLeft1, maxLeft2);
            return (Math.max(maxLeft1, maxLeft2) + Math.min(minRight1, minRight2)) / 2.0;
        } else if (maxLeft1 > minRight2) {
            R = i - 1;
        } else {
            L = i + 1;
        }
    }
    return 0.0;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(log(min(m,n))) | Binary search on smaller array |
| Space | O(1)             | |

---

## Common Mistakes

- Not handling edge cases where partition is at 0 or at full array length — use MIN/MAX_VALUE sentinels.
- Searching on the larger array — always binary search on the smaller one.

---

## Related Problems

- **Kth Smallest Element in Sorted Matrix (LC 378)** — binary search on value
