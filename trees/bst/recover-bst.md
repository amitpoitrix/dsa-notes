# Recover Binary Search Tree — LC #99

**Pattern:** Inorder Traversal (Find Swapped Nodes)
**Difficulty:** Hard
**Companies:** Amazon · Microsoft

---

## Problem

Two nodes in a BST are swapped by mistake. Recover the tree without changing structure.

---

## Intuition

Inorder traversal of valid BST is sorted. Find where the order is violated — there will be 1 or 2 such violations. The two swapped nodes are the first node in the first violation and the second node in the second (or first) violation.

---

## Code — Java

```java
TreeNode first, second, prev;

public void recoverTree(TreeNode root) {
    inorder(root);
    int temp = first.val;
    first.val = second.val;
    second.val = temp;
}

private void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    if (prev != null && prev.val > node.val) {
        if (first == null) first = prev;
        second = node;
    }
    prev = node;
    inorder(node.right);
}
```

## Complexity — O(n) time, O(h) space
