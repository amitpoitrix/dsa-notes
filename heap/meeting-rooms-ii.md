# Meeting Rooms II — LC #253

**Pattern:** Heap (Min-Heap) / Greedy
**Difficulty:** Medium
**Companies:** Google · Facebook · Amazon · Uber

---

## Problem

Given an array of meeting intervals `[start, end]`, find the minimum number of conference rooms required.

```
Input:  [[0,30],[5,10],[15,20]]
Output: 2
```

---

## Intuition

Sort intervals by start time. Use a min-heap of end times. For each new meeting, check if the earliest-ending room is free (its end ≤ new start). If yes, reuse it (update end time in heap). If no, allocate a new room. Heap size = rooms in use = answer.

---

## Algorithm

1. Sort intervals by start time.
2. Push first interval's end time to min-heap.
3. For each subsequent interval:
   - If `heap.peek() <= interval.start` → `heap.poll()` (reuse that room).
   - Push `interval.end` to heap (assign this meeting to a room).
4. Return `heap.size()`.

---

## Code — Java

```java
public int minMeetingRooms(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

    PriorityQueue<Integer> minHeap = new PriorityQueue<>(); // end times
    for (int[] interval : intervals) {
        if (!minHeap.isEmpty() && minHeap.peek() <= interval[0]) {
            minHeap.poll(); // room is free, reuse it
        }
        minHeap.offer(interval[1]); // assign room, record end time
    }
    return minHeap.size();
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n) | Sort + heap ops |
| Space | O(n) | Heap holds all rooms |

---

## Dry Run — [[0,30],[5,10],[15,20]]

Sorted: [[0,30],[5,10],[15,20]]

| interval | heap.peek() | free? | heap after |
|----------|-------------|-------|------------|
| [0,30]  | — (empty)   | —     | [30] |
| [5,10]  | 30 > 5      | no    | [10,30] |
| [15,20] | 10 ≤ 15     | yes, pop 10 | [20,30] |

**heap.size() = 2** ✓

---

## Edge Cases

- No overlap → 1 room.
- All overlap → n rooms.
- Meeting ending exactly when next starts `[5,10],[10,15]` → `10 <= 10` → reuse same room.

---

## Common Mistakes

- Using `<` instead of `<=` for free-room check — a room ending at time 10 can host a meeting starting at 10.
- Not sorting by start time first.

---

## Related Problems

- **Merge Intervals (LC 56)** — sorting + merging overlapping
- **Non-overlapping Intervals (LC 435)** — remove minimum to avoid overlap
- **Task Scheduler (LC 621)** — schedule with constraints
