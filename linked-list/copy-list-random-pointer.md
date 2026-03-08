# Copy List with Random Pointer — LC #138

**Pattern:** HashMap Clone
**Difficulty:** Medium
**Companies:** Amazon · Microsoft · Meta

---

## Problem

Deep copy a linked list where each node has a `next` and `random` pointer (random can point to any node or null).

---

## Code — Java

```java
public Node copyRandomList(Node head) {
    if (head == null) return null;
    Map<Node, Node> map = new HashMap<>();

    // first pass: create all new nodes
    Node curr = head;
    while (curr != null) {
        map.put(curr, new Node(curr.val));
        curr = curr.next;
    }

    // second pass: assign next and random
    curr = head;
    while (curr != null) {
        map.get(curr).next = map.get(curr.next);
        map.get(curr).random = map.get(curr.random);
        curr = curr.next;
    }
    return map.get(head);
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two passes |
| Space | O(n) | HashMap |
