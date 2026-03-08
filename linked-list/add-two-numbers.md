# Add Two Numbers — LC #2

**Pattern:** Carry Simulation
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta · Microsoft

---

## Problem

Two non-empty linked lists represent non-negative integers in reverse order. Add them, return as linked list in reverse order.

```
Input:  l1=[2,4,3], l2=[5,6,4]  (342 + 465)
Output: [7,0,8]  (807)
```

---

## Code — Java

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    int carry = 0;

    while (l1 != null || l2 != null || carry != 0) {
        int sum = carry;
        if (l1 != null) { sum += l1.val; l1 = l1.next; }
        if (l2 != null) { sum += l2.val; l2 = l2.next; }
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
    }
    return dummy.next;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(max(m,n)) | |
| Space | O(max(m,n)) | Result list |

---

## Common Mistakes

- Forgetting `carry != 0` in while condition — misses the final carry digit.
