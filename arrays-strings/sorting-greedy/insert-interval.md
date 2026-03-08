# Insert Interval — LC #57

**Pattern:** Linear Scan + Merge
**Difficulty:** Medium
**Companies:** Google · LinkedIn · Microsoft

---

## Problem

Given sorted non-overlapping intervals and a new interval, insert and merge if necessary.

```
Input:  intervals=[[1,3],[6,9]], newInterval=[2,5]
Output: [[1,5],[6,9]]
```

---

## Algorithm

1. Add all intervals ending before new interval starts.
2. Merge all overlapping intervals with new interval.
3. Add the merged interval, then remaining intervals.

---

## Code — Java

```java
public int[][] insert(int[][] intervals, int[] newInterval) {
    List<int[]> result = new ArrayList<>();
    int i = 0, n = intervals.length;

    // add all before new interval
    while (i < n && intervals[i][1] < newInterval[0]) result.add(intervals[i++]);

    // merge overlapping
    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
        i++;
    }
    result.add(newInterval);

    // add remaining
    while (i < n) result.add(intervals[i++]);

    return result.toArray(new int[0][]);
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Linear scan |
| Space | O(n) | Result |

---

## Common Mistakes

- Overlap condition: intervals[i][0] <= newInterval[1] (not <).
- Boundary condition: intervals[i][1] < newInterval[0] (not <=) for "before" check.
