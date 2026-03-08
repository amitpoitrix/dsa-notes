# Sort List — LC #148

**Pattern:** Merge Sort on Linked List
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Sort a linked list in O(n log n) time and O(1) memory (ignoring recursion stack).

---

## Code — Java

```java
public ListNode sortList(ListNode head) {
    if (head == null || head.next == null) return head;

    // find middle and split
    ListNode mid = getMid(head);
    ListNode right = mid.next;
    mid.next = null;

    ListNode left = sortList(head);
    right = sortList(right);
    return merge(left, right);
}

private ListNode getMid(ListNode head) {
    ListNode slow = head, fast = head.next;
    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
    }
    return slow;
}

private ListNode merge(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0), curr = dummy;
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
| Time  | O(n log n) | Merge sort |
| Space | O(log n)   | Recursion stack |
