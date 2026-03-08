# Merge Intervals — LC #56

**Pattern:** Sort + Merge
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given array of intervals, merge all overlapping intervals.

```
Input:  [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
```

---

## Algorithm

1. Sort by start time.
2. Add first interval to result.
3. For each interval: if it overlaps with last in result (start <= last.end), merge by updating end = max(last.end, curr.end). Else add new interval.

---

## Code — Java

```java
public int[][] merge(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    List<int[]> result = new ArrayList<>();
    result.add(intervals[0]);

    for (int i = 1; i < intervals.length; i++) {
        int[] last = result.get(result.size() - 1);
        if (intervals[i][0] <= last[1]) {
            last[1] = Math.max(last[1], intervals[i][1]);
        } else {
            result.add(intervals[i]);
        }
    }
    return result.toArray(new int[0][]);
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n) | Sort dominates |
| Space | O(n)       | Result list |

---

## Common Mistakes

- Not taking `max` when merging end — `[1,10],[2,3]` should stay `[1,10]`, not become `[1,3]`.
