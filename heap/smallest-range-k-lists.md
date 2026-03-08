# Smallest Range Covering K Lists — LC #632

**Pattern:** Heap (Min-Heap) + Sliding Range
**Difficulty:** Hard
**Companies:** Google · Airbnb

---

## Problem

Given `k` sorted lists, find the smallest range `[a, b]` such that at least one number from each list is in `[a, b]`.

```
Input:  [[4,10,15,24,26],[0,9,12,20],[5,18,22,30]]
Output: [20,24]
```

---

## Intuition

Use a min-heap holding one element from each list (initially the first element). Track the current max across all heap elements. The range is `[heap min, current max]`. To shrink the range, advance the list that contributed the minimum. Stop when any list is exhausted.

---

## Algorithm

1. Push `(value, listIndex, elementIndex)` of each list's first element.
2. Track `currentMax` = max of all initial elements.
3. While heap has k elements:
   - `min = heap.peek()`. Range = `[min, currentMax]`. Update best.
   - Pop min, push next element from same list.
   - Update `currentMax` if new element is larger.
   - If list exhausted → stop.
4. Return best range.

---

## Code — Java

```java
public int[] smallestRange(List<List<Integer>> nums) {
    // [value, listIdx, elemIdx]
    PriorityQueue<int[]> heap = new PriorityQueue<>((a,b) -> a[0]-b[0]);
    int max = Integer.MIN_VALUE;

    for (int i = 0; i < nums.size(); i++) {
        heap.offer(new int[]{nums.get(i).get(0), i, 0});
        max = Math.max(max, nums.get(i).get(0));
    }

    int[] best = {heap.peek()[0], max};

    while (true) {
        int[] curr = heap.poll();
        int val = curr[0], li = curr[1], ei = curr[2];

        if (ei + 1 == nums.get(li).size()) break; // list exhausted

        int next = nums.get(li).get(ei + 1);
        heap.offer(new int[]{next, li, ei + 1});
        max = Math.max(max, next);

        int[] top = heap.peek();
        if (max - top[0] < best[1] - best[0]) {
            best = new int[]{top[0], max};
        }
    }
    return best;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(N log k) | N total elements, heap size k |
| Space | O(k) | Heap |

---

## Edge Cases

- Single list → range is `[min, max]` of that list.
- All lists have single element → range spans min to max of those elements.

---

## Common Mistakes

- Not tracking running max — can't compute range without knowing current max.
- Stopping too late — must stop as soon as any list is exhausted (can't cover all k lists anymore).

---

## Related Problems

- **Merge K Sorted Lists (LC 23)** — same heap structure
- **Find Median from Data Stream (LC 295)** — two heap design
