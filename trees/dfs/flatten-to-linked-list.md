# Flatten Binary Tree to Linked List — LC #114

**Pattern:** DFS (Morris / Iterative)
**Difficulty:** Medium
**Companies:** Amazon · Microsoft

---

## Problem

Flatten binary tree to a linked list in-place (right pointers, all left pointers null, preorder order).

---

## Code — Java (Iterative with stack)

```java
public void flatten(TreeNode root) {
    if (root == null) return;
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.push(root);

    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        if (node.right != null) stack.push(node.right);
        if (node.left != null) stack.push(node.left);
        if (!stack.isEmpty()) node.right = stack.peek();
        node.left = null;
    }
}
```

---

## Complexity — O(n) time, O(n) space
