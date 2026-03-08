# Remove Nth Node From End — LC #19

**Pattern:** Two Pointer (Gap)
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Remove the nth node from the end in one pass.

```
Input:  1→2→3→4→5, n=2
Output: 1→2→3→5
```

---

## Intuition

Use two pointers with a gap of n. Move fast n steps ahead. Then move both until fast reaches the end. Slow is now at the node just before the one to remove.

---

## Code — Java

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode slow = dummy, fast = dummy;

    for (int i = 0; i <= n; i++) fast = fast.next; // move fast n+1 steps

    while (fast != null) { slow = slow.next; fast = fast.next; }

    slow.next = slow.next.next;
    return dummy.next;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | |

---

## Common Mistakes

- Moving fast `n` steps vs `n+1` steps — need `n+1` so slow stops at the predecessor.
- Not using dummy node — edge case when removing the head.
