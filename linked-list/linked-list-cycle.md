# Linked List Cycle — LC #141

**Pattern:** Fast / Slow Pointer (Floyd's)
**Difficulty:** Easy
**Companies:** Amazon · Microsoft · Meta

---

## Problem

Given linked list, return `true` if it has a cycle.

---

## Code — Java

```java
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | |
| Space | O(1) | |

---

## Related Problems

- **Linked List Cycle II (LC 142)** — find the cycle start node
- **Find Duplicate Number (LC 287)** — same Floyd's pattern on array
