# Reorder List — LC #143

**Pattern:** Find Middle + Reverse + Merge
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Problem

Reorder list: L0→L1→...→Ln to L0→Ln→L1→Ln-1→L2→Ln-2→...

```
Input:  1→2→3→4→5
Output: 1→5→2→4→3
```

---

## Algorithm

1. Find middle (slow/fast pointer).
2. Reverse second half.
3. Merge the two halves alternately.

---

## Code — Java

```java
public void reorderList(ListNode head) {
    // 1. find middle
    ListNode slow = head, fast = head;
    while (fast.next != null && fast.next.next != null) {
        slow = slow.next; fast = fast.next.next;
    }

    // 2. reverse second half
    ListNode second = slow.next;
    slow.next = null;
    ListNode prev = null;
    while (second != null) {
        ListNode next = second.next;
        second.next = prev; prev = second; second = next;
    }

    // 3. merge
    ListNode first = head; second = prev;
    while (second != null) {
        ListNode tmp1 = first.next, tmp2 = second.next;
        first.next = second;
        second.next = tmp1;
        first = tmp1; second = tmp2;
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Three passes |
| Space | O(1) | In-place |
