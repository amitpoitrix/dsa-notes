# Find Middle of Linked List — LC #876

**Pattern:** Fast / Slow Pointer
**Difficulty:** Easy
**Companies:** Amazon · Google

---

## Problem

Return the middle node. If two middles, return the second.

```
Input:  1→2→3→4→5 → return node 3
Input:  1→2→3→4   → return node 3 (second middle)
```

---

## Code — Java

```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | |
| Space | O(1) | |
