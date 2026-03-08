# Search in Rotated Sorted Array — LC #33

**Pattern:** Binary Search (Modified)
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given rotated sorted array `nums` with no duplicates, return index of `target` or -1.

```
Input:  nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

---

## Intuition

At any `mid`, one half is always sorted. Determine which half is sorted. Check if target falls within the sorted half — if yes, search there; otherwise search the other half.

---

## Algorithm

1. While `L <= R`:
   - If `nums[L] <= nums[mid]` → left half is sorted:
     - If `target` in `[nums[L], nums[mid])` → search left.
     - Else → search right.
   - Else → right half is sorted:
     - If `target` in `(nums[mid], nums[R]]` → search right.
     - Else → search left.

---

## Code — Java

```java
public int search(int[] nums, int target) {
    int L = 0, R = nums.length - 1;

    while (L <= R) {
        int mid = L + (R - L) / 2;
        if (nums[mid] == target) return mid;

        if (nums[L] <= nums[mid]) { // left half sorted
            if (target >= nums[L] && target < nums[mid]) R = mid - 1;
            else L = mid + 1;
        } else { // right half sorted
            if (target > nums[mid] && target <= nums[R]) L = mid + 1;
            else R = mid - 1;
        }
    }
    return -1;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(log n) | Still halves search space |
| Space | O(1)     | |

---

## Dry Run — [4,5,6,7,0,1,2], target=0

| L | R | mid | nums[mid] | action |
|---|---|-----|-----------|--------|
| 0 | 6 | 3   | 7         | left sorted [4..7], 0 not in it → L=4 |
| 4 | 6 | 5   | 1         | right sorted [1..2], 0 not in it → R=4 |
| 4 | 4 | 4   | 0 ✓       | found |

**Result:** 4

---

## Common Mistakes

- Using strict `<` instead of `<=` for left-sorted check — fails when L == mid (single element).
- Getting the boundary conditions wrong — draw it out carefully.

---

## Related Problems

- **Find Minimum in Rotated Sorted Array (LC 153)** — find the pivot point
- **Search in Rotated Array II (LC 81)** — with duplicates (need to handle `nums[L] == nums[mid]`)
