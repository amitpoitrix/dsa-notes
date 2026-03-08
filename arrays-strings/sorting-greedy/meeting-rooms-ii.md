# Meeting Rooms II — LC #253

**Pattern:** Sort + Min-Heap (or Two-Pointer)
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Uber

---

## Problem

Given array of meeting intervals, find the minimum number of conference rooms required.

```
Input:  [[0,30],[5,10],[15,20]]
Output: 2
```

---

## Intuition

Sort by start time. Use a min-heap storing end times of active meetings. For each meeting: if earliest-ending meeting has ended (heap.peek() <= start), reuse that room (poll heap). Always push current meeting's end time.

---

## Code — Java

```java
public int minMeetingRooms(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    PriorityQueue<Integer> heap = new PriorityQueue<>(); // min-heap of end times

    for (int[] interval : intervals) {
        if (!heap.isEmpty() && heap.peek() <= interval[0]) {
            heap.poll(); // reuse room
        }
        heap.offer(interval[1]);
    }
    return heap.size();
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n) | Sort + heap operations |
| Space | O(n)       | Heap |

---

## Related Problems

- **Merge Intervals (LC 56)** — merging instead of counting
- **Task Scheduler (LC 621)** — similar resource allocation
