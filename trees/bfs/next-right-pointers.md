# Populating Next Right Pointers — LC #116

**Pattern:** BFS Level Linking
**Difficulty:** Medium
**Companies:** Microsoft · Amazon

---

## Problem

Populate each node's `next` pointer to its right neighbor at the same level.

---

## Code — Java (BFS)

```java
public Node connect(Node root) {
    if (root == null) return null;
    Queue<Node> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            Node node = queue.poll();
            if (i < size - 1) node.next = queue.peek();
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
    }
    return root;
}
```

## O(1) Space Solution (Perfect Binary Tree)

Use existing next pointers to traverse the level above and link the level below.
