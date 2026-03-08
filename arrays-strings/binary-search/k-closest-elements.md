# Find K Closest Elements — LC #658

**Pattern:** Binary Search + Sliding Window
**Difficulty:** Medium
**Companies:** Google · LinkedIn

---

## Problem

Given sorted array `arr`, integer `k`, and `x`, return the `k` closest elements to `x` (sorted). When tie, prefer smaller.

```
Input:  arr = [1,2,3,4,5], k = 4, x = 3
Output: [1, 2, 3, 4]
```

---

## Intuition

Binary search for the left boundary of the window of size k. Compare `x - arr[mid]` vs `arr[mid + k] - x`. If left element is farther, shift window right.

---

## Code — Java

```java
public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int L = 0, R = arr.length - k;

    while (L < R) {
        int mid = L + (R - L) / 2;
        if (x - arr[mid] > arr[mid + k] - x) L = mid + 1;
        else R = mid;
    }

    List<Integer> result = new ArrayList<>();
    for (int i = L; i < L + k; i++) result.add(arr[i]);
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(log(n-k) + k) | Binary search + collect |
| Space | O(k)            | Output |

---

## Common Mistakes

- Comparing absolute differences directly — `x - arr[mid] > arr[mid+k] - x` works without abs since arr is sorted and mid < mid+k.

---

## Related Problems

- **K Closest Points to Origin (LC 973)** — 2D version using heap
