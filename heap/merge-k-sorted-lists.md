# Merge K Sorted Lists — LC #23

**Pattern:** Heap (Min-Heap)
**Difficulty:** Hard
**Companies:** Amazon · Google · Microsoft · Facebook

---

## Problem

Given an array of `k` linked lists, each sorted in ascending order, merge them all and return one sorted list.

```
Input:  [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
```

---

## Intuition

Use a min-heap to always pick the smallest current node across all lists. Push the head of each list into the heap. Each time you pop the minimum, push its next node. Repeat until heap is empty.

---

## Algorithm

1. Push head of every non-null list into min-heap (ordered by node value).
2. While heap is not empty:
   - Poll minimum node, append to result.
   - If polled node has a next → push it to heap.
3. Return result.

---

## Code — Java

```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> heap = new PriorityQueue<>(
        (a, b) -> a.val - b.val
    );

    for (ListNode node : lists) {
        if (node != null) heap.offer(node);
    }

    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;

    while (!heap.isEmpty()) {
        ListNode node = heap.poll();
        curr.next = node;
        curr = curr.next;
        if (node.next != null) heap.offer(node.next);
    }
    return dummy.next;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(N log k) | N total nodes, heap size k |
| Space | O(k) | Heap holds at most k nodes at once |

---

## Dry Run — [[1,4,5],[1,3,4],[2,6]]

Initial heap: {1(L1), 1(L2), 2(L3)}

| Poll | Append | Push next | Heap |
|------|--------|-----------|------|
| 1(L1) | 1 | 4(L1) | {1(L2),2,4} |
| 1(L2) | 1 | 3(L2) | {2,4,3} |
| 2(L3) | 2 | 6(L3) | {3,4,6} |
| 3(L2) | 3 | 4(L2) | {4,4,6} |
| 4(L1) | 4 | 5(L1) | {4,5,6} |
| 4(L2) | 4 | none  | {5,6} |
| 5     | 5 | none  | {6} |
| 6     | 6 | none  | {} |

**Result:** 1→1→2→3→4→4→5→6

---

## Edge Cases

- Empty input `[]` → return null.
- Lists with nulls — check before pushing to heap.
- Single list → return it directly.

---

## Common Mistakes

- Pushing null nodes to heap → NullPointerException.
- Not using a dummy head node — makes handling the result list simpler.

---

## Related Problems

- **Merge Two Sorted Lists (LC 21)** — simpler two-pointer merge
- **Kth Smallest Element in Sorted Matrix (LC 378)** — heap on matrix rows
- **Find Median from Data Stream (LC 295)** — heap-based design
