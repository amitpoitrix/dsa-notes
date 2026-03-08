# Merge Two Sorted Lists — LC #21

**Pattern:** Two Pointer Merge
**Difficulty:** Easy
**Companies:** Amazon · Google · Meta · Microsoft

---

## Problem

Merge two sorted linked lists and return the sorted merged list.

```
Input:  l1=1→2→4, l2=1→3→4
Output: 1→1→2→3→4→4
```

---

## Code — Java

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) { curr.next = l1; l1 = l1.next; }
        else { curr.next = l2; l2 = l2.next; }
        curr = curr.next;
    }
    curr.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(m+n) | |
| Space | O(1)   | |
