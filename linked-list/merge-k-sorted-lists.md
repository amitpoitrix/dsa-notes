# Merge K Sorted Lists — LC #23

**Pattern:** Min-Heap / Divide and Conquer
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Merge `k` sorted linked lists into one sorted list.

---

## Approach 1: Min-Heap

```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> heap = new PriorityQueue<>((a, b) -> a.val - b.val);
    for (ListNode node : lists) if (node != null) heap.offer(node);

    ListNode dummy = new ListNode(0), curr = dummy;
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
| Time  | O(n log k) | n total nodes, heap size k |
| Space | O(k)       | Heap |

---

## Approach 2: Divide and Conquer

Pair up lists and merge pairs recursively. O(n log k) time, O(log k) space.
