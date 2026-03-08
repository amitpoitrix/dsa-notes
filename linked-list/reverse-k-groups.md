# Reverse Linked List in K-Groups — LC #25

**Pattern:** Group Reversal
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Reverse nodes of linked list in groups of `k`. Leave remaining nodes (< k) as is.

```
Input:  1→2→3→4→5, k=2
Output: 2→1→4→3→5
```

---

## Algorithm

1. Check if k nodes exist ahead.
2. Reverse k nodes.
3. Connect: prev group's tail → reversed head, reversed tail → next group.
4. Recurse/iterate on remaining.

---

## Code — Java

```java
public ListNode reverseKGroup(ListNode head, int k) {
    ListNode curr = head;
    int count = 0;
    while (curr != null && count < k) { curr = curr.next; count++; }
    if (count < k) return head; // less than k nodes, don't reverse

    // reverse k nodes
    ListNode prev = null; curr = head;
    for (int i = 0; i < k; i++) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    head.next = reverseKGroup(curr, k); // head is now the tail
    return prev; // prev is the new head
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | |
| Space | O(n/k) | Recursion stack |

---

## Common Mistakes

- Not checking if k nodes remain — leave remaining nodes unchanged.
