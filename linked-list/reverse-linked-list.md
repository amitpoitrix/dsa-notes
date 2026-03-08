# Reverse Linked List — LC #206

**Pattern:** Iterative / Recursive
**Difficulty:** Easy
**Companies:** Amazon · Google · Meta · Microsoft · Everywhere

---

## Problem

Reverse a singly linked list.

```
Input:  1 → 2 → 3 → 4 → 5
Output: 5 → 4 → 3 → 2 → 1
```

---

## Code — Java (Iterative)

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null, curr = head;

    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

---

## Code — Java (Recursive)

```java
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode newHead = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return newHead;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | |
| Space | O(1) iterative / O(n) recursive | Call stack |

---

## Common Mistakes

- Losing reference to `curr.next` before updating — always save `next` first.
