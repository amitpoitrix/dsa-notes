# Non-overlapping Intervals — LC #435

**Pattern:** Greedy (Sort by End Time)
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given intervals, find the minimum number of intervals to remove to make the rest non-overlapping.

```
Input:  [[1,2],[2,3],[3,4],[1,3]]
Output: 1   // remove [1,3]
```

---

## Intuition

Greedy: sort by end time. Keep as many non-overlapping intervals as possible. When two intervals overlap, remove the one with the later end time (greedy — keeps more room for future intervals).

---

## Code — Java

```java
public int eraseOverlapIntervals(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[1] - b[1]); // sort by end
    int count = 0, end = Integer.MIN_VALUE;

    for (int[] interval : intervals) {
        if (interval[0] >= end) {
            end = interval[1]; // keep this interval
        } else {
            count++; // remove this interval (it overlaps and has later end)
        }
    }
    return count;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n) | Sort |
| Space | O(1)       | |

---

## Common Mistakes

- Sorting by start instead of end — greedy correctness requires sorting by end.
